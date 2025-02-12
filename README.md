# Setup Fontist

🔠 Install [Fontist](https://www.fontist.org/) for GitHub Actions

<table align=center><td>

```yml
- uses: fontist/setup-fontist@v1
- run: fontist install "Fira Code"
```

</table>

💎 Uses Ruby to install the fontist Ruby gem \
🟦 Works with Windows \
🐧 Works with Ubuntu \
🍎 Works with macOS \
⚡ Caches installation in `$RUNNER_TOOL_CACHE` and/ior the workflow cache \
📐 Caches `~/.fontist` font installs by default using `manifest.yml`

## Usage

![GitHub Actions](https://img.shields.io/static/v1?style=for-the-badge&message=GitHub+Actions&color=2088FF&logo=GitHub+Actions&logoColor=FFFFFF&label=)
![GitHub](https://img.shields.io/static/v1?style=for-the-badge&message=GitHub&color=181717&logo=GitHub&logoColor=FFFFFF&label=)

**🚀 Here's what you're after:**

```yml
on: push
jobs:
  job:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: fontist/setup-fontist@v1
      - run: fontist install "Fira Code"
```

💡 You can use `fontist manifest-install manifest.yml` to install fonts listed in a manifest file similar to `package.json`, `requirements.txt`, and `Cargo.toml`.

### Inputs

- **`fontist-version`:** The version of Fontist to install. This can be an exact version lile `1.10.0` or a semver range such as `1.x` or `~1.15.0`. The default value is `latest`.

- **`fontist-token`:** The GitHub token to use when fetching the version list from fontist/fontist. You shouldn't have to touch this. The default is the `github.token` if you're on github.com or unauthenticated (rate limited) if you're not on github.com.

- **`cache`:** Whether or not to use [@actions/cache](https://www.npmjs.com/package/@actions/cache) to cache things in the GitHub workflow cache. This is enabled by default.

- **`cache-dependency-path`:** A multiline list of globs to use to derive the `~/.fontist` cache key. The default is `manifest.yml` and `manifest.yaml`. If no files are matched at runtime then the `~/.fontist` folder will not be cached.

### Outputs

- **`fontist-version`:** The version of Fontist that was installed. This will be something like `1.10.0` or similar.

- **`cache-hit`:** Whether or not Fontist was restored from the runner's cache or newly downloaded.

## Development

![Bun](https://img.shields.io/static/v1?style=for-the-badge&message=Bun&color=000000&logo=Bun&logoColor=FFFFFF&label=)
![Node.js](https://img.shields.io/static/v1?style=for-the-badge&message=Node.js&color=339933&logo=Node.js&logoColor=FFFFFF&label=)
![Ruby](https://img.shields.io/static/v1?style=for-the-badge&message=Ruby&color=CC342D&logo=Ruby&logoColor=FFFFFF&label=)

This action tries to restore the result of `gem install fontist` from both the `$RUNNER_TOOL_CACHE` as well as the workflow cache via [@actions/cache](https://www.npmjs.com/package/@actions/cache). It then tries to restore the `~/.fontist` folder local cache from the workflow cache.

**How do I test it?** \
Open a PR (even a draft one works) and some magic GitHub Actions will run to test your changes.

Note that since [Bun doesn't support Windows yet](https://github.com/oven-sh/bun/issues/43) we can't run the `bun build` command on Windows runners. Don't worry! The action should still work ok since Bun is only used for the build step; it runs using `node <the-js-file>` via `using: node20` in both testing and releases. Once Bun adds Windows support remember to add back the Windows tests. 😉

## Contributions

This GitHub Action was originally created by @jcbhmr for the
[Typst project](https://github.com/typst-community/typst.js)
and contributed to [Fontist](https://www.fontist.org).

Huge thanks to @jcbhmr for the tremendous effort in improving the Fontist
ecosystem!
