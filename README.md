# cDNA Synthesis Calculator

**Interactive calculator for cDNA synthesis reaction setup**

> Designing a reverse transcription reaction should not require mental arithmetic. Enter your RNA concentration and volume, choose your kit, and get the exact volumes to pipette.

---

## What it does

- Takes RNA input quantity (ng) and concentration (ng/µL)
- Calculates water volume, buffer, enzyme, and primer volumes for your reaction
- Scales to your total reaction volume
- Supports common RT reaction formats

## How to run

Open the app folder and launch with R Shiny:

```r
shiny::runApp("cDNA Calculator/")
```

Or open `index.html` directly if a static version is available.

---

## Who it is for

Wet lab researchers setting up RT-qPCR experiments. Saves time, reduces pipetting errors.

**License:** MIT
