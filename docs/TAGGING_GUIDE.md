# RADAR Tagging Guide

A practical guide for using RADAR tags in DSA compliance assessments and reports.

## Quick Start

RADAR tags are standardised identifiers for DSA infringements. Each tag follows the format `category_number` (e.g., `cr_01`, `dp_02`).

### Basic Process
1. **Observe** the platform behaviour
2. **Match** it to RADAR infringements
3. **Document** with RADAR tags
4. **Report** using standard format

## Understanding RADAR Tags

### Tag Structure

```
cr_01
│  │
│  └── Sequential number (01-99)
└───── Category code (2-3 letters)
```

### Category Quick Reference

| Tag Prefix | Category | Common Issues |
|------------|----------|---------------|
| `cr_` | Content-Related | Illegal content, moderation failures |
| `tr_` | Transparency | Missing reports, unclear policies |
| `cp_` | Consumer Protection | Trader violations, product safety |
| `pa_` | Platform Accountability | Non-cooperation, risk assessment |
| `ch_` | Child Protection | Minor safety, age verification |
| `icg_` | Illegal Content & Goods | CSAM, hate speech, counterfeit |
| `cv_` | Cyber Violence | Harassment, threats, doxxing |
| `dmm_` | Disinformation | False info, deepfakes, manipulation |
| `dp_` | Dark Patterns | Deceptive design, forced actions |
| `tap_` | Targeted Ads | Illegal targeting, transparency |
| `pad_` | Political Advertising | Unlabeled political ads |
| `ei_` | Election Integrity | Electoral disinformation |
| `das_` | Data Access | Research access restrictions |
| `com_` | Compliance Function | Missing compliance officer |

## How to Tag Infringements

### Step 1: Document What You Observe

Be specific about:
- **What** happened (the behavior)
- **Where** it occurred (platform feature)
- **When** you observed it (date/time)
- **How** it affects users
- **Evidence** collected (screenshots, videos)

### Step 2: Find Matching RADAR Tags

#### Method A: Browse by Category
1. Identify the general area (e.g., "This is about content moderation")
2. Go to that category (e.g., Content-Related)
3. Review infringements in that category
4. Check observables to confirm match

#### Method B: Search by Keyword
- Search for specific terms (e.g., "delete account")
- Review all matching infringements
- Check which category fits best

#### Method C: Search by DSA Article
- If you know the relevant DSA article
- Find all infringements linked to that article
- Match your observation to the descriptions

### Step 3: Verify the Match

Check the observables list. Your observation should match at least one observable behavior. For example:

**Infringement**: `dp_01` - Obstruction  
**Observables**:
- ✓ "Processes for account deletion requiring many more steps than sign-up"
- ✓ "Absence of clearly visible 'cancel' option"
- ✓ "Interfaces that loop when trying to opt out"

If your observation matches these patterns, use this tag.

### Step 4: Document Multiple Infringements

One behavior might violate multiple infringements:

**Example**: A platform showing political ads to minors without labels
- `tap_01` - Ads Targeting Minors
- `pad_01` - Failure to Label Political Advertisements
- `ch_01` - Failure to Implement Minor Protection

Tag all that apply.

## Tagging Best Practices

### ✅ DO
- **Tag comprehensively**: Include all relevant infringements
- **Be specific**: Document exactly what you observed
- **Provide evidence**: Reference screenshots, recordings, or documents
- **Note patterns**: If behavior is systematic, document frequency
- **Include context**: Platform version, date, user type affected
- **Use current version**: Always note which RADAR version you're using

### ❌ DON'T
- **Force fit**: Don't use tags that don't quite match
- **Over-generalize**: Avoid vague descriptions
- **Skip evidence**: Don't tag without supporting documentation
- **Modify IDs**: Keep tag IDs exactly as specified
- **Mix versions**: Use consistent RADAR version throughout report

## Report Formatting

### Standard Tagging Annex

Add this annex to your report:

```
---
ANNEX: RADAR Framework Tags
Digital Service Act Infringement Analysis

Platform: [Platform Name]
Assessment Date: [YYYY-MM-DD]
Assessment Period: [Start Date] to [End Date]
RADAR Version: [e.g., 1.7]

Identified Infringements:

Category: Content-Related Infringements
- cr_01: Failure to take action against Illegal Content
  * Observed: [Specific description of what you observed]
  * Frequency: [One-time, Occasional, Systematic]
  * Evidence: [Reference to report section/appendix]
  * Impact: [Number of users affected, severity]

- cr_02: Misapplication of Notice-and-Action Mechanisms
  * Observed: [Description]
  * Frequency: [Frequency]
  * Evidence: [Reference]
  * Impact: [Impact]

Category: Dark Patterns
- dp_01: Obstruction
  * Observed: [Description]
  * Frequency: [Frequency]
  * Evidence: [Reference]
  * Impact: [Impact]

Summary:
- Total Infringements: [Number]
- Categories Affected: [Number]
- DSA Articles Potentially Violated: [List, e.g., 14, 16, 25]
- Systemic Issues: [Yes/No, with brief explanation]

---
```

### Inline References

In your main report, reference RADAR tags inline:

```markdown
The platform's account deletion process (RADAR: dp_01) requires users to navigate through 
seven different pages, compared to the single-click signup process. This dark pattern of 
obstruction violates DSA Article 25 requirements for fair interface design.
```

## Common Tagging Scenarios

### Scenario 1: Content Moderation Failure

**Observation**: "Terrorist content remained online for 72 hours despite multiple user reports"

**Tags**:
- `cr_01` - Failure to take action against Illegal Content
- `icg_01` - Terrorist & Extremist Content

**Evidence Needed**:
- Screenshots of the content
- Timestamps showing duration
- Evidence of user reports

### Scenario 2: Hidden Subscription Fees

**Observation**: "Free trial automatically converts to paid subscription without clear notice"

**Tags**:
- `dp_03` - Hidden Information (Sneaking)
- `cp_01` - Misleading Commercial Practices

**Evidence Needed**:
- Signup flow screenshots
- Terms visibility analysis
- User complaint examples

### Scenario 3: Minor Exposure to Harmful Content

**Observation**: "Platform's algorithm recommends violent content to 13-year-old users"

**Tags**:
- `ch_01` - Failure to Implement Adequate Minor Protection
- `tr_03` - Opaque Recommendation Practices

**Evidence Needed**:
- Test account data
- Recommendation screenshots
- Age verification process

## Web Metadata Implementation

### For Online Reports

Include machine-readable metadata:

#### Option 1: Meta Tag
```html
<meta name="radar-assessment" content='{"version":"1.7","platform":"ExampleApp","date":"2024-12-20","categories":{"cr":["cr_01","cr_02"],"dp":["dp_01"]},"totalInfringements":3}'>
```

#### Option 2: JSON-LD
```html
<script type="application/ld+json">
{
  "@context": "https://radar.checkfirst.network/schema.json",
  "@type": "DSAAssessment",
  "version": "1.7",
  "platform": "ExampleApp",
  "assessmentDate": "2024-12-20",
  "infringements": {
	"cr": ["cr_01", "cr_02"],
	"dp": ["dp_01"]
  },
  "totalInfringements": 3,
  "report": "https://example.org/report"
}
</script>
```

## Advanced Tagging

### Severity Indicators

While not part of the official tag, you may indicate severity:

```
- cr_01: Failure to take action against Illegal Content
  * Severity: High (terrorist content)
  * Observed: Active terrorist recruitment videos
  * Duration: 72+ hours online
```

### Pattern Documentation

For systematic violations:

```
- dp_01: Obstruction
  * Pattern: Systematic across all cancellation flows
  * Affected Features: Subscriptions, Account deletion, Marketing opt-out
  * Test Results: 12/12 flows showed obstruction patterns
```

### Cross-Platform Analysis

When assessing multiple platforms:

```
Platform Comparison (RADAR v1.7):
- Platform A: cr_01, cr_02, dp_01 (3 infringements)
- Platform B: cr_01, tap_01, tap_02 (3 infringements)
- Platform C: ch_01, cv_01, cv_02, dmm_01 (4 infringements)

Common Issues: cr_01 (content moderation failures across all platforms)
```

## Troubleshooting

### "I can't find a matching infringement"

1. Try broader search terms
2. Check related categories
3. Review similar observables
4. Consider if it's a new type of violation
5. Submit suggestion for new infringement

### "Multiple tags seem to apply"

- Use all relevant tags
- Document why each applies
- Note primary vs. secondary violations

### "The behaviour is borderline"

- Document what you observe
- Note why it's borderline
- Consider severity and impact
- Err on side of tagging if systematic

## Resources

- **Framework Browser**: [radar.checkfirst.network](https://radar.checkfirst.network)
- **Tag Generator**: [radar.checkfirst.network/generator](https://radar.checkfirst.network/generator)
- **Latest Version**: Check versions.json in repository
- **Submit Suggestions**: [Google Form](https://docs.google.com/forms/d/1U1teYbnEWku9RrJ-rGZDb5EfeKbGA55T0KWO1tIx05s/viewform)

## Questions?

For clarifications about tagging:
1. Check this guide
2. Review framework documentation
3. Open a GitHub issue
4. Contact: radar[at]checkfirst.network