![Student Performance EDA](assets/banner.svg)

# Student Performance EDA — study hours explain 60% of the variance, the rest is mostly noise

200 students, four plausible predictors, one exam score. I ran the work in Excel and then again in Python, because the point of a second pass is to see whether the spreadsheet answer survives contact with code.

`Excel` · `Python` · `pandas` · n = 200

---

## The question

> **Of study hours, sleep, attendance and previous scores, which actually predicts exam performance — and how much of the score can be explained at all?**

## Headline findings

Pearson correlation with `exam_score` (n = 200):

| Predictor | r | Verdict |
|---|---|---|
| `hours_studied` | **0.777** | Strong — the dominant driver |
| `previous_scores` | 0.431 | Moderate |
| `attendance_percent` | 0.226 | Weak |
| `sleep_hours` | 0.188 | Weak |

1. **Four variables explain 84% of exam-score variance** (linear model, R² = 0.841). Study hours alone explain ~60% (r² = 0.603); previous scores alone explain only 18.6%.
2. **Sleep barely matters here** — r = 0.19. The popular "less sleep, worse results" story does not survive this dataset.
3. **The gap is real at the tails:** students with previous scores ≥ 85 average 38.6 on the exam; those under 55 average 30.1.
4. **The exam is not scored out of 100:** scores run 17.1 to 51.3, median 34.1. Reading this column as a percentage is wrong, and it is the first thing a reviewer tries to do.

The honest conclusion: for this cohort, effort beats both aptitude proxies and attendance. That is a finding about 200 students, not a law.

## Method

1. Loaded the 200-row CSV; confirmed no missing values and unique student IDs.
2. Built histograms and scatter plots with trendlines in Excel (the PNGs below).
3. Repeated it in Python: Pearson correlation per predictor, then ordinary least squares on all four.
4. Compared the two paths — the Excel trendline slopes and the Python coefficients agree, which is the only reason to do it twice.

Regression coefficients (intercept, hours, sleep, attendance, previous): `-2.14, 1.56, 0.95, 0.11, 0.18`.

## Charts

| File | What it shows |
|---|---|
| `charts/hist_exam_score.png` | Score distribution (median 34.1) |
| `charts/hist_attendance.png` | Attendance spread, 50.3–100% |
| `charts/scatter_hours_vs_exam.png` | The strong relationship, r = 0.777 |
| `charts/scatter_previous_vs_exam.png` | The moderate one, r = 0.431 |
| `charts/scatter_attendance_vs_exam.png` | The weak one, r = 0.226 |
| `charts/scatter_sleep_vs_exam.png` | The near-flat one, r = 0.188 |

## Reproduce

```bash
pip install pandas numpy openpyxl matplotlib seaborn
jupyter lab
```

Or open `data/student_result_analysis.xlsx` for the original pivots and trendlines.

## Limitations

- **Correlation is not causation.** Study hours are self-selected; motivated students both study more and score higher for reasons this file cannot separate.
- 200 rows, no term, cohort or school breakdown, and no note on how the sample was drawn.
- The exam scale is undocumented, so absolute scores are not comparable across institutions.

## Next

Add a term/teacher dimension to see whether the hours effect survives a change of cohort, and test a quadratic term — the scatter suggests returns to study hours flatten at the top end.

---

**Md. Abir Ul Islam** · [GitHub](https://github.com/abir2022) · [LinkedIn](https://www.linkedin.com/in/md-abir-ul-islam/)
