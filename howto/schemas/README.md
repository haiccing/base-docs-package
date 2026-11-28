# schemas

The first build's schemas: AVRO, a file each in schemas/, retiring as packages are brought to types/.

Pattern: schemas

The first build's form: a schema a file, `schemas/<name>.json`, its
AVRO name the fullname of its URI, a module's in its own `schemas/`.
Nothing registers or lists them any more: registration at deploy was
removed with the request's new structure, and the info layer's
`schemas` page is retired. Still carried by the packages not yet
brought over. A package brought to schemas declares `types/` instead
(the how-to `types`), its types gathered by the schema registry.

## Steps

**In development**: these steps act on the packages where they are built, not inside an install: an `sh` procedure, no `steps.haicc`; their check is the pre-release.

```sh
# a package still in the first form: its schemas, a file each
ls haiccing/<pkg>/schemas
# brought over: its types declared instead (the how-to types), schemas/ removed
$EDITOR haiccing/<pkg>/types/<name>.avsc
tools/bare tools/package-test.js haiccing/<pkg>
```

## Notes

- **Where nothing is typed yet**, the first build's `json` type
  (`pear-full-square/mycelium-value-avro/json`) carries the value; not
  used by what is brought to the request.
