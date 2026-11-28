# /avro

The mrepo's register of the types and variants it uses: a cache, this machine's.

What a runtime checks by is here, in its own mrepo. Non-atomic, on
disk, never replicated: what it holds comes from the runtime package and
from the schema registry, so it is rebuilt, not copied. Three base
folders (the human, 2026-11-27: "I propose three base folders: registry,
types, variants"):

| folder | |
|---|---|
| `types/` | the types the mrepo holds, a file a type at its URI: `types/<org>/<package>/<name>.avsc` |
| `registry/` | the link to the schema registry, what a type not held is asked through; not there yet |
| `variants/` | a variant where it is in use, by `<layer>/<folders>`; not there yet |

## Its types

- **The three essential types**, what a runtime checks a record at its
  inbox by: `types/haiccing/base-package-runtime/record.avsc`,
  `request.avsc`, `attachment.avsc`. The runtime package's own, files
  in its `mrepo/avro/types/`, laid in as the mrepo is deployed: there
  before its runtime's first record. The one exception (the human: "The
  runtime three is an exception for bootstrapping a deployment into
  action"): no other package's types are laid in at deploy.
- **Dynamic** (the human: "that layer has to be dynamic"): any other
  type is asked of the schema registry, the authoritative point for
  schemas, and kept here once given. Not built yet: a type not held is
  refused, said.

## Design

- **Local**: `mycelium-git` keeps the layer on this machine's disk
  under every storage (`isLocal`).
- **No folder is empty**: `registry/` and `variants/` come with what
  fills them.
- **The mrepo's internal use** (the human, 2026-11-28: "the avro layer
  is for mrepo internal use. The cached data gets checkpointed, other
  data (like variants) is committed"): types cached from the registry
  checkpointed, variants committed. The rules for checkpointing and
  committing are a later piece of work, once the functionality runs.
- **The design**: `base-docs-vision`, "Type system" and "Solutions".
