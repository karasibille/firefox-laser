# Laser for Firefox

Simple Laser vaporwave theme for Firefox, inspired by the MiTo GMK Laser
keycap set. Published on
[addons.mozilla.org](https://addons.mozilla.org/firefox/addon/laser/).

The same palette is used for the desktop in
[dotfiles](https://github.com/karasibille/dotfiles) (`config/xrdb/colors/laser`).

## Colors

| Firefox key                                       | Color     | Laser name          |
|---------------------------------------------------|-----------|---------------------|
| `frame`, `popup`                                  | `#1f1658` | Midnight Blue Dark  |
| `toolbar`                                         | `#2d227d` | Midnight Blue       |
| `toolbar_field`                                   | `#444b9b` | Midnight Blue Light |
| `toolbar_text`, `toolbar_field_text`, `popup_text`| `#eceeee` | Light Steel Blue    |
| `tab_background_text`, `toolbar_field_highlight`  | `#c551a3` | Dawn                |
| `tab_line`, `tab_loading`                         | `#6056de` | Dusk                |
| `toolbar_bottom_separator`, `toolbar_vertical_separator` | `#b82857` | Old Rose     |

## Try it

In Firefox, open `about:debugging#/runtime/this-firefox`, then
**Load Temporary Add-on…** and pick `manifest.json`. The theme stays until
Firefox restarts.

## Build

```sh
npx web-ext lint     # the checks addons.mozilla.org runs on upload
npx web-ext build    # web-ext-artifacts/laser-<version>.zip
```

`web-ext-config.mjs` keeps the README and the license out of the package.
The CI runs both on every push and keeps the package as the `laser-xpi`
artifact of the run.

## Release

Raise `version` in `manifest.json`, commit, then push a tag with that
version:

```sh
git tag v1.1 && git push origin v1.1
```

The release workflow checks that the tag matches the manifest, lints and
builds the theme, submits it to addons.mozilla.org as a new listed version
(AMO reviews it, the workflow does not wait), and creates a GitHub release
with `laser-<version>.xpi`. It needs an AMO API key
([addons.mozilla.org/developers/addon/api/key](https://addons.mozilla.org/developers/addon/api/key/))
in the repository secrets `AMO_JWT_ISSUER` and `AMO_JWT_SECRET`.

The add-on ID in `browser_specific_settings` must stay the same, or AMO
treats the upload as another add-on.

## License

[CC BY 3.0](LICENSE), as on addons.mozilla.org.
