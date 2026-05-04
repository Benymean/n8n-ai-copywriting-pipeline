# n8n AI Copywriting Pipeline

An n8n automation that turns copywriting briefs into structured, SEO-aware draft outputs.

This project was built to reduce the manual admin work involved in handling client content briefs. The workflow watches Gmail for labelled brief emails, extracts DOCX attachments, converts them to text, parses the brief into structured JSON, splits multi-task briefs into individual writing tasks, plans keyword usage, generates drafts with OpenAI, validates SEO rules, and prepares the final markdown output for Google Drive.

## Why I Built This

Copywriting work involves more than writing.

A typical brief can include company information, target locations, word counts, task titles, page outlines, keyword lists, phone numbers, CTA requirements, and formatting rules. Manually extracting that information, planning keyword placement, writing the draft, checking SEO requirements, and preparing the final file takes time.

This workflow automates the repetitive parts while keeping the writing process structured, traceable, and easier to review.

## What the Workflow Does

- Monitors Gmail for pending brief emails
- Downloads DOCX attachments
- Converts DOCX files into plain text
- Extracts structured brief data with OpenAI
- Supports multi-task briefs
- Normalises parsed output
- Splits briefs into individual writing tasks
- Selects keywords based on word count
- Generates draft copy using a dedicated writer node
- Validates SEO and formatting rules
- Tracks token usage and runtime data
- Combines task outputs into a final markdown payload
- Prepares the final draft file for Google Drive

## Workflow Architecture

The workflow is designed as a pipeline rather than one large AI prompt.

### 1. Gmail Intake

The workflow starts with a Gmail trigger that watches for emails matching a specific label and attachment filter.

### 2. Attachment Splitting

DOCX attachments are filtered, renamed safely, and assigned a unique brief ID so each file can be tracked through the workflow.

### 3. DOCX to Text Conversion

Each DOCX file is converted into plain text before being sent to the parser.

### 4. Brief Parser

The parser extracts structured JSON from the flattened brief. It captures fields such as:

- company name
- phone number
- target audience
- target geography
- content type
- general notes
- writing style
- master keyword list
- task title
- word count
- task keywords
- outline

The parser is instructed to extract only explicit information and avoid guessing.

### 5. Normalisation

The normaliser cleans the parser output, handles missing values, derives fallback keyword lists, and preserves metadata such as the original attachment filename and brief ID.

### 6. Task Expansion

Multi-page or multi-post briefs are split into individual task items. Each task receives its own task ID, word count, title, outline, selected keywords, and business context.

### 7. Keyword Planning

The keyword planner selects a target number of keywords based on the required word count. It prioritises task-level keywords first, then uses master keywords as fallback options.

### 8. Draft Generation

The copywriter node generates one complete draft per task. It follows house-style rules for tone, structure, Australian English, keyword placement, metadata, headings, CTAs, and banned AI-style phrasing.

### 9. Validation

The validator checks the generated draft against rules such as:

- Meta title length
- Meta description length
- H1 matching the meta title
- Required keyword counts
- Keyword placement rules
- Heading title case
- Intro requirements
- CTA requirements
- Phone number placement
- Word count
- Missing structure

The validator returns a pass or fail result, failure reasons, keyword counts, metadata counts, and a report for debugging.

### 10. Final Payload

The final payload builder groups task outputs back into their original brief, adds validator failures when present, combines the drafts into markdown, and prepares the output filename.

## Tech Stack

- n8n
- Gmail trigger
- DOCX converter node
- OpenAI nodes
- JavaScript code nodes
- Google Drive handoff
- Markdown output
- JSON parsing and validation

## Key Features

- Multi-attachment support
- Multi-task brief support
- Structured schema extraction
- Keyword deduplication
- Word-count-based keyword planning
- Dedicated writer and validator stages
- Token and runtime tracking
- SEO validation reports
- Google Drive-ready markdown output
- Debug-friendly task and brief IDs

## Lessons Learned

This project showed me that useful AI automation is less about one perfect prompt and more about system design.

The most important parts were:

- separating parsing, writing, validation, and packaging
- preserving task context across nodes
- handling inconsistent brief formats
- avoiding over-reliance on AI output
- building validation around the model
- making failures visible instead of silent

## Current Status

The workflow is functional but still being improved.

Planned improvements:

- Add a dedicated SEO patching node for failed validator checks
- Improve validator coverage
- Add better error routing

## Security Note

This repository does not include real client briefs, credentials, Gmail label IDs, API keys, private business data, or generated client work. Any sample data in this repo is anonymised.

## Disclaimer

This project is a personal automation and portfolio project. It is not a plug-and-play SaaS product. The workflow may require changes depending on Gmail labels, credential setup, OpenAI models, DOCX formatting, and Google Drive configuration.
