# Validation of the combined WWAN update

Validated on 2026-10-25 with the installed Omarchy 4.5 components, and shell components downloaded from the official omacom/omarchy v4.0.0 and v4.0.4 tags.

- `node test-model.js`: modem/profile state parsing, Wi-Fi owning the default route, PIN/FDN handling, generated connect/disconnect and radio commands, failure exit codes, and icon thresholds including 46% without alert glyphs.
- `node tests/test-locale.js`: locale normalization, LC_ALL > LC_MESSAGES > LANG > Qt precedence, regional codes, Chinese mapping, C/POSIX and invalid input.
- `python3 -m unittest discover -s tests -v`: all 13 catalogs have the same keys, nonempty values and matching placeholders; literal UI translation keys exist.
- `omarchy plugin validate .`: plugin manifest validation.
- `bash tests/run-qml.sh`: production panel and service with simulated mmcli/nmcli/ip only. Native live switching through all supported languages, regional and English fallbacks, RTL restoration, German number formatting, radio state, state/IPC identifier preservation and markup-shaped external text in plain-text sinks.
- The same QML test with `PLUGIN_TEST_SHELL` pointing at each official legacy shell: dynamic native-component failure correctly selects the environment-based translator. Number formatting and translated state/error rendering work without Commons.I18n or Commons.Translations.
- German and Arabic production-panel previews inspected visually with a simulated connected modem. RTL reverses controls, translated radio help wraps, and profile/provider strings remain literal.

To use old source on current Qt, `tests/prepare-legacy-fixture.py` copies the source and qualifies Commons.Color references to avoid a newer Qt Color type collision. It changes no installed files and does not replace the old component APIs.

These are component compatibility tests with the current Qt/Quickshell runtime, **not complete tests of old desktop/OS installations**, modem hardware, carrier authentication or real network switching. Language catalogs still benefit from native-speaker review.

The installed plugin and existing worktrees were left unchanged. The combined changes are developed in a separate worktree/branch; the radio work and existing localization implementation are preserved.
