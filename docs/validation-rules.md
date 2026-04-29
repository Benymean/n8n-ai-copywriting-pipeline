# Validation Rules

The validator is designed to catch common issues before the draft reaches final review.

## Metadata Checks

- Meta title exists
- Meta title length is within the target range
- Meta description exists
- Meta description length is within the target range
- Meta title and H1 match
- Meta title does not include the company name
- H1 does not include the company name

## Keyword Checks

- The keywords used line matches selected keywords
- Each selected keyword appears the required number of times
- Meta title contains the expected number of selected keywords
- Meta description contains the expected number of selected keywords
- H1 contains the expected number of selected keywords
- Intro contains the expected number of selected keywords
- Section heading and body keyword limits are respected

## Structure Checks

- Keywords used line appears first
- Meta title appears
- Meta description appears
- H1 appears
- Intro appears
- CTA appears
- H2 headings use title case

## CTA Checks

- CTA body includes a contact-page style phrase
- Phone number appears in the CTA body when supplied
- Phone number does not appear in restricted sections

## Reporting

The validator returns:

- pass or fail status
- failure codes
- human-readable failure messages
- keyword count breakdown
- metadata character counts
- content word count
