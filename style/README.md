# The style directory

`zu/terms.yml` is the terminology table: the words zu uses, and the words it does not. It exists because nine repositories in seven languages write prose about one database, and a node that is a vertex on one page and a node on the next is two data models to a reader who does not already know it is one.

It is one file and it is shared. The guides on this site, the doc comments in `tamnd/zu` that become reference pages, the CLI's help text, and the text of an error all answer to it, which is the only arrangement under which "what do we call this" has one answer rather than nine.

## What it covers

Prose, and only prose. Identifiers answer to the language they are written in, so a Rust `Vertex` type would be a naming problem and not a terminology one, and quoted material answers to whoever said it, so a paper's abstract is left alone. A reader that fires on a code span teaches people to ignore it, which costs more than the drift it catches.

## The schema

```yaml
schema: 1
doc: The words zu uses, and the words it does not.

terms:
  - term: node
    group: graph model
    doc: An element of a graph, held by exactly one node table.
    instead:
      - vertex
      - vertices
```

| Key | Required | Meaning |
| --- | --- | --- |
| `schema` | yes | Moves when the shape of the file changes, not when the terms do. It is `1`. |
| `doc` | file and term | What the term means, in one sentence somebody wrote. On a term it is also the glossary entry this site renders. |
| `terms` | yes | The terms, in the order a glossary shows them. |
| `term` | yes | The word or phrase, spelled the way it should be written. |
| `group` | yes | The section of the glossary it belongs to. |
| `instead` | no | Forms that must give way to the term. A term with none is here for its definition, which is the case for the three words that are close enough to be confused and different enough to keep apart. |

`instead` matches whole words and ignores case, except where the form differs from the term only in case. That exception is what lets `zu` refuse `Zu` at the start of a sentence without also refusing every other capitalised word, and it is a rule rather than a flag because a flag on forty entries is thirty nine chances to set it wrong.

## Where the reader is

`cargo xtask terms` in [tamnd/zu](https://github.com/tamnd/zu). It is there rather than here because the two hardest consumers are there, the CLI's help and the errors, and because a table checked by nine repositories against nine readers would be nine tables. This site's own prose is checked by the same command once the site build runs it.

## Adding a term

A term earns its place by having been got wrong, or by being close enough to another term that somebody will. A table that lists every word in the documentation is a table nobody reads, and the entries that matter are the ones where two spellings are both plausible and only one is right.

Write the definition first. If it cannot be said in a sentence, the disagreement is about the thing and not about the word, and the table is the wrong place to settle it.
