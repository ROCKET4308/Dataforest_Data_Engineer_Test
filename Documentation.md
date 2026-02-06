# Data Processing & Matching Documentation

## 1. Matching Approach

When I matched companies from two datasets, I focused on finding real connections even when names were written differently. I created a cleaned-up company name, `company_norm`, to make comparisons consistent.

I merged Dataset 1 with Dataset 2 using these normalized names. To make sure the matches were real, I verified locations using a tiered approach: first I looked for exact matches on postcode, city, state, and country, then loosened the criteria step by step down to postcode only. Once a strong match was found, I didn’t check lower tiers.

---

## 2. Data Quality Issues Found

### Dataset 1

Dataset 1 had several issues:

- **Missing values:** Many records were missing country, secondary address lines, or postal codes.  
- **Inconsistencies:** Countries and states appeared in multiple formats, and a few entries had clearly incorrect data in the wrong fields.  
- **Shared addresses:** Some addresses were used by multiple clients. This could be legitimate or indicate messy data.

### Dataset 2

Dataset 2 had its own quirks:

- **Standardization issues:** Country, state, and city names were inconsistent, with mixed uppercase, full names, and codes.  
- **Missing values:** Some primary address fields were blank, making certain records unusable. Extra address lines were often empty, which is expected.  
- **No duplicates:** Each customer number and address combination was unique.

---

## 3. Normalization / Transformations Applied

To make matching reliable, I applied these cleaning steps:

- **Company names and cities:** Converted to lowercase, removed extra spaces, stripped unusual characters.  
- **Postcodes:** Made uppercase and removed spaces.  
- **Countries:** Mapped to consistent two-letter codes (e.g., Canada → CA, United States → US).  
- **States/Provinces:** Standardized to two-letter codes (e.g., Ontario → ON, Quebec → QC, British Columbia → BC).

---

## 4. Calculated Metrics

To measure how well the matching worked, I tracked:

- How many companies in Dataset 1 found a match in Dataset 2.  
- How many companies didn’t match.  
- Cases where one company matched multiple entries in Dataset 2, indicating duplicates or ambiguous naming.  
- Matches where shared physical locations were confirmed using the tiered logic.

=== Summary Metrics ===
- Total companies in Dataset 1: 1013
- Companies matched in Dataset 2: 425 41.95%
- Companies unmatched: 588 58.05%
- One-to-many matches: 35 3.46%
- Number of overlapping locations: 399