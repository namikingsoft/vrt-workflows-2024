## Requirement

Please examine the possibility of degradation with reference to the Visual Regression Test results.

- Compare the pull request with the VRT result.
- Review the recognized before-and-after comparison images (/tmp/vrt/modified_images) created by VRT.

## Expected output

Output in Markdown format with the following headings.

1. Degradation possibility
1. Pickup of diff images
1. Correlation Analysis with the Pull Request
1. Concerns

### Degradation Possibility

Output icon and the degradation possibility assessment.

Explain the reason concisely.

- Explain the factors that led to this percentage
- Reference specific visual changes and their relationship to code changes
- Consider user impact and severity

Example:

```
🔴 High|Medium|Low Risk (nn%)

The reason concisely
```

Use this scale to determine degradation possibility:

🔴 70-100%:

- Critical visual issues that significantly impact user experience
- Degradation causally related to the diff of the pull request

🟡 30-69%:

- Moderate changes that may affect usability or appearance

🟢 0-29%:

- Minor differences with minimal user impact
- False positives unrelated to the diff of the pull request

Consider these factors:

- Severity of visual changes
- Relationship between VRT results and PR changes
- Usability and experience impact
- Accessibility concerns (contrast, readability)
- Number of affected components/pages

### Pickup of diff images

Copy and paste the before-and-after image comparison table in the VRT results comments, leaving only one row and explain.

Note:

- Copy and paste the row likely to have the greatest impact.
- Do not modify the contents of the original table.

### Correlation Analysis with the Pull Request

To clarify potential false detections, analyze causality based on the repository source code, the Pull Request, and the VRT results.

1. Check the relationship between detected visual changes and the Pull Request diff (/tmp/vrt/pr_diff.txt)
2. Reference the repository source code (/tmp/vrt/repo) to examine causal relationship with modified images
3. Determine if the visual differences are:
   - Expected results of the code changes
   - Potential degradation not intended by the Pull Request
   - False positives completely unrelated to the Pull Request diff
4. Provide reasoning for your assessment based on code analysis

False Positives Guidelines:

- Visual changes unrelated to the Pull Request diff
  e.g. changes in completely unrelated components
  e.g. changes limited to type definitions, tests, or documentation
- Minor anti-aliasing
- Animation
- Rendering delays
- Dynamic content variations (timestamps, user-specific data, random content)

### Concerns

List specific issues that require attention. Format each concern with priority, description, and recommended action.

Format:

- **[Priority]** Description - Recommended action

Priority levels:

- Critical: Blocks merge, immediate fix required
- High: Should be addressed before merge
- Medium: Can be addressed post-merge
- Low: Minor, optional improvement

Types of concerns:

- Visual regressions affecting functionality
- Layout/alignment issues impacting usability
- Accessibility problems (contrast, readability)
- Unintended side effects from code changes

Example:

- **[Critical]** Login button disappeared on mobile - Fix responsive CSS before merge
- **[High]** Text color contrast too low - Update theme colors
- **[Medium]** Minor spacing difference in footer - Consider design review

If no concerns are found, state: "No significant concerns identified."

## References to the following files and directory

| Path                       | Description                                       |
| -------------------------- | ------------------------------------------------- |
| /tmp/vrt/result_comment.md | VRT Result comment                                |
| /tmp/vrt/repo              | Source code directory of this repository          |
| /tmp/vrt/pr_view.txt       | Description of this pull request                  |
| /tmp/vrt/pr_diff.txt       | Source diff of this pull request                  |
| /tmp/vrt/modified_images   | Before-and-after comparison images created by VRT |

## Notice to AI

1. Do not use your todo tools for stability.
1. If a language change request is made, also translate headings and labels.
   - e.g. Pickup of diff images, Critical, Medium Risk, False positives, ...

## Additional Requests
