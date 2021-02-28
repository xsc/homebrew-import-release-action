# homebrew-import-release-action

[![CI](https://github.com/xsc/homebrew-import-release-action/workflows/CI/badge.svg)](https://github.com/xsc/homebrew-import-release-action/actions?query=workflow%3ACI)
[![Release](https://img.shields.io/github/v/release/xsc/homebrew-import-release-action?include_prereleases&sort=semver)](https://github.com/xsc/homebrew-import-release-action/releases/latest)

This is a [Github Action][gha] to populate a [Homebrew tap][tap] with formulas
based on Github releases and their assets.

## Usage

```yaml
- uses: xsc/homebrew-import-release-action@v1
  with:
    target: into-docker.rb
    repository: into-docker/into-docker
```

## Prerequisites

- Existing Github release with corresponding tag (e.g. `v1.0.0`).
- An asset attached to the release that matches a defined selector (see below).
- A file `.homebrew.rb` in the repository that can utilise the following
  variables for substitution:
  - `HOMEBREW_VERSION`: version of the formula.
  - `HOMEBREW_ASSET_URL`: URL to the matched release asset.
  - `HOMEBREW_SHA256`: SHA-256 hash of the matched release asset.
  - `HOMEBREW_ASSET_URL_ALT`: URL to the alternative release asset (e.g. Linux version).
  - `HOMEBREW_SHA256_ALT`: SHA-256 hash of the alternative release asset (e.g. Linux version).

## Inputs

| Name            | Required | Description                                                                        |
| :-------------- | :------: | :--------------------------------------------------------------------------------- |
| `target`        |   Yes    | Path to the output file.                                                           |
| `repository`    |   Yes    | Repository to query for releases and the formula template.                         |
| `selector`      |   Yes    | Substring that is contained within the main asset's filename.                      |
| `alt-selector`  |    No    | Substring that is contained within the alternative asset's filename.               |
| `template-path` |    No    | Path inside `repository` to use as the formula template (no leading `./`).         |
| `template-ref`  |    No    | Ref (branch/tag/commit) to use for the template lookup.                            |
| `tag`           |    No    | Specific release tag to use for creating the formula (defaults to latest release). |
| `version`       |    No    | Override the formula version (defaults to using the tag minus a `v` prefix)        |

## Outputs

None.

## Development

We use [prettier][] to ensure consistent formatting of Markdown and YAML files.
Please run `yarn` or `npm install` to register the pre-commit hook.

[gha]: https://help.github.com/en/actions
[tap]: https://docs.brew.sh/Taps
[prettier]: https://prettier.io/

## License

```
MIT License

Copyright (c) 2020 Yannick Scherer

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```