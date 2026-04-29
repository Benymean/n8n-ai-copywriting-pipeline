# Setup

This repo is a portfolio version of the workflow. It does not include private credentials, real Gmail labels, real client briefs, or production execution data.

## Requirements

- n8n
- Gmail OAuth credential
- OpenAI credential
- DOCX to text conversion node
- Optional Google Drive credential for final file handoff

## Recommended Setup Steps

1. Create a Gmail label for pending briefs.
2. Create optional labels for processing, done, and error states.
3. Configure the Gmail trigger with your own search query.
4. Add your Gmail OAuth credential in n8n.
5. Add your OpenAI credential in n8n.
6. Add the DOCX converter community node if needed.
7. Import the sanitised workflow export.
8. Replace placeholder label names, folder IDs, model names, and credentials.
9. Test with an anonymised sample brief before using real work.

## Gmail Search Example

```text
label:YOUR_LABEL/Pending has:attachment -label:YOUR_LABEL/Done -label:YOUR_LABEL/Error
```

## Important

Do not commit your real n8n workflow export until it has been cleaned. n8n exports can contain credential references, webhook IDs, label IDs, account-specific filters, folder IDs, and private prompt text.
