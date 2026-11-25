# mrepo-definition

A package that defines an mrepo: its list, the packages that mrepo is made of.

Pattern: mrepo-definition

A package with `mrepo/packages/.layer.json` defines an mrepo when it is
the one deployed: its list, in deploy order, ends with itself, and the
runtime config (the hooks, the service state) is laid in from it, the
last of the list, only. A component does so; a protocol package can, to
be deployed on its own.

## Making it

In development, where the packages are built (`howto/`, "Written where"):

```sh
# the list: the packages in deploy order, itself last
$EDITOR haiccing/<pkg>/mrepo/packages/.layer.json
# its README: ## Included packages, the list but itself, siblings
$EDITOR haiccing/<pkg>/README.md
# the check: its info test, the included packages against the list
tools/bare haiccing/<pkg>/main.js /test/info
```

## Steps

The script, [steps.haicc](steps.haicc): each line as typed after `haicc`, what it answers under it; run with `howto/run`, shown here at info extraction.

## Notes

- **Each package of the list** brings its part of the structure, read
  from its bundle, in order: a later file replaces an earlier one.
