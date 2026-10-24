# Technical notes - 24 October 2026

The tested machine ran CachyOS, Wine 11.20 and FL26 2.2 / executable 26.2.0.3. All experiments were in a separate game copy and Wine prefix.

1. `Settings > Edit Mode` is redirected to `TopMenu/TopMenuModeInit` in the experimental copy.
2. The Sider module changes the native mode manager to `ONLINE_LOBBY` (26) when its initializer JSON is read. The ordinary installation remains unchanged.
3. The online initializer event points to `Online/Login/LoginFlow`. Native login dispatch routes to the lobby.
4. At executable offset `0xbc9496`, initialization flags change from `00000100` to `00ef0100` (0x10000 to 0x1ef00). Only byte 0xbc9497 differs on disk. Patched SHA-256: `8fefd36ed9643f736bace53241a214b167a851bc5f903465c33ad85d277254f4`.
5. The local `LiveDataSetFlowOnMode` was observed waiting indefinitely on a blank panel. The test module guards and replaces the local flow-selector entry with `xor eax,eax; ret`, allowing the native task's existing no-local-flow path. Login/account/menu result checks are retained. This is a workaround, not a proven diagnosis of every underlying cause.
6. Each test profile uses its own player's locally selected Steam identity. No identity is bundled. Do not copy another player's sys.ini.
7. Only `online-mode.lua` is enabled in the test Sider configuration. No Stat Editor/trainer module is enabled.

The game established TCP service connections to the PESBUL endpoint on ports 10000 and 10001. The UI then showed the Europe server list, room list, own room and another player's room. Full peer-to-peer match traffic was not validated.

The 0x10000 flag was initially misidentified as a Live Update switch. That interpretation was incorrect; the source code and notes here preserve the corrected final 0x1ef00 setup.

Checks completed locally: generated JSON matches all four working overrides; patching a private executable copy gives the expected target hash; another executable is rejected; Python and Lua parse; guide navigation/persistence/path substitution unit checks pass. These checks do not replace a Windows runtime or two-player match test.
