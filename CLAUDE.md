# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Polish-language body mass reduction calculator ("Kalkulator Redukcji Masy Ciała") based on recommendations from the Polish Society for the Treatment of Obesity (PTLO - Polskie Towarzystwo Leczenia Otyłości).

The application is a **single-file web application** - all HTML, CSS, and JavaScript are contained in `index.html`. There are no build steps, dependencies, or external files.

## Architecture

### Single-Page Application Structure

The entire application is contained in `index.html` with three main sections:

1. **CSS Styles** (lines 7-378): All styling is in an inline `<style>` tag
2. **HTML Structure** (lines 380-519): User interface with input fields and condition checkboxes
3. **JavaScript Logic** (lines 521-775): Calculation engine and UI interactions

### Core Functionality

The calculator computes weight loss recommendations based on:
- **User inputs**: Current weight (kg) and height (cm)
- **BMI calculation**: Computed in real-time from weight and height
- **Medical complications**: 14 selectable conditions with associated weight loss targets

### Key Functions (in index.html)

- `calculateBMI(weight, height)` (line 522): Computes BMI from weight and height
- `getBMICategory(bmi)` (line 527): Categorizes BMI into ranges (underweight, normal, obesity grades)
- `updateBMIDisplay()` (line 536): Real-time BMI display as user types
- `toggleCondition(element)` (line 570): Handles condition selection with mutual exclusions
- `calculateWeightLoss()` (line 602): Main calculation logic for weight loss recommendations

### Mutual Exclusion Logic

Some medical conditions are mutually exclusive (lines 578-598):
- **Prediabetes** ↔ **Diabetes Type 2** (cannot select both)
- **MASLD** (fatty liver) ↔ **MASH** (hepatic inflammation) (cannot select both)

### Weight Loss Calculation

Each condition has three weight loss targets: minimum, average, and maximum percentages (stored in `value` attribute as `min|avg|max`).

The calculator:
1. Finds the highest percentage across all selected conditions
2. Calculates weight loss in kg based on current weight
3. Computes target weight ranges
4. Validates that target BMI doesn't fall below 18.5 (underweight threshold)
5. Displays health benefits for each selected condition

## Development

### Running the Application

Simply open `index.html` in any modern web browser. No build process or server required.

```bash
# macOS
open index.html

# Linux
xdg-open index.html

# Or just drag index.html into your browser
```

### Testing

To test the application:
1. Enter weight (e.g., 85 kg) and height (e.g., 175 cm)
2. BMI should calculate automatically
3. Select one or more medical complications
4. Click "Oblicz zalecaną redukcję" (Calculate recommended reduction)
5. Results should display with weight loss targets and health benefits

### Medical Conditions Data

The 14 medical complications are hardcoded in the HTML (lines 411-507). Each includes:
- Polish name
- Weight loss percentage range (min-max)
- Expected health benefits (`data-benefits` attribute)
- Optional mutual exclusion markers (`data-exclusion` attribute)

## Language

All UI text, comments, and user-facing content are in **Polish**. When modifying the application:
- Maintain Polish language for all user-visible text
- Variable names and function names are in English
- Comments in the code are minimal but can be in English

## No External Dependencies

This project intentionally has no:
- Package managers (npm, yarn)
- Build tools (webpack, vite)
- Frameworks (React, Vue, etc.)
- External CSS or JS libraries

Keep it as a standalone HTML file for maximum portability and simplicity.
