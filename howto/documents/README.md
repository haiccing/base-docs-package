# documents

An mrepo that documents every package in the install's store, beyond the packages it is made of.

Pattern: documents

A list (`mrepo/packages/.layer.json`) with `"documents": "store"`: its
info extraction reads, besides its own packages, every package in the
install's store, `<work>/packages/`, through its packages manifest's
mapping, read only. Nothing of them is placed in the mrepo or runs.
Their pages are split on package, each below its organisation, in its
own context. What is installed is what is documented: the docs mrepo,
the install's manual.

## Making it

In development, where the packages are built (`howto/`, "Written where"):

```sh
# the list: what the mrepo is made of, and what it documents beyond it
$EDITOR haiccing/<pkg>/mrepo/packages/.layer.json   # "documents": "store"
# its hooks: the build at initialise, removed at shutdown
$EDITOR haiccing/<pkg>/mrepo/runtime/hooks/initialise.haicc   # info/extract
$EDITOR haiccing/<pkg>/mrepo/runtime/hooks/shutdown.haicc     # info/clear
# its README: what it documents, beside its included packages
$EDITOR haiccing/<pkg>/README.md
```

## Steps

The script, [steps.haicc](steps.haicc): each line as typed after `haicc`, what it answers under it; run with `howto/run`, shown here at info extraction.

## Notes

- **Only `store`**: a list documents nothing else.
- **`initialise` again** adds what is new in the store; **`shutdown`**
  removes the build, `initialise` builds it again.
- **Nothing of a documented package runs**: it is not in the mrepo.
