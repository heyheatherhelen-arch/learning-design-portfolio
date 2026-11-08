# Accessibility audit: From AI Competencies to Curriculum — Version 5

**Audit date:** November 8, 2026  
**Artifact:** `From_AI_Competencies_to_Curriculum_V5_Accessibility_Fix.html`  
**Target:** WCAG 2.2 Level AA  
**Result:** **Not certified / conformance not established.** Automated and scripted checks passed in the tested areas; several manual success-criterion checks remain outstanding.

## Scope and methods

- Loaded the complete HTML into headless Chromium using Playwright and exercised each of five sections at viewport widths of 1440, 1280, 768, 640, 390, and 320 CSS pixels (height varied). Browser sandbox restrictions prevented direct `file://` navigation; the same file contents were loaded using `page.set_content`.
- Checked for document-level horizontal overflow, JavaScript page errors, unique IDs, accessible form labels, text-bearing button names, keyboard focus visibility, heading focus after navigation, and dynamic feedback status/live-region markup.
- Inspected Chromium's accessibility tree for unnamed interactive elements in the Decide section. No unnamed button, radio, textbox, combobox, or checkbox nodes were detected in that tested section.
- Sampled computed foreground/background contrast on visible text in the Decide section using a custom script. No failures were found in that sample. This is not an exhaustive contrast audit and the script does not fully resolve layered/alpha backgrounds.
- Confirmed that the three horizontally scrollable tables are keyboard-focusable (`tabindex=0`) and have accessible labels.
- Tested a 200% CSS zoom approximation at a 1280px viewport without document overflow.

## Results

| Test area | Result | Qualification |
|---|---|---|
| Five-section reflow at 320–1440 CSS px | Pass | No document-level overflow in tested states; intentional labeled scroll regions exist |
| Keyboard focus indicator | Pass in sample | Full keyboard-only journey and all controls not exhaustively tested |
| Navigation focus management | Pass in sample | Section heading receives programmatic focus |
| Apply stage focus management | Pass in sample | Stage heading receives focus |
| Accessible names on HTML form fields | Pass in DOM inspection | Does not establish contextual clarity of every name |
| Accessible names in Chromium accessibility tree | Pass in Decide section | Other sections not exhaustively examined in AX tree |
| Dynamic status and feedback | Markup present | Real NVDA/JAWS/VoiceOver announcement behavior not verified |
| Text contrast | No failures in sampled Decide text | Complete color/contrast audit outstanding |
| 200% zoom approximation | Pass | Actual browser zoom and 400% full workflow outstanding |
| 400% zoom | Inconclusive | A previous test applied 400% zoom to a 320px viewport, effectively creating an 80px CSS-width layout. This is **not** a valid proxy for WCAG 1.4.10's 320 CSS px reflow requirement. At 320 CSS px, the module passed reflow checks. |
| Screen-reader comprehension | Not tested | Requires real assistive technology and human evaluation |
| WCAG 2.2 AA conformance | **Not established** | Full success-criterion audit and manual testing needed |

## Outstanding verification required before a WCAG 2.2 AA claim

1. Conduct the full experience with NVDA + Firefox or Chrome and VoiceOver + Safari, including radio groups, dashboard metric switches, choice feedback, the five Apply stages, and downloaded brief.
2. Conduct a keyboard-only end-to-end journey; confirm no traps, predictable focus, keyboard scroll of wide tables, and no focus loss when stages are hidden or revealed.
3. Verify at real 200% and 400% browser zoom with a 1280px browser viewport, including content reflow and all input controls.
4. Audit all WCAG 2.2 A/AA success criteria applicable to the module, including semantics, relationships, name/role/value, focus not obscured, target sizes, error identification, status messages, and non-text contrast.
5. Review chart and table relationships with a screen reader and verify that alternative text/data representation supports equivalent understanding.
6. Run a standards-based accessibility engine (such as axe-core) on every visible section and interaction state, then manually review findings. **axe-core was not available in this offline runtime**, so this was not completed.
7. Test on a real mobile device with mobile screen reader and touch interaction.

## Release recommendation

**Appropriate for internal/formative usability review. Not appropriate to label 'WCAG 2.2 AA compliant,' 'fully accessibility-tested,' or 'certified accessible.'** Once outstanding manual and automated checks have been completed and defects resolved, produce a criterion-by-criterion conformance record.

## Reproducibility

Test scripts and machine-readable results: `audit_full.py`, `audit_extra.py`, `Accessibility_Audit_V5_results.json`, `Accessibility_Audit_V5_extra.json`.
