# Suggested Power BI Measures

Create a table named `QualityRelease` from `data/synthetic_quality_release_data.csv`.

```DAX
Total Lots =
DISTINCTCOUNT(QualityRelease[lot_id])

FTR Lots =
CALCULATE(
    [Total Lots],
    QualityRelease[ftr_status] = "FTR"
)

Non-FTR Lots =
CALCULATE(
    [Total Lots],
    QualityRelease[ftr_status] = "Non-FTR"
)

FTR Rate =
DIVIDE([FTR Lots], [Total Lots])

Non-FTR Rate =
DIVIDE([Non-FTR Lots], [Total Lots])

Moisture Exception Lots =
CALCULATE(
    [Total Lots],
    QualityRelease[moisture_in_spec] = FALSE()
)

Bushel Weight Exception Lots =
CALCULATE(
    [Total Lots],
    QualityRelease[bushel_weight_in_spec] = FALSE()
)
```

## Recommended Dashboard Layout

**KPI cards**
- Total Lots
- FTR Rate
- Non-FTR Lots
- Moisture Exception Lots
- Bushel Weight Exception Lots

**Visuals**
- FTR Rate by Production Month
- Non-FTR Lots by Exception Reason
- Non-FTR Rate by Line
- Lot-level exception table

**Slicers**
- Production Date
- Line
- Product Family
- FTR Status

The thresholds in the synthetic dataset are illustrative portfolio assumptions and are not proprietary production specifications.
