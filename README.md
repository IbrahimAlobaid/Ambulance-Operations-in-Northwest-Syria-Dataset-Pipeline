
# Ambulance Operations in Northwest Syria Dataset Pipeline

This project downloads and merges the monthly Excel files of the **Ambulance Operations in Northwest Syria** dataset from HDX.

The script uses the HDX CKAN API to fetch all available Excel resources, downloads them into a local folder, reads the ambulance sheets, cleans the columns, adds useful metadata, and exports one merged CSV file.

## Dataset Source

Dataset: Ambulance Operations in Northwest Syria  
Publisher: The White Helmets  
Platform: Humanitarian Data Exchange HDX  
Dataset ID:

```text
ambulance-operations-in-northwest-syria-jan
```

## Project Structure

```text
.
├── download_and_merge_ambulance.py
├── README.md
└── Dataset/
    ├── Ambulance-Syria-January-2024.xlsx
    ├── Ambulance-Syria-February-2024.xlsx
    └── ambulance_syria_merged.csv
```

The `Dataset` folder is created automatically when the script runs.

## What the Script Does

The script performs the following steps:

1. Connects to the HDX API.
2. Fetches all dataset resources.
3. Filters only Excel files.
4. Downloads missing Excel files into the `Dataset` folder.
5. Reads the `Ambulance` sheet from each file.
6. Cleans empty columns and column names.
7. Adds metadata columns:

   * `source_file`
   * `report_year`
   * `report_month`
   * `report_period`
8. Merges all monthly files into one CSV file.
9. Saves the final output as:

```text
Dataset/ambulance_syria_merged.csv
```

## Requirements

This project uses:

```text
python
pandas
requests
openpyxl
```

## Running the Project with uv


Initialize the project with `uv`:

```bash
uv init
```

create venv
```bash
uv venv
.venv\Scripts\activate
```

Add the required packages:

```bash
uv add pandas requests openpyxl
```

Run the script:

```bash
uv run python download_and_merge_ambulance.py
```

After running, the final merged file will be available here:

```text
Dataset/ambulance_syria_merged.csv
```

## Notes

The script skips files that already exist locally. This means you can run it multiple times without downloading the same files again.

The output CSV is saved using `utf-8-sig` encoding to make Arabic text display correctly in Microsoft Excel.

If HDX changes the file naming pattern or sheet structure, the script may need small adjustments, especially in the `extract_month_year` function or the Excel `header` value.


