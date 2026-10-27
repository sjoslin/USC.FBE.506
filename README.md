# USC.FBE.506

Course site for FBE 506, Quantitative Methods in Finance: local setup and
working with coding agents.

Published at <https://sjoslin.github.io/USC.FBE.506/> by
`.github/workflows/pages.yml` on every push to `main`.

Jekyll 4.4 with the [Just the Docs](https://just-the-docs.com) theme, pinned
in `Gemfile`.

## Previewing locally

macOS ships Ruby 2.6, which is too old for Jekyll 4.4. Install a current one
and put it ahead of Apple's on your PATH:

```bash
brew install ruby
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zprofile
exec zsh -l
ruby -v            # expect 3.x, not 2.6
```

Then, from this directory, once:

```bash
gem install bundler
bundle install
```

and from then on:

```bash
bundle exec jekyll serve --livereload
```

Open <http://localhost:4000/USC.FBE.506/>. Note the path: `baseurl` in
`_config.yml` means the site is not served at the bare root.

Saving a `.md` file rebuilds and refreshes the browser. Editing `_config.yml`
does not; stop the server with `Ctrl+C` and start it again.

## Pages

| File | URL | Nav |
|---|---|---|
| `index.md` | `/` | Home |
| `overview.md` | `/install/` | 1, Overview |
| `overview_local_python.md` | `/install/python/` | 1.1 |
| `overview_vscode.md` | `/install/vscode/` | 1.2 |
| `overview_codex.md` | `/install/codex/` | 1.3 |
| `setup.md` | `/setup/` | 2, Setup |
| `setup_mac.md` | `/install/mac/` | 2.1 |
| `setup_pc.md` | `/install/windows/` | 2.2 |
| `setup_vscode_python.md` | `/install/vscode/python/` | 2.3 |
| `optional.md` | `/optional/` | 3, Optional Topics |
| `python-and-uv.md` | `/optional/environments/` | 3.1 |
| `containers.md` | `/optional/sandboxing/` | 3.2 |
| `support-applications.md` | `/optional/support-applications/` | 3.3 |

`overview_mac_draft.md` preserves the former Mac overview as an unpublished editing source. `setup_mac_old_link.md` keeps the old URL working with a link to Mac Setup.

Each page sets its own `permalink`, and internal links are written as
`{{ site.baseurl }}/install/mac/` rather than as relative `.md` paths, because
`jekyll-relative-links` is not among the plugins here.

Child pages carry a `parent:` naming their section, which has to match that
parent's `title:` exactly. Reword that title and the children drop
out of the nav with no build error.

## Styling

Theme overrides live in `_sass/custom/`, which just-the-docs imports
automatically:

- `setup.scss` for theme variables, currently just a wider left nav
- `custom.scss` for rule overrides

`assets/css/custom.css` is a leftover from the 633 repo and is **not loaded**.
`custom_css` is not a just-the-docs configuration key and there is no
`_includes/head_custom.html`, so nothing ever linked it. Safe to delete.

## Term records

The site is not forked per term. To mark what students were given in a
particular term, tag it:

```bash
git tag 26.03 && git push --tags
```
