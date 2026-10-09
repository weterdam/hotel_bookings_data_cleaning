# Hotel Bookings Data Cleaning (Python and pandas)

A data cleaning project in Python that takes a raw hotel bookings dataset of about 119,000 records and turns it into an analysis-ready table. It covers missing values, column renaming, data type correction, binning, and duplicate removal.

## Project Overview

Before any analysis or modelling can happen, raw data has to be checked and fixed. In this project I worked through a standard data cleaning workflow with pandas on a real-world hotel bookings dataset, documenting each step in a Jupyter notebook.

## Dataset

- **Source:** Hotel bookings dataset (`hotel_bookings.csv`)
- **Size:** 119,390 rows and 32 columns before cleaning, 87,389 rows after removing duplicates
- **Contents:** Booking details for a resort hotel and a city hotel, including:
  - Booking info: `hotel`, `is_canceled`, `lead_time`, `reservation_status`
  - Arrival dates: `arrival_date_year`, `arrival_date_month`, `arrival_date_week_number`, `arrival_date_day_of_month`
  - Stay details: `stays_in_weekend_nights`, `stays_in_week_nights`
  - Guests: `adults`, `children`, `babies`, `country`
  - Booking channel: `market_segment`, `distribution_channel`, `agent`, `company`
  - Room and payment: `reserved_room_type`, `assigned_room_type`, `deposit_type`, `adr`

## Cleaning Steps

| Step | What I did | pandas methods |
|---|---|---|
| 1. Load and inspect | Read the CSV and previewed the first rows | `read_csv()`, `head()` |
| 2. Find missing values | Calculated the percentage of nulls in each column | `isnull().sum()` |
| 3. Handle missing values | Dropped `company` (about 94% missing), filled `children` with -1 as a flag, filled `country` with "Unknown", and filled `agent` with the column mean | `drop()`, `replace()`, `mean()` |
| 4. Rename columns | Made column names clearer (`adults` to `num_adults`, `children` to `num_children`, `babies` to `num_babies`) | `rename()` |
| 5. Correct data types | Converted `num_children` to integer, and `is_repeated_guest` and `is_canceled` to boolean | `astype()`, `dtypes` |
| 6. Create bins | Grouped `lead_time` into 100-day ranges (0-100, 101-200, ... 701-800) in a new column | `pd.cut()` |
| 7. Remove duplicates | Identified duplicated rows and removed them, keeping the last occurrence | `duplicated()`, `drop_duplicates()` |

## Results

| Metric | Before | After |
|---|---|---|
| Rows | 119,390 | 87,389 |
| Columns | 32 | 32 (`company` dropped, `lead_time_binned` added) |
| Duplicate rows removed | | 32,001 |


## Tools and Skills Used

- Python 3
- pandas and NumPy
- Jupyter Notebook
- Data cleaning, missing value imputation, type conversion, feature binning, deduplication

## Files

| File | Description |
|---|---|
| `data_cleaning_project.ipynb` | The full cleaning workflow with code and outputs |
| `hotel_bookings.csv` | The raw dataset |

## How to Run

1. Clone this repository.
2. Install the dependencies: `pip install pandas numpy jupyter`
3. Make sure `hotel_bookings.csv` is in the same folder as the notebook.
4. Run `jupyter notebook` and open `data_cleaning_project.ipynb`.
5. Run the cells from top to bottom.

## Key Learnings

- Dropping a column is reasonable when most of its values are missing (`company` was about 94% null).
- Choosing how to fill missing values depends on the column: a flag value, a label like "Unknown", or a mean each suit different data.
- Setting correct data types makes later analysis and memory use more efficient.
- Binning continuous values such as `lead_time` makes them easier to group and summarize.

## Author

**Allen Abajong**
https://www.linkedin.com/in/allen-weterdam-abajong-3905bb328 | allenabajongweterdam@gmail.com
