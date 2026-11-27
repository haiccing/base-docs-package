# attachment

An action attaching data to its answer, and reading what another attached.

Data that is an answer's product is attached, not said: a wrapper, the
attachment, carrying its content as bytes by the type it names
(`base-docs-avro`, "The cascade"; `base-docs-vision`, "Type system").
An action never sees bytes: it hands over a value and is given a value;
the conversion is the platform's, under the hood.

## Steps

**In development**: these steps act on the packages where they are built, not inside an install: an `sh` procedure, no `steps.haicc`; their check is the pre-release.

```sh
# the value's type: one the mrepo holds (its avro layer), or one of AVRO's own by its URI (avro/string, avro/long, ...)
ls haiccing/<pkg>/types
# the action returns what it says and what it attaches: a name, a type by URI, the value
$EDITOR pear-full-square/<module>/external/<action>/index.js   # return { message, attachments: [{ name, type: 'avro/string', value }] }
# what is attached is not also said: the message says what it is, not the data again
# an action that ran a command reads what was attached as a value
$EDITOR pear-full-square/<module>/external/<other>/index.js    # const { attachments } = await exec.run([...]); attachments[0].value
# data that has an address its reader can use is pointed to, not carried: { name, type, at }
# its README: what it attaches, under Returns
$EDITOR pear-full-square/<module>/external/<action>/README.md
# the check: its module's tests, its package's pre-release
tools/bare tools/package-test.js haiccing/<pkg>
```

## Notes

- **The proof of concept**: a value to bytes by a type and back,
  `mycelium-value`'s `avro(type)` (its test); bytes as base64 text in
  JSON and in memory, `mycelium-avro`'s `base64`.
- **Small content**: an attachment's content is in the request's record
  wherever it is kept and at every hop; a large one is pointed to.
- **A value that does not fit its type**, or a type the mrepo does not
  hold, fails the request, nothing of it kept.
- **A type the reader does not hold**: the attachment's name and type
  are there, it is passed on untouched; its value is refused, said.
- **Where it is done**: `mrepo-base-request`, `lib/attachment.js`
  (`wrapped`, `opened`), used by the execution; the actions that
  attach a value: `avro-registry/get`, its schema a text; `info/get`,
  its page.
- **Shown by the `haicc` command**: `Attached: <name> (<type>)`, content
  of one of AVRO's own types below it, readable; any other its size.
