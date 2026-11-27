# types

A package's core types: AVRO, a file each in types/, named by its URI, checked in a test of the package's own.

Pattern: types

A core type is a data structure a package owns the contract of: what
its actions take and answer, what it keeps. The package declares it
once, in `types/<name>.avsc`, its base schema; the same structure in
AVRO, in JS and in JSON, every field of a concrete type. A type is a
package's, never a module's (`base-docs-avro`, "Core types"). What is
structured and what is said: `base-docs-avro`, "Structure or language".

## Steps

**In development**: these steps act on the packages where they are built, not inside an install: an `sh` procedure, no `steps.haicc`; their check is the pre-release.

```sh
# the type: its AVRO name the fullname of <org>/<package>/<name>, a doc on it and on every field
cat > haiccing/<pkg>/types/<name>.avsc <<'END'
{ "type": "record", "name": "haiccing.<pkgCamel>.<nameCamel>", "doc": "...", "fields": [ { "name": "...", "type": "...", "doc": "..." } ] }
END
# its README: types/, each type with what it is
$EDITOR haiccing/<pkg>/types/README.md
# the engine carried, for its check: package.json, modules: pear-full-square/mycelium-avro
$EDITOR haiccing/<pkg>/package.json
# its check, a test of the package's own: valid, named, documented; examples valid as it, strictly, the same after AVRO and back
$EDITOR haiccing/<pkg>/test/types/types.test.js
# in its sets: full, validate and validate-in-situ
$EDITOR haiccing/<pkg>/test/full.json haiccing/<pkg>/test/validate.json haiccing/<pkg>/test/validate-in-situ.json
# the check: its pre-release
tools/bare tools/package-test.js haiccing/<pkg>
```

## Notes

- **The example**: `haiccing/base-package-runtime`, its `types/` (the
  record, the request, the attachment) and its `test/types`.
- **For every field, what acts on it exactly**; where nothing does, it
  is said, in natural language, not a field.
- **No any**: a carrier's base holds no value; with its value it is a
  variant of the base, its value its own type's.
- **Strict**: a value with a field its type does not name is not valid.
- **A module's code is checked against the type here**, in the package
  that declares it, not in the module's own tests.
- **In the running mrepo too**: the test in `validate-in-situ`, run with
  `runtime/run` where the package is deployed.
- **Loaded by the schema registry**: `avro-registry/load` checks a
  placed package's `types/*.avsc` as contracts and commits them into
  its `main`; a type that is no contract fails the load.
