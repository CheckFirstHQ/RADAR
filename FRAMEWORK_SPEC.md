# RADAR Framework Specification

Version 1.7 | Last Updated: June 2025

## Overview

The RADAR (Regulatory Assessment for Digital Service Act Risks) framework is a structured taxonomy for categorising and identifying Digital Service Act (DSA) compliance issues. This document defines the technical specification of the framework's data structure and formatting requirements.

## Framework Structure

### 1. Core Components

The RADAR framework consists of three hierarchical levels:

```
Framework
├── Categories
│   ├── Infringements
│   │   └── Observables
```

### 2. Category Structure

Each category represents a major area of DSA compliance concern.

#### Category Object Schema
```json
{
  "id": "string",           // Unique 2-3 letter code (e.g., "cr", "dp")
  "name": "string",         // Human-readable category name
  "description": "string",  // Detailed description of the category
  "infringements": []       // Array of infringement objects
}
```

#### Category Codes
| Code | Category Name |
|------|--------------|
| `cr` | Content-Related Infringements |
| `tr` | Transparency and Reporting Infringements |
| `cp` | Consumer Protection and Market Fairness |
| `pa` | Platform Accountability and Cooperation |
| `pad` | Political Advertising Infringements |
| `ei` | Election Integrity Infringements |
| `ch` | Child Protection and Safety Online |
| `icg` | Illegal Content and Goods |
| `cv` | Cyber Violence |
| `dmm` | Disinformation and Manipulated Media |
| `dp` | Dark Patterns and Manipulative Design |
| `tap` | Targeted Advertisements & Profiling |
| `das` | Data Access and Scrutiny |
| `com` | Compliance Function |

### 3. Infringement Structure

Each infringement represents a specific type of DSA violation.

#### Infringement Object Schema
```json
{
  "id": "string",           // Format: category_number (e.g., "cr_01")
  "name": "string",         // Concise infringement title
  "description": "string",  // Detailed explanation (nullable)
  "dsaArticles": [],       // Array of DSA article numbers as strings
  "observables": []        // Array of observable behaviour strings
}
```

#### Infringement ID Format
- Pattern: `[category]_[number]`
- Category: 2-3 lowercase letters
- Number: 2-digit zero-padded integer
- Examples: `cr_01`, `dp_03`, `tap_02`

### 4. Observable Structure

Observables are specific, measurable behaviours that indicate an infringement.

#### Observable Requirements
- Must be specific and measurable
- Should describe what can be directly observed
- Written in clear, non-technical language
- Actionable for assessment purposes

#### Observable Examples
```json
"observables": [
  "Large backlog of unaddressed user reports over a prolonged period",
  "Evidence of repeated non-compliance with legal takedown requests",
  "Lack of documentation on notice-and-action procedures"
]
```

## Data Format Specifications

### 1. JSON Structure

The framework is distributed in JSON format with the following root structure:

```json
{
  "metadata": {
	"lastUpdated": "ISO 8601 datetime",
	"source": {
	  "filename": "string",
	  "conversionTool": "string",
	  "conversionDate": "ISO 8601 datetime"
	},
	"version": "string",
	"description": "string",
	"authors": [{
	  "name": "string",
	  "affiliation": "string"
	}],
	"license": "CC-BY-SA-4.0",
	"schemaVersion": "1.0",
	"organization": "CheckFirst",
	"organizationSector": "company"
  },
  "framework": "RADAR - Regulatory Assessment for Digital Service Act Risks Framework",
  "categories": []
}
```

### 2. Version Management

#### Version File Structure
```
framework/
├── versions.json    # Version registry
├── 1.6.json        # Version 1.6 data
├── 1.7.json        # Version 1.7 data (current)
└── 1.8.json        # Version 1.8 data (development)
└── ... 
```

#### versions.json Schema
```json
{
  "versions": [{
	"version": "string",      // Semantic version (e.g., "1.7")
	"label": "string",        // Status label (e.g., "Latest", "Development")
	"default": boolean,       // Is this the default version?
	"date": "YYYY-MM-DD",    // Release date
	"description": "string",  // Version description
	"authors": []            // Array of author names
  }]
}
```

### 3. DSA Article References

DSA articles are stored as strings to maintain flexibility:
- Format: Numeric strings (e.g., "14", "25")
- Can include sub-articles if needed (e.g., "14.1")
- Sorted numerically when displayed

## Validation Rules

### 1. Required Fields

#### Category Level
- `id`: Must be unique, 2-3 lowercase letters
- `name`: Non-empty string
- `description`: Non-empty string
- `infringements`: Array (can be empty)

#### Infringement Level
- `id`: Must match pattern `[category]_[0-9]{2}`
- `name`: Non-empty string
- `dsaArticles`: Array of strings (can be empty)
- `observables`: Array of strings (recommended non-empty)

### 2. Consistency Rules
- Infringement IDs must be unique across the entire framework
- Category codes in infringement IDs must match parent category
- Version numbers must follow semantic versioning

### 3. Content Guidelines
- Names should be concise (< 100 characters)
- Descriptions should be comprehensive but clear
- Observables should be specific and measurable
- At least one observable per infringement (recommended)

## Web Metadata Schema

For web implementations, RADAR supports embedded metadata:

### Meta Tag Format
```html
<meta name="radar-assessment" content='{"version":"1.7","platform":"Platform Name","date":"YYYY-MM-DD","categories":{"cr":["cr_01","cr_02"]}}'>
```

### JSON-LD Format
```json
{
  "@context": "https://radar.checkfirst.network/schema.json",
  "@type": "DSAAssessment",
  "version": "string",
  "platform": "string",
  "assessmentDate": "YYYY-MM-DD",
  "infringements": {
	"category": ["infringement_ids"]
  },
  "totalInfringements": number,
  "report": "URL (optional)"
}
```

## Change Management

### 1. Version Increments
- **Major version** (X.0): Structural changes, breaking compatibility
- **Minor version** (X.Y): New infringements or categories
- **Patch version** (X.Y.Z): Corrections, clarifications (if used)

### 2. Deprecation Policy
- Infringement IDs are never reused
- Deprecated infringements marked with status field
- Minimum 6-month deprecation notice for structural changes

### 3. Change log Requirements
Each version must document:
- Added infringements
- Modified infringements
- Removed infringements
- Structural changes
- DSA article updates

## Implementation Notes

### 1. Performance Considerations
- Full framework JSON ~200-300KB
- Support partial loading by category
- Enable caching with version-based ETags

### 2. Internationalisation
- Framework distributed in English
- Translations maintained separately
- IDs remain constant across languages

### 3. Extension Points
- Custom observables can be added locally
- Additional metadata fields allowed
- Backward compatibility required

## Compliance

This specification adheres to:
- JSON Schema Draft 07
- ISO 8601 date formats
- Semantic Versioning 2.0.0
- CC BY-SA 4.0 licensing requirements