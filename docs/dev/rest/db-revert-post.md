# rest/db-revert-post.md

::: {.versionadded} 0.14.50 :::

Request revert of a receive only folder. Reverting a folder means to undo all local changes. This API call does nothing if the folder is not a receive only folder.

Takes the mandatory parameter \[folder\]{.title-ref} \(folder ID\).

\`\`\` {.sourceCode .bash} curl -X POST -H X-API-Key:... [http://127.0.0.1:8384/rest/db/revert?folder=default](http://127.0.0.1:8384/rest/db/revert?folder=default)

\`\`\`

