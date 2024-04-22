# Prioritize Technical Debt

Beyond simply identifying issues. Digma also analyzes their effect on the application to determine their criticality.&#x20;

### Issue criticality

Each issue is assessed for criticality based on its overall effect on the application. In local environments, this is merely measured by the severity of the issue and the scope of different application flows affected by it. In shared environments such as CI, staging, or production, however, actual usage is also measured to determine the true impact of the issue.&#x20;

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

The criticality of each issue is reflected by the color coding of the issue icon. Hovering over the icon will also reveal the criticality score. When reviewing the overall issue list, you can choose to sort by latest or by the most critical issues to help prioritize the backlog and avoid micro-optimizations:

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### Asset performance impact

Digma assesses each asset (query, code location, endpoint etc.) to determine its performance impact on the application. This helps identify the best candidates for optimization that would carry the most 'punch for the bucks' if their performance is improved. Assessment of performance impact is available only in shared environments such as CI/staging or production and relies on measuring actual usage.

For example, a slow query that is rarely used or has a marginal effect on the overall request would be ranked lower than a slow query that is heavily used and critically affects multiple flows.





