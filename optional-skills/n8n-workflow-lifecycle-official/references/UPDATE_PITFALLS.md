# update_workflow pitfalls

## Multiline JSON breaks the tool call
- `update_workflow` takes expression strings such as `value: "=💡 Daily Quote:\n\n{{ $json.quote }}\n\n— {{ $json.author }}"`.
- Passing that inside `operations[].parameters` commonly fails before it reaches n8n, with a JSON parse error like `Expecting ',' delimiter` at the multiline expression boundary.
- Fix: use a single-line expression string, or build the multiline value inside the workflow with concatenation. Example safe form:
  - `value: "={{ \"💡 Daily Quote: \" + $json.quote + \" — \" + $json.author }}"`

## Workaround when you must preserve multiline display text
- If the displayed text needs line breaks, prefer formatting in the final consumer, or keep a short placeholder and append formatting in a downstream Set node instead of fighting `update_workflow` serialization.

## Reproduce recipe
1. Create workflow via MCP.
2. Call `get_workflow_details` and notice a mangled multiline expression in a Set node.
3. Call `update_workflow` with `type: updateNodeParameters`, `nodeName`, and `parameters` containing the same multiline expression.
4. Observe tool-call JSON parse failure at the newline boundary.
5. Replace multiline value with single-line concatenation and retry; update succeeds.
