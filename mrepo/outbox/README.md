# /outbox

The records the mrepo sends: each a record around a request returned,
for where the request's `reply` says. Non-atomic; its one writer, the
runtime.

What a request attached goes with it as it is, the wrapper, its content
base64 text: whoever collects it carries it on untouched.

Each record is committed, then written into its folder, `<dir>/outbox/`,
made when the mrepo is built, so it can be watched from the start. A
parent follows its child's outbox folder directly; others subscribe, the
subscriber's runtime copying the new records into its own inbox.
