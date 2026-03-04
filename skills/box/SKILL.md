---
name: box
description: >
  Work with Box content via the Box MCP server. Use when the user needs to
  search, read, upload, or organize files in Box, run Box AI queries, or
  extract structured metadata. This skill covers best-practice workflow
  patterns — it does not replicate tool documentation.
---

# Box MCP Skill

The Box MCP server exposes tools for content management, search, AI, hubs,
collaboration, and document generation. The MCP schema already describes each
tool's parameters, so this skill focuses on **how** to use them well.

> **Mandatory guardrails live in `.cursor/rules/box.mdc`.** That file covers
> confirmation gates for destructive actions, hub modifications, file comments,
> Doc Gen output locations, externally shared folders, content display
> preferences, and Box AI governance. This skill does not duplicate those
> rules — read and follow them in every session.

## Search

- When the user refers to a folder by name, use `search_folders_by_name` first
  to resolve the folder ID, then scope subsequent file searches to that folder.
- Prefer `search_files_metadata` over keyword search when the user's query
  maps to known metadata fields or templates — it returns more precise results.

## File writes

- When uploading new files with `upload_file`, prefer writing to a dedicated
  output folder rather than the root or the same folder as source files. Ask
  the user where to place output if it isn't obvious.

## Metadata and structured extraction

- Prefer `ai_extract_structured` over `ai_extract_freeform` when a metadata
  template exists. Check for available templates first (e.g., via context or
  prior results) and infer the best match. Only ask the user if no template
  can be determined. Always tell the user which template was selected.
- When extracting from multiple files, process them in batches and summarize
  results clearly — don't dump raw JSON unless asked.
- Use `ai_extract_structured_from_fields_enhanced` when the user needs custom
  field definitions without a pre-existing template.

## Box AI

- Use `get_file_content` to retrieve file content.
- Use `ai_qa_single_file` for questions about one document, `ai_qa_multi_file`
  for cross-file analysis, and `ai_qa_hub` when the user has an existing hub.
- Box AI responses include citations — surface them when possible so the user
  can verify answers.

## General guidelines

- Call `who_am_i` at the start of a session if you need to verify permissions
  or identify the authenticated user.
- When listing folder contents, paginate if needed and summarize large
  directories rather than printing every item.
- Prefer reading file details with `get_file_details` before operating on a
  file — it confirms the file exists and shows current state.
- For exploratory or demo usage, prefer working within a dedicated folder
  rather than operating across the user's entire Box account.
- Avoid granting or assuming broad enterprise-wide access. Default to
  least-privilege — only access the folders and files the task requires.
