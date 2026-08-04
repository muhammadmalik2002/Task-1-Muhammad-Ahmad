# Project 1: Advanced EDA & Feature Engineering

**Data Science Internship — Decode Labs**
**Intern:** Muhammad Ahmad

## Overview
This project transforms a raw e-commerce order dataset into a clean, machine-learning-ready dataset through statistical missing value imputation, outlier treatment, and feature engineering — all implemented using vectorized Pandas/NumPy operations.

## Dataset
- **Source:** `Dataset_for_Data_Analytics.xlsx`
- **Size:** 1,200 e-commerce order records, 14 columns
- **Fields:** OrderID, Date, CustomerID, Product, Quantity, UnitPrice, ShippingAddress, PaymentMethod, OrderStatus, TrackingNumber, ItemsInCart, CouponCode, ReferralSource, TotalPrice

## What Was Done

### 1. Missing Value Treatment
- Only `CouponCode` had missing values (309 rows, ~25.75%)
- Applied **KNN Imputation** (k=5) on the label-encoded column, using related numeric order attributes (Quantity, UnitPrice, ItemsInCart, TotalPrice) to estimate the most statistically likely category for each missing row

### 2. Outlier Detection & Treatment
- Applied the **IQR method** (Q1 − 1.5×IQR to Q3 + 1.5×IQR) across all numeric columns: `Quantity`, `UnitPrice`, `ItemsInCart`, `TotalPrice`
- Outliers were **capped (winsorized)** via `numpy.clip()` rather than deleted, to preserve row count and data integrity

### 3. Feature Engineering
Three new predictive features were engineered:
| Feature | Description |
|---|---|
| `OrderMonth` | Calendar month extracted from `Date`, capturing seasonality |
| `DiscountPct` | % gap between expected price (`Quantity × UnitPrice`) and actual `TotalPrice`, capturing discount/coupon effect |
| `IsRepeatCustomer` | Binary flag for customers with more than one order, capturing retention |

## Results
- **Final dataset:** 1,200 rows × 17 columns (14 original + 3 engineered)
- Zero missing values remaining
- All numeric fields statistically bounded

## Repository Contents
- `Project - I.ipynb` — full notebook (Google Colab compatible)
- `Cleaned Dataset (Project - I).csv` — final cleaned output dataset
- `Data Science Project 1.pdf` — original project brief from Decode Labs
- `Project 1 Report.docx` — formal write-up of methodology and results

## Tools & Libraries
`Python`, `Pandas`, `NumPy`, `Scikit-learn` (KNNImputer, LabelEncoder)

## How to Run
1. Open `Project - I.ipynb` in Google Colab
2. Upload `Dataset_for_Data_Analytics.xlsx` when prompted (or mount Google Drive)
3. Run all cells top to bottom
