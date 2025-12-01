## Requirement

Please examine the possibility of degradation with reference to the Visual Regression Test results.

- Compare the pull request with the VRT result.
- Review the recognized all before-and-after comparison images (/tmp/vrt/modified_images) created by VRT.

## Expected output

Output in Markdown format with the following headings.

1. Possibility Degradation
1. Pickup of diff images
1. Possibility of non-deterministic rendering
1. Concerns

Set the top-level heading (h1) to “Visual Regression Test Analysis”.
Do not place any text above the top-level heading. Start directly with the heading.

### Possibility Degradation

Output icon and a degradation possibility assessment.

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
- Visual changes that do not match the title or content of the Pull Request

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

Copy and paste the before-and-after image comparison table rows from the VRT results comments, selecting exactly one most impactful image from each causal relationship category (up to 3 categories maximum) with the pull request diff.

Selection criteria:

- Select exactly one representative image from each causality category
- Choose the most impactful example within each category
- Prioritize SP (smartphone) layout differences when available
- Analyze all images to determine their causal relationship before selection
- Maximum 3 causality categories to maintain readability

Note:

- Copy and paste one row from each causality category that exists
- Keep the correct HTML markup for the table
- If copying only tr tags without table structure, wrap them in proper table tags
- Do not modify the contents of the original table rows
- Provide brief explanation for each selected image focusing on the causal relationship

Output format:

```
### {Causality category title 1}

{Casuality category description 2}

<table>
{Copy and paste the before-and-after image comparison table row, selecting exactly one most impactful image}
</table>
```

### Possibility of non-deterministic rendering

For each diff image in the VRT Result comment (/tmp/vrt/result_comment.md), verify the possibility of non-deterministic rendering based on the causal relationship with the Pull Request diff (/tmp/vrt/pr_diff.txt) and the repository source (/tmp/vrt/repo).

Guidelines for non-deterministic rendering:

- Visual changes unrelated to the pull request diff
  Example: Changes to completely unrelated components
  Example: Changes limited to type definitions, tests, or documentation
- Minor anti-aliasing
- Animations
- Rendering delays
- Fluctuations in dynamic content (timestamps, user-specific data, random content)

Based on the verified information, derive the following points for each diff image:

- Percentage: of non-deterministic rendering
- Concise reason: Summary of image diff and reason for judging it as non-deterministic rendering
- Before image path: Copy and paste from vrt result (/tmp/vrt/result_comment.md)

Output format:

{Listed image differences exceeding 50%. | No image differences with high possibility were found.}

| Image                                         | %             | Reason           |
| --------------------------------------------- | ------------- | ---------------- |
| <img src="{Before image path}" width="100" /> | {Percentage}% | {Concise reason} |
| <img src="{Before image path}" width="100" /> | {Percentage}% | {Concise reason} |

<!-- non-deterministic rendering detected: {yes or no} -->

<details>
<summary>Detailed rationale</summary>

{Clearly and comprehensively explain the basis for your determination of causality.}

</details>

### Concerns

List specific issues that require attention. Format each concern with priority, description, and recommended action.

But, Ignore concern not checked on the pull request comment checklist. This is because we do not perform checks as part of our workflow.

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
- Unintended visual changes that don't match PR title and comment scope

Output format:

| Priority    | Description                                                                           |
| ----------- | ------------------------------------------------------------------------------------- |
| 🔥 Critical | Login button disappeared on mobile - Fix responsive CSS before merge                  |
| 🔴 High     | Unintended visual changes that don't match PR title and comment scope - Review impact |
| 🟡 Medium   | Text color contrast too low - Update theme colors                                     |
| 🟢 Low      | Minor spacing difference in footer - Consider design review                           |

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
1. Strictly follow all notes outlined in this prompt without exception.
1. If a language change request is made, also translate all headings and labels.
   - e.g. Pickup of diff images, Critical, Medium Risk, False positives, ...
1. However, keep the content within comments <!-- e.g. text --> in English.

## Additional Requests
