# Employee-Motivation-Financial-Incentives-Survey
Employee Motivation — Financial Incentives Survey

# Employee Motivation — Financial Incentives Survey

A focused Class XII Business Administration/Skill Subject project instrument built around the six financial motivation methods supplied for Chapter 5:

1. Pay and Allowance
2. Bonus
3. Profit Sharing
4. Commission
5. Performance-Linked Incentives
6. Stock Options

## Files

- `index.html` — landing screen, survey screen and post-submission thank-you screen.
- `style.css` — participant-facing style.
- `script.js` — 20-question survey, validation, optional photo compression and submission.
- `app-script/Code.gs` — Apps Script backend, duplicate-email blocking, Google Sheet storage, Drive photo storage and analytics.
- `app-script/admin.html` — private owner dashboard.

## Core design

Exactly 20 core questions measure only the six financial methods above. Name, email, organisation, department, optional workplace photo, optional written summary, human-verification calculation and agreement are metadata/verification fields and are not part of the 20.

Response types deliberately vary: multi-select with conditional Other, 0–100 scalar bar, seven-point directional motivation scale, single-choice provision/clarity questions and direct six-method comparison.

The dashboard derives two descriptive indices:

- **Incentive Index:** pay/allowance satisfaction + bonus clarity + profit-sharing fairness/transparency + commission clarity + performance-link strength.
- **Motivation Index:** extra-pay effect + bonus effect + profit-sharing effect + commission effect + performance-linked effect + stock-option long-term effect.

These are analytical indices for the school project, not clinical or employment assessments.

## Apps Script setup

1. Create/open the Google Sheet.
2. Extensions → Apps Script.
3. Replace `Code.gs` with `app-script/Code.gs`.
4. Add an HTML file named exactly `admin` and paste `app-script/admin.html`.
5. Confirm `OWNER_EMAIL` in `Code.gs` is the owner's Google account email.
6. Save and run `setup()` once; authorize Sheets and Drive access.
7. If the old `Responses` sheet contains the earlier 12-question schema, `setup()` preserves it by renaming it `Responses_Old_YYYYMMDD_HHMMSS` and creates a clean `Responses` sheet for this survey.
8. A Drive folder named `Employee Motivation Photos` is created automatically.

## Public survey deployment

Deploy as **Web app**:

- Execute as: **Me**
- Who has access: **Anyone**

The supplied `script.js` already contains the previously created public Apps Script URL. After replacing `Code.gs`, update that deployment to a new version so the `/exec` URL serves the new code.

## Private admin deployment

Create a second Web app deployment from the same Apps Script project:

- Execute as: **Me**
- Who has access: **Only myself**

Open the private deployment URL with `?view=admin`.

Example:
`https://script.google.com/macros/s/YOUR_PRIVATE_DEPLOYMENT/exec?view=admin`

The code also checks `OWNER_EMAIL`.

## GitHub Pages

Publish these participant-facing files in the GitHub Pages repository:

```text
index.html
style.css
script.js
```

Do not publish `Code.gs` or `admin.html` as the public participant site.

## Data rules

- Email is canonicalized to lowercase and checked server-side; duplicate email submissions are rejected.
- One organisation can have multiple respondents because uniqueness is based on email, not organisation name.
- First name is required and must use standard capitalization such as `Joyson`.
- Second name is optional and follows the same standardization when supplied.
- Generic organisation entries such as `NGO`, `company`, `organisation`, `firm` and similar exact labels are rejected.
- The alias `aakash` is stored as `Aakash Institute`.
- Invalid fields show a specific red error message and the form scrolls to the first problem.
- Workplace photo and written summary are optional.
- Uploaded photos are compressed client-side and stored in Drive; the file URL is stored in the `Workplace Photo` column.

## Dashboard

The owner dashboard refreshes every 30 seconds and can be refreshed manually. It includes:

- participant, organisation and department counts;
- incentive index vs respondent;
- motivation index vs respondent;
- incentives-vs-motivation scatter plot with linear trend;
- six-method comparison from Question 20;
- descriptive method evidence scores;
- mean, median, mode, mean deviation, minimum and maximum;
- average first-difference rates per respondent;
- regression slope for Δ(motivation)/Δ(incentives);
- correlation between incentive and motivation indices;
- a recalculated sample-average model user;
- the exact four-column respondent summary table requested by the project: User Name | User Mail Id | User Department | User Summary;
- CSV export.

The model user is descriptive: it shows the current sample average and updates as sample size grows. It is not a prescriptive "perfect" employee.

## CAPTCHA note

The participant page uses a lightweight arithmetic human-verification check. It is suitable for a small academic survey but is not equivalent to Google reCAPTCHA or enterprise bot protection. Duplicate-email prevention and Apps Script locking provide the main integrity controls.
