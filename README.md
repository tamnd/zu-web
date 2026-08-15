# zudb.dev

The documentation site for [zu](https://github.com/tamnd/zu), an embedded property-graph database.

Astro and Starlight, statically built, no runtime framework on a reference page. Search is Pagefind, built at build time, so it works offline and on a fork's preview with no service and no API key. Diagrams are Mermaid rendered to inline SVG. Code is highlighted by Shiki with the same GQL grammar the VS Code extension ships, so a query looks identical in your editor and on the page.

```
npm install
npm run dev
```

## Two thirds of this site is generated

The reference sections are not written here. They are rendered from artifacts the engine build publishes: the API model per language, the GQL grammar and function registry, the error catalog, the CLI command tree, and the conformance scoreboard. `cargo xtask docs fetch --version 0.5.0` pulls a release's artifacts, `--version main` pulls the nightly ones, which is what a docs PR against unreleased behaviour uses. Nothing generated is committed.

That split is also the answer to the obvious objection about a separate docs repository. What kills docs-as-code is documentation that is not generated from the source of truth and drifts silently, not documentation that lives at a different path. So the gates move with the content: a pull request in `tamnd/zu` that removes a documented public symbol fails there, against that pull request's own API model, not here and not later.

## Code samples are files, not fenced blocks

Every example in `snippets/` is a real source file in a real project in its own language. It compiles, it runs, it is formatted by that language's formatter and linted by that language's linter, and its output is a checked-in golden. A page pulls one in with `<Snippet file="python/bulk-load-parquet.py" region="load" />`. Fenced blocks are allowed for shell transcripts and output, and that is all.

The snippet jobs run against published artifacts, not a workspace build, which is the difference between "the example works on the maintainer's machine" and "the example works after `pip install zudb`".

## Editing

Hand-written guides live in `src/content/docs/`. If a page has a `generated_from` field in its frontmatter, do not edit it here; fix the doc comment or the registry entry in [tamnd/zu](https://github.com/tamnd/zu) and it will regenerate. Every page carries an "Edit this page" link that resolves to whichever of the two repositories actually owns it.

`style/zu/terms.yml` is the terminology table, and it is not only this site's. The guides here, the doc comments in `tamnd/zu` that become reference pages, the CLI's help and the text of an error all answer to it, so that a node is never a vertex on one page and a node on the next. `style/README.md` has the schema and the rule for adding a term.

## Where things live

| What | Where |
|---|---|
| Engine, Rust SDK, CLI, `zu.h`, conformance corpus, doc comments | [tamnd/zu](https://github.com/tamnd/zu) |
| Clients | `zu-python`, `zu-node`, `zu-go`, `zu-java`, `zu-c`, `zu-dotnet`, `zu-kit` |
| This site | here |

## Status

Pre-1.0 and pre-release. Nothing is deployed yet.

## Specification

Spec/2064g/docs/ in [tamnd/zu](https://github.com/tamnd/zu), particularly `02-platform-and-toolchain.md` and `05-executable-documentation.md`. Milestone: D0 (tamnd/zu#173).

## License

Apache-2.0, same as the engine.
