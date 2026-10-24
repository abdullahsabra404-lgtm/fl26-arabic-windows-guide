# Linux / Wine - tested configuration and reproduction

This appendix describes the arrangement tested on CachyOS with Wine 11.20. It is not an installer for every Linux distribution. Start with a working, official FL26 2.2 offline installation and a working Wine prefix. The source files support one exact executable hash; full online match completion remains unverified.

## 1. Close and isolate

Save and close the game. Set the first two paths to YOUR installation and prefix. The new directory must not already exist.

```bash
SOURCE="$HOME/Games/Windows/SP Football Life 2026"
SOURCE_PREFIX="$HOME/Games/sp-football-life-2026"
ONLINE="$HOME/Games/fl26-online"
test ! -e "$ONLINE" || { echo 'Choose a new empty destination'; exit 1; }
WINEPREFIX="$SOURCE_PREFIX" wineserver -k
WINEPREFIX="$SOURCE_PREFIX" wineserver -w
mkdir -p "$ONLINE/prefix"
cp -a --reflink=auto "$SOURCE" "$ONLINE/game"
cp -a --reflink=auto "$SOURCE_PREFIX/drive_c" "$SOURCE_PREFIX/dosdevices" \
  "$SOURCE_PREFIX/system.reg" "$SOURCE_PREFIX/user.reg" "$SOURCE_PREFIX/userdef.reg" "$ONLINE/prefix/"
ln -sfnT ../drive_c "$ONLINE/prefix/dosdevices/c:"
touch "$ONLINE/.fl26-online-copy"
```

Check free space first. `--reflink=auto` falls back to a full copy on filesystems without reflinks. Data and download must be private copies, not symlinks to the main game. The main game's saves and graphics settings were not modified in the test.

Before launching, resolve Documents inside the CLONED prefix. If it links to real home Documents or to the original prefix, stop and make a private Documents directory in the clone first. Do not treat a copied symlink as save isolation. The tested source prefix used real private Documents directories.

## 2. Apply only to the isolated copy

From the root of this repository, obtain your OWN most-recent Steam identity locally and choose an ASCII display name:

```bash
STEAM_ID="$(python3 linux/steam-identity.py)"
python3 linux/apply-copy.py --game "$ONLINE/game" --steam-id "$STEAM_ID" --name MyPlayer
```

The script refuses a target lacking the isolated-prefix marker and checks the executable. It uses the same core transformation as the Windows helper; it does not clone files or change hosts. The Steam identity reader only reads loginusers.vdf, not passwords or tokens. The source transformation is verified locally; the commands were adapted from the tested arrangement and should still be reviewed for your paths/filesystem.

## 3. PESBUL host routing

Use the [current official connector](https://pes2021.pesbul.eu/pes-2021-is-online-again/) as the authority. `connector-config.json` is the endpoint snapshot reviewed on 24 October 2026, not a promise that the IP will remain current. Recheck it against the current official BAT before applying.

```bash
sudo python3 linux/configure-linux.py install
# To remove only the marked block later:
# sudo python3 linux/configure-linux.py remove
```

The helper backs up hosts before installing the marked mappings and refuses conflicting mappings. It does not disable a firewall, open router ports or restart local AI services. No new game assets are downloaded.

## 4. Launch

```bash
bash linux/start-online.sh "$ONLINE"
```

On the tested i9-14900KF, the direct game launch needed affinity to CPUs 0-15 (performance cores). For that machine:

```bash
FL26_CPUSET=0-15 bash linux/start-online.sh "$ONLINE"
```

Do not copy that affinity to another CPU without checking its topology. A normal FL start executable was unreliable under Wine in the test, so this script starts Sider first and then FL_2026.exe directly. It does not replace the ordinary launcher.

At the title screen press Enter/X. Then Settings (gear) > Edit Mode > Europe > Create Match Room > Next > Next. Edit Mode is repurposed ONLY in this copy. Another player must join; both players select Start Match. Server selection, room creation, join and one local ready state were verified; kickoff/completion were not.

## Controller and limitations

The tested DualSense worked after a prefix-scoped `winebus DisableHidraw=1` change and in-game verification. Preserve a registry rollback before changing this on another prefix. A process launch alone does not establish controller support.

Keep trainers out of the online copy. A room working does not prove peer-to-peer connectivity, matching databases or cross-platform compatibility.
