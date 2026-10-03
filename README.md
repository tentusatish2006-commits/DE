# SmartDefect AI

**Detect. Understand. Prevent.**

## Problem

Manufacturing sensor and defect data can be difficult to validate and turn into timely quality actions. Missing readings, duplicate batches, and machine-level patterns can obscure what a team should investigate.

## Solution

SmartDefect AI is a browser-based manufacturing quality dashboard. It validates and analyzes a CSV locally, makes cleaning steps visible, and turns the current dataset into machine summaries, prototype risk scores, charts, insights, and recommendations.

## Features

- Load the included demo dataset or upload a manufacturing CSV by file picker or drag and drop
- Validate required columns and numeric values; report missing values and exact duplicate records
- Clean missing numeric values with median imputation and remove exact duplicate rows
- Classify temperature and batches with defects
- Explore machine health, prototype risk scores, and batch-level history
- Filter and search records; interact with the analytics charts
- Generate dataset-based insights, recommendations, and alerts
- Explore a clearly labeled live simulation with adjustable anomaly thresholds
- Download the cleaned dataset and a generated analysis report

## Technology

- React, TypeScript, and Vite
- Tailwind CSS
- Recharts
- Lucide React

All CSV processing takes place in the browser. Uploaded data is not sent to a server.

## How to run

Use the SmartDefect AI web preview in Replit. To run the app in the workspace, start the `artifacts/smartdefect-ai: web` workflow.

## Dataset format

The CSV must include these case-sensitive columns:

```csv
BatchID,MachineID,Temperature,Vibration,DefectCount
B101,M1,72,2.1,0
```

Temperature, Vibration, and DefectCount must be numeric when provided. Blank numeric cells are treated as missing and can be filled during cleaning.

## Cleaning and analysis methodology

- Missing Temperature and Vibration values are replaced with the median of the available values in that column.
- Exact duplicate data records are removed.
- Temperature is categorized as LOW below 75, NORMAL from 75 through 85 inclusive, and HIGH above 85.
- A batch is classified as defective when `DefectCount > 0`.
- Machine health includes average temperature and vibration, total defects, and defect rate.
- Prototype risk combines normalized temperature, vibration, and observed defect-history components with weights of 0.35, 0.35, and 0.30, respectively. The dashboard explains its normalization and status thresholds.

Risk labels are Healthy (0–39), Warning (40–69), and Critical (70–100).

## Limitations

The prototype risk score is a transparent heuristic, not a scientifically validated machine-learning prediction. Insights describe the currently uploaded dataset and do not imply that correlation proves causation. Simulation readings are not live IoT sensor data. The supplied demo dataset is small; larger historical datasets and production-grade validation are recommended before using this approach for operational decisions.