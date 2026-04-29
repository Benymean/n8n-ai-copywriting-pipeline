# Architecture

This workflow is built as a staged content operations pipeline.

## Pipeline Overview

1. Gmail trigger collects labelled brief emails with DOCX attachments.
2. Attachment splitter filters DOCX files and creates traceable brief IDs.
3. DOCX converter turns each document into plain text.
4. Parser extracts structured JSON from the brief.
5. Normaliser cleans the parser output and fills safe defaults.
6. Task splitter expands multi-task briefs into separate writing jobs.
7. Keyword planner selects the right number of keywords for each task.
8. Writer generates one draft per task.
9. Validator checks SEO, structure, keyword, and formatting rules.
10. Final payload builder groups the work back into a reviewable markdown output.

## Design Choice

The main design choice was to avoid one giant AI prompt. Each stage has one responsibility. That makes the workflow easier to debug, easier to improve, and safer to run on inconsistent briefs.

## Main Data Objects

### Brief

A brief represents one uploaded DOCX attachment.

Typical fields:

- brief_id
- original_attachment_filename
- company_name
- contact_phone
- target_geo
- target_audience
- general_notes
- writing_style
- content_type
- master_keyword_list
- tasks

### Task

A task represents one piece of copy inside a brief.

Typical fields:

- task_id
- task_number
- task_title
- required_word_count
- outline
- keywords
- selected_keywords

### Draft

A draft represents generated output for one task.

Typical fields:

- final_draft
- writer_model
- writer_runtime_seconds
- writer_input_tokens
- writer_output_tokens
- writer_reasoning_tokens
- writer_total_tokens

### Validation Report

A validation report captures whether the draft passed the rules.

Typical fields:

- validator_pass
- validator_failures
- validator_report
- validator_keyword_counts
- validator_meta_title_char_count
- validator_meta_description_char_count
- validator_content_word_count
