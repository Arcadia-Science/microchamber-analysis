# Microchamber analysis

This repo contains code for quantifying and comparing the movement of *Chlamydomonas reinhardtii* in 384 well plates and custom-developed microchambers. These analyses are included in the publication [Microchamber slide design for cell confinement during imaging](https://research.arcadiascience.com/pub/resource-microchamber-slide).

![Max_R5_24h_label](https://user-images.githubusercontent.com/64554648/184939172-52512740-18e8-43ba-8d1f-cdeebbbdb0f8.png)

## Repository contents
- `code/FIJI/` — ImageJ/Fiji macros for pre-processing raw timelapse movies (see [`code/FIJI/README.md`](code/FIJI/README.md)).
- `code/CellProfiler/` — CellProfiler pipelines that segment/track cells and export per-cell measurements (see [`code/CellProfiler/README.md`](code/CellProfiler/README.md)).
- `code/R/` — R notebook that analyzes the exported measurements and produces the figures (see [`code/R/README.md`](code/R/README.md)).

The full image-to-figure workflow is: **Fiji macro** (raw `.nd2` movies → processed frames) → **CellProfiler pipeline** (`chlamy_swim_track.cppipe`, tracks cells and exports `measurements_Cells.csv`) → **R notebook** (statistics and figures). The exported `measurements_Cells.csv.gz` is also archived on Zenodo, so the R analysis can be reproduced without rerunning the image-processing steps.

## Reproducing the R analysis
The R analysis lives in `code/R/analyzing_chlamydomonas_movement_384_vs_microchambers.ipynb` and can be run on its own from the published data.

1. Install **R 4.x** and **Jupyter** with the [IRkernel](https://irkernel.github.io/) so the notebook can run R cells.
2. Install the only R package dependency, `vioplot` (developed/tested with `vioplot` v0.3.7):

```r
install.packages("vioplot")
```

3. Download the input data, `measurements_Cells.csv.gz`, from Zenodo (DOI: [10.5281/zenodo.6999004](https://doi.org/10.5281/zenodo.6999004)). See [`code/R/README.md`](code/R/README.md) for the exact `curl` command.
4. Open the notebook in Jupyter and update the data path cell to point at the downloaded CSV, then run all cells.

## Associated timelapse image data 
The following Zenodo repositories contain image data associated with the ["Microchamber slide design for cell confinement during imaging"](https://research.arcadiascience.com/pub/resource-microchamber-slide) pub and the project to [dissect mechanisms of environmental adaptation in protists](https://research.arcadiascience.com/mechanisms-environmental-adaptation-protists).


*Colpoda steinii* cyst rotation. [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10151314.svg)](https://doi.org/10.5281/zenodo.10151314)

*Colpoda steinii* early encystment. [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10151874.svg)](https://doi.org/10.5281/zenodo.10151874)

*Colpoda steinii* in 384 well or microwells. [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10139789.svg)](https://doi.org/10.5281/zenodo.10139789)

*Colpoda steinii* reanimation experiment. [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10151222.svg)](https://doi.org/10.5281/zenodo.10151222)

*Tetrahymena rostrata* swimming. [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10138859.svg)](https://doi.org/10.5281/zenodo.10138859)

## Versions and platforms
*Fiji macro* was used with ImageJ2 Version: 2.3.0/1.53q Build: d544a3f481. *Cellprofiler pipeline* was run on CellProfiler version 5.

Computation was performed on an image analysis workstation with the following specifications:

Operating system: Windows 10 Pro Version 21H2 OS Build 19044.1889

| Component | Specification |
| --- | --- |
| Platform | Intel Xeon C621E EATX |
| Motherboard | Supermicro X12SPA-TF 64L |
| CPU | Intel Xeon W-3365 2.7GHz Thirty-Two Core 48MB 270W |
| RAM | 8 x DDR4-3200 64GB ECC Reg. |
| Video Card | NVIDIA RTX A6000 48GB PCI-E |
| Primary Hard Drive | Samsung 980 Pro 2TB Gen4 M.2 SSD |
| Secondary Hard Drive | Samsung 870 EVO 4TB SATA3 2.5inch SSD |
| Tertiary Hard Drive | Western Digital Ultrastar 18TB SATA3 |
| Case | Fractal Design Define 7 XL |
| Power Supply | Super Flower LEADEX Platinum 850W |
| Additional Cooling | Case Fans Upgrade Kit (PWM Ramping) |
