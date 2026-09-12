# Hugo on One9x Pages

A minimal Hugo site, wired to deploy to [One9x Pages](https://one9x.com) on every
push. **Use this template** to start from it, or read it as a reference for a
site you already have.

```sh
hugo --minify
one9x pages release ./public --site mysite --deploy --error 404:/404.html
```

No `--spa`: Hugo writes a real HTML file per page, so an unmatched path genuinely
is a 404 and says so.

**No theme and no submodule.** The layouts here are four small files, on purpose
— a template whose first clone is broken because someone forgot `--recursive` is
a bad first impression. Add a theme when you want one; the deploy does not
change.

## Turn on the deploy workflow

`.github/workflows/deploy.yml` is already here. It needs two settings, both under
**Settings → Secrets and variables → Actions**:

| | Name | Value |
| --- | --- | --- |
| Variable | `ONE9X_SITE` | the site to deploy to |
| Secret | `ONE9X_TOKEN` | `one9x tokens create "github actions"` |

Create the site first:

```sh
one9x pages create mysite
```

Until `ONE9X_SITE` exists the job is **skipped**, not failed.

## Local development

```sh
hugo server
```

## Set `baseURL`

`hugo.toml` has a placeholder. Hugo bakes `baseURL` into canonical tags, feeds
and sitemaps — set it to the host you actually serve from.

## Drafts and future posts

`hugo` excludes drafts and future-dated content by default. In CI that matters
more than locally: a post dated tomorrow in your timezone silently does not
publish. `hugo --buildFuture` includes them.

## Docs

- [Hugo on One9x Pages](https://one9x.com/docs/frameworks/hugo)
- [All frameworks](https://one9x.com/docs/frameworks)
- [GitHub Actions](https://one9x.com/docs/github-actions)

## License

MIT
