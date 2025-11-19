# cDNA Calculator

![Version](https://img.shields.io/badge/version-2.1.0-blue.svg)
![R](https://img.shields.io/badge/R-4.0%2B-brightgreen.svg)
![License](https://img.shields.io/badge/license-MIT-orange.svg)

A Shiny application for calculating RNA and DEPC water volumes for cDNA synthesis reactions, with automatic volume adjustments based on RNA concentration to ensure accurate pipetting.

## Features

- **Automatic Volume Adjustment**: Intelligently adjusts total reaction volume based on RNA concentration to keep RNA volumes within pipettable range (0.3-1.5 µL)
- **Interactive Data Tables**: Sortable, searchable tables with color-coded volume adjustments
- **Print Functionality**: Print clean, formatted tables for lab use
- **Excel Export**: Download results with both sample calculations and reaction volumes
- **Modern UI**: Clean, professional interface with gradient themes and responsive design

## Installation

### Prerequisites

- R (version 4.0.0 or higher)
- RStudio (recommended)

### Required R Packages

The application will automatically install required packages on first run:

```r
packages <- c("shiny", "bslib", "shinyWidgets", "shinyjs", "readxl", "DT", "openxlsx")
```

### Running the App

1. Save the R script as `app.R`
2. Open the script in RStudio
3. Click "Run App" button, or run:

```r
shiny::runApp()
```

## Usage

### Input File Requirements

Prepare an Excel file (`.xlsx`) with the following columns:

| Column Name | Description | Example |
|-------------|-------------|---------|
| `SampleNumber` | Sample identifier | 13N, 13T, 17N |
| `RNA_Concentration` | RNA concentration in ng/µL | 167.68, 435.84 |

**Note:** If your file contains a `SampleName` column, it will be automatically removed.

### Example Input File

```
| SampleNumber | RNA_Concentration |
|--------------|-------------------|
| 13N          | 167.68           |
| 13T          | 435.84           |
| 17N          | 116.14           |
```

### Volume Adjustment Rules

The application automatically adjusts total reaction volume based on RNA concentration to ensure RNA volumes remain in the pipettable range:

| RNA Concentration (ng/µL) | Total Volume | RNA Volume Target |
|---------------------------|--------------|-------------------|
| 0 - 100                   | 5 µL         | Higher volumes    |
| 100 - 165                 | 10 µL        | Standard          |
| 165 - 600                 | 20 µL        | Mid-range         |
| 600 - 800                 | 30 µL        | Lower volumes     |
| 800 - 1200                | 40 µL        | Very low volumes  |
| ≥ 1200                    | 50 µL        | Ultra-low volumes |

### Output Columns

The application calculates and displays:

- **SampleNumber**: Your sample identifier
- **RNA_Concentration**: Input concentration (ng/µL)
- **Total_Volume**: Adjusted total reaction volume (µL)
- **RNA_Volume**: Calculated RNA volume to pipette (µL)
- **DEPC_Volume**: Calculated DEPC water volume to pipette (µL)

### Color Coding

Tables use color highlighting to indicate volume adjustments:

- **Light Blue** (5 µL): Very low concentration samples
- **White** (10 µL): Standard volume (no adjustment needed)
- **Yellow** (20 µL): Moderate adjustment
- **Pink** (30 µL): Significant adjustment
- **Light Red** (40 µL): High adjustment
- **Red** (50 µL): Maximum adjustment

## Features in Detail

### 1. Upload Data

- Click "Browse..." to select your Excel file
- The app validates columns and provides error messages if columns are missing
- Successfully loaded samples are confirmed with a notification

### 2. View Calculations

- **Sample Calculations Table**: Shows all samples with calculated volumes
  - Sortable by any column
  - Searchable by sample number or concentration
  - Pagination for large datasets
  - Color-coded volume adjustments

- **Reaction Volumes Table**: Standard cDNA synthesis components per sample
  - 5x SYBR RT Mix: 2.0 µL
  - 10x Reverse Transcriptase: 1.0 µL
  - Unispike: 0.5 µL
  - Nuclease-free water: 4.5 µL
  - RNA: 2.0 µL

### 3. Print Tables

- Click "Print Tables" to open print dialog
- Prints both tables with clean formatting
- All samples included (no pagination in print view)
- Optimized for standard letter/A4 paper

### 4. Download Results

- Click "Download Results" to export Excel file
- Two sheets included:
  - **Sample Calculations**: All calculated volumes
  - **Reaction Volumes**: Standard reaction components
- Filename format: `cDNA_calculations_YYYYMMDD.xlsx`

## Calculation Formula

The RNA volume is calculated using:

```
RNA_Volume (µL) = (5 / RNA_Concentration) × Total_Volume
```

Where:
- `5` is the target amount of RNA (ng)
- `RNA_Concentration` is in ng/µL
- `Total_Volume` is determined by concentration range

DEPC volume is calculated as:

```
DEPC_Volume (µL) = Total_Volume - RNA_Volume
```

## Example Workflow

1. **Prepare Excel file** with sample numbers and RNA concentrations
2. **Launch the app** in RStudio
3. **Upload your file** using the file browser
4. **Review calculations** in the interactive table
   - Check that RNA volumes are in pipettable range
   - Note which samples have adjusted volumes
5. **Print tables** for bench work
6. **Download Excel** file for records

## Troubleshooting

### Error: "Excel must have columns: SampleNumber, RNA_Concentration"

- Ensure your Excel file has exactly these column names
- Column names are case-sensitive
- Check for extra spaces in column names

### RNA volumes still too small or too large

- Very extreme concentrations (< 5 ng/µL or > 1500 ng/µL) may produce volumes outside the ideal range
- Consider diluting or concentrating samples if possible
- The app uses maximum 50 µL total volume


## Technical Details

### Technologies Used

- **Shiny**: Web application framework for R
- **bslib**: Modern Bootstrap themes
- **DT**: Interactive DataTables
- **readxl**: Excel file reading
- **openxlsx**: Excel file writing
- **shinyjs**: JavaScript integration

### Browser Compatibility

- Chrome (recommended)
- Firefox
- Safari
- Edge

### Performance

- Handles datasets with hundreds of samples efficiently
- Real-time calculations and table updates
- Responsive design works on desktop and tablet


## License

This project is licensed under the MIT License - feel free to use, modify, and distribute.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

### Suggested Improvements

- [ ] Add support for CSV files
- [ ] Include master mix calculations for multiple samples
- [ ] Add concentration dilution recommendations
- [ ] Support for different target RNA amounts
- [ ] Save/load custom volume adjustment rules
- [ ] Export to PDF format

## Support

For questions, issues, or feature requests:
- Open an issue on GitHub
- Email: your.email@example.com

## Version History

### v1.0.0 (2024)
- Initial release
- Automatic volume adjustment based on concentration ranges
- Excel upload/download functionality
- Print functionality
- Interactive tables with search and sort
- Modern, responsive UI

## Acknowledgments

- Built with R Shiny framework
- Designed for molecular biology laboratories
- Inspired by the need for accurate pipetting in cDNA synthesis protocols


## 📚 Citation

If you use this tool in your research, please cite:

```
cDNA Calculator (2024). Version 1.0.0.
Available at: https://github.com/markbarsoummarkarian/cdna-synthesis-calculator
```

---

**Made with ❤️ for the molecular biology community**
