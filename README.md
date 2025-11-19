# cDNA Calculator

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![R](https://img.shields.io/badge/R-4.0%2B-brightgreen.svg)
![License](https://img.shields.io/badge/license-MIT-orange.svg)

A Shiny web application for automated calculation of RNA and DEPC water volumes for cDNA synthesis reactions.

## 🧬 Overview

The cDNA Calculator streamlines the preparation of cDNA synthesis reactions by automatically calculating optimal RNA and DEPC water volumes based on RNA concentrations. The application ensures pipetting accuracy by automatically scaling reactions when volumes fall outside safe pipetting ranges.

## ✨ Features

- **Automated Volume Calculations**: Calculates exact RNA and DEPC water volumes for 5 µg RNA per sample
- **Smart Volume Adjustment**: Automatically scales reactions to maintain pipetting accuracy (0.2-1.5 µL range)
- **Batch Processing**: Process multiple samples simultaneously via Excel upload
- **Interactive Tables**: Sortable, searchable data tables with formatting
- **Print Functionality**: Generate printer-friendly reports for lab notebooks
- **Excel Export**: Download calculations in Excel format with multiple sheets
- **Modern UI**: Clean, responsive interface with gradient design elements

## 📋 Prerequisites

- R (version 4.0 or higher)
- RStudio (recommended)

### Required R Packages

The application will automatically install missing packages on first run:


### Example Input File

```
SampleNumber    RNA_Concentration
Sample-1        250.0
Sample-2        125.5
Sample-3        500.0
Sample-4        75.3
```

**Note**: If your file contains a `SampleName` column, it will be automatically removed during processing.

## 🔬 Calculation Method

### Basic Formula

For each sample, the application calculates:

```
RNA Volume (µL) = (5 µg ÷ RNA Concentration) × 10
DEPC Water (µL) = Total Volume - RNA Volume
```

### Volume Adjustment Logic

**Normal Range (0.2-1.5 µL)**
- No adjustment needed
- Standard 10 µL total volume

**Below Range (< 0.2 µL)**
- RNA volume set to 0.2 µL (minimum pipettable)
- Total volume scaled up proportionally
- Example: 0.1 µL → 0.2 µL means 2× scaling → 20 µL total

**Above Range (> 1.5 µL)**
- RNA volume set to 1.5 µL (maximum recommended)
- Total volume scaled down proportionally
- Example: 2.0 µL → 1.5 µL means 0.75× scaling → 7.5 µL total

## 📖 Usage Guide

### Step 1: Prepare Your Data
Create an Excel file with `SampleNumber` and `RNA_Concentration` columns.

### Step 2: Upload File
1. Click the "Browse..." button
2. Select your .xlsx file
3. Wait for confirmation message

### Step 3: Review Results
- Check the **Sample Calculations** table for volumes
- Note any samples with adjustments (scaled up/down)
- Review the **cDNA Synthesis Reaction Volumes** reference table

### Step 4: Export Results
- **Print**: Click "Print Tables" to generate a printable report
- **Download**: Click "Download Results" to save as Excel

## 📐 Output Tables

### Sample Calculations Table

| Column | Description |
|--------|-------------|
| SampleNumber | Sample identifier |
| RNA_Concentration | Input RNA concentration (µg/µL) |
| RNA_Volume | Calculated RNA volume to use (µL) |
| DEPC_Volume | DEPC water volume to add (µL) |
| Total_Volume | Total reaction volume (µL) |
| Adjustment | Scaling status (Normal/Scaled up/Scaled down) |

### Reaction Volumes Table

Standard cDNA synthesis master mix (per 10 µL reaction):

| Component | Volume (µL) |
|-----------|-------------|
| 5× SYBR RT Mix | 2.0 |
| 10× Reverse Transcriptase | 1.0 |
| Unispike | 0.5 |
| Nuclease-free water | 4.5 |
| RNA | 2.0 |
| **Total** | **10.0** |

## 🎨 User Interface

### Sidebar
- File upload widget
- Print button with modern gradient styling
- Excel download button

### Main Panel
- Interactive sample calculations table
- Standard reaction components reference
- Real-time data filtering and sorting

## ⚙️ Configuration

### Modify Volume Constraints

Edit these values in the server logic:

```r
# Minimum RNA volume (µL)
min_volume <- 0.2

# Maximum RNA volume (µL)
max_volume <- 1.5

# Target RNA amount (µg)
target_rna <- 5
```

### Customize Theme

Modify the `bs_theme()` settings:

```r
theme <- bs_theme(
  version = 5,
  bg = "#ffffff",        # Background color
  fg = "#2c3e50",        # Foreground color
  primary = "#3498db",   # Primary accent color
  base_font = font_google("Inter")
)
```


## 📝 Example Workflow

```r
# 1. Launch the app
shiny::runApp()

# 2. Upload your Excel file with samples

# 3. Review calculations
#    Sample-1: 250 µg/µL → 0.2 µL RNA + 9.8 µL DEPC (Normal)
#    Sample-2: 500 µg/µL → 0.2 µL RNA + 19.8 µL DEPC (Scaled up)
#    Sample-3: 50 µg/µL → 1.5 µL RNA + 4.5 µL DEPC (Scaled down)

# 4. Download or print results for lab use
```

## 🔬 Scientific Background

### Why 5 µg RNA?
This is the standard input amount for most cDNA synthesis kits, providing optimal balance between:
- Sufficient template for downstream applications
- Avoiding reaction saturation
- Maintaining cost-effectiveness

### Why Volume Constraints?
- **Pipetting accuracy**: Most pipettes are inaccurate below 0.5 µL
- **Reproducibility**: Larger volumes reduce percentage error
- **Practical handling**: Very small volumes are difficult to visualize

### DEPC Water
DEPC (Diethyl pyrocarbonate) treatment inactivates RNases, protecting RNA samples from degradation during preparation.

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.


## 🙏 Acknowledgments

- Built with [Shiny](https://shiny.rstudio.com/) by RStudio
- UI components from [bslib](https://rstudio.github.io/bslib/)
- Icons from [Font Awesome](https://fontawesome.com/)

## 📚 Citation

If you use this tool in your research, please cite:

```
cDNA Calculator (2024). Version 1.0.0.
Available at: https://github.com/markbarsoummarkarian/cdna-calculator
```

---

**Made with ❤️ for the molecular biology community**
