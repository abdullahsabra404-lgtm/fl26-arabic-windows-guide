# Football Life 2026: Arabic guide, Windows and Linux

**Unofficial community review edition. Not endorsed by SmokePatch or PESBUL.**

## ابدأ هون

1. [نزّل دليل PDF بالسوري](FL26-Windows11-Syrian-Arabic-Guide.pdf?raw=true).
2. [نزّل الحزمة التفاعلية مع الصور والبرامج المساعدة](FL26-Windows11-Syrian-Arabic-Guide.zip?raw=true). فك ضغط ZIP وافتح **OPEN-GUIDE.html**.
3. [دليل Linux / Wine منفصل](GUIDE-LINUX.md).

[Download all original helper source code, preserving its folder structure](FL26-Source-Windows-Linux.zip?raw=true). Extract the source archive, open `fl26-source`, and follow the Linux guide from that directory. The PDF is for reading/printing; the Windows ZIP includes the interactive guide with saved progress and embedded pictures.

## What is actually verified?

| Item | Evidence/status |
|---|---|
| Main FL26 offline game under Wine | Launched; controller and match previously verified |
| Isolated Linux/Wine online copy | Reached PESBUL notices, server selection and live room list |
| Own room | Created and entered |
| Another player's room | Joined; both players displayed; local Start Match selected |
| Full online match | **Not verified**: other player did not ready during the test |
| Windows setup | Source logic checked locally; **native Windows launch not tested** |

Do not interpret a room screenshot as proof of a playable match or cross-platform compatibility. The Windows guide and Linux appendix are separate because their validation differs.

## Contents

- PDF: 36 pages, 102 steps, Syrian Arabic, annotated screenshots and website links.
- Windows ZIP: interactive guide, image attribution and experimental setup source files.
- Source ZIP: separate `windows/`, `linux/` and `docs/` directories; extract before following source commands.
- [Technical notes and validation limits](TECHNICAL-NOTES.md).
- No game binaries, CPK assets, saves, Wine prefixes or Steam account files are distributed.

The helper supports only official FL26 2.2 executable SHA-256:
`9ee0c30651e5e3c37e3d308fb8224f5fea135cd8e929dee2cddca6e041836281`.
It refuses other executable builds. Do not remove that guard or install another gameplay executable over the experimental copy.

## Official sources and support

- [SmokePatch FL26](https://www.pessmokepatch.com/2025/10/spfl26.html)
- [SmokePatch official contact](https://www.pessmokepatch.com/p/contact-us.html): `pessmokepatch@gmail.com`
- [PESBUL official instructions](https://pes2021.pesbul.eu/pes-2021-is-online-again/)
- [PESBUL Discord](https://discord.gg/GJmeG9p26w)

No official SmokePatch Discord was verified from its website/FAQ/contact pages. A community server must not be described as developer-operated without evidence.

## Review and contributions

Windows testers: report FL26 version/hash, Windows version, CPU, controller, the last completed guide step and any error. Verify launch, room creation, two-player join, actual match kickoff/completion and reconnect separately. Do not upload credentials, full prefixes, game files or career saves.

Maintainers are invited to review the instructions and image attribution before considering a link on their websites. The current publication is a community contribution, not their approval.

## Attribution

SmokePatch tutorial pictures come from its older FL23 installation article; captions identify that difference. FL26 lobby screenshots came from the Linux/Wine test. Arrows are illustrative annotations; they do not establish Windows compatibility. Third-party screenshots retain their owners' rights and are not relicensed here. No separate license has been selected for the original helper code yet.
