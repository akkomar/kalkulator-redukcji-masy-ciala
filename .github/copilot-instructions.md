# Copilot Instructions

This is a Polish-language medical weight reduction calculator based on recommendations from PTLO (Polskie Towarzystwo Leczenia Otyłości - Polish Society for Obesity Treatment).

## Architecture

**Single-file application**: Everything resides in `index.html` with no build system, dependencies, or external files.

```
index.html (777 lines)
├── CSS Styles (lines 7-378)
├── HTML Structure (lines 380-519) 
└── JavaScript Logic (lines 521-775)
```

## Core Medical Logic

### Condition Data Structure
Medical conditions are stored in HTML with `value="min|avg|max"` format:
```html
<input type="checkbox" value="5|10|15" data-name="Cukrzyca typu 2" 
       data-benefits="1) Reduction 1|2) Reduction 2|3) Remission...">
```

### Critical Business Rules

**Mutual Exclusions** (lines 578-598):
- Prediabetes ↔ Diabetes Type 2 (cannot coexist)
- MASLD ↔ MASH (liver conditions hierarchy)

**Safety Constraints**:
- Target BMI must stay ≥18.5 (prevents underweight recommendations)
- Maximum weight loss is capped when BMI safety limit would be violated

### Calculation Algorithm
1. Parse selected conditions' percentages (`min|avg|max`)
2. Find highest percentage across all selected conditions
3. Calculate weight loss in kg based on current weight
4. Validate target BMI ≥18.5, adjust if necessary
5. Display per-condition benefits and overall recommendation ranges

## Key Functions

- `toggleCondition()`: Handles condition selection with mutual exclusion logic
- `calculateWeightLoss()`: Main calculation engine with safety validations
- `updateBMIDisplay()`: Real-time BMI calculation and color-coding
- `calculateBMI()` / `getBMICategory()`: Core BMI utilities

## Development Workflow

**Running**: Simply open `index.html` in any browser - no server or build required.

**Testing**: Enter weight (85kg), height (175cm), select conditions, click "Oblicz zalecaną redukcję".

**Medical Data**: 14 conditions hardcoded in HTML (lines 411-507) with Polish names, percentage ranges, and health benefits.

## Language Convention

- **UI Text**: Always Polish (user-facing)
- **Code**: English (functions, variables, comments)
- **Medical Terms**: Polish medical terminology from PTLO guidelines

## No External Dependencies

Intentionally zero dependencies - no package.json, build tools, frameworks, or external libraries. Keep it simple and self-contained.

## File Structure Pattern

When making changes:
- CSS modifications: Lines 7-378 in `<style>` tag
- UI changes: Lines 380-519 in `<body>` section  
- Logic updates: Lines 521-775 in `<script>` tag

Preserve the single-file architecture and avoid introducing any external dependencies or build complexity.