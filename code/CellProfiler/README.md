# CellProfiler pipelines

These pipelines segment and track cells in the pre-processed timelapse images and export per-cell measurements. They were run with **CellProfiler version 5**.

To run a pipeline: open CellProfiler, choose `File > Open Project...` (or drag the `.cppipe` onto the window), drag the input images into the **Images** module file list, set the **Default Output Folder**, and click **Analyze Images**.

## `chlamy_swim_track.cppipe`
Tracks swimming *Chlamydomonas reinhardtii* and produces the measurements used by the R analysis.

- **Inputs:** The frame-subtracted 8-bit TIFFs produced by `code/FIJI/batch_framesubtraction.ijm` (the macro's `subtract/` output). The pipeline's NamesAndTypes rule selects files whose path/name contains `subtract`. Metadata (Sample, Well, hour) is extracted from the folder/file names, so keep the macro's output folder structure intact.
- **What it does:** rescales intensity, identifies primary objects (cells), tracks objects across frames (`TrackObjects`), and saves overlay/label images.
- **Outputs:** Exports comma-delimited per-object measurement tables to the Default Output Folder with the prefix `measurements_`. The cells table is `measurements_Cells.csv` — this is the file the R notebook reads (archived gzip-compressed as `measurements_Cells.csv.gz` on Zenodo, DOI [10.5281/zenodo.6999004](https://doi.org/10.5281/zenodo.6999004)).

## `colpoda_segment_cells.cppipe`
Segments *Colpoda steinii* cells (used for the *Colpoda* datasets rather than the *Chlamydomonas* swim-track analysis).

- **Inputs:** Color/RGB images of *Colpoda*; metadata (including `chamber`) is extracted from file names.
- **What it does:** converts color channels to grayscale, identifies primary objects, overlays outlines, and measures object size/shape.
- **Outputs:** Exports object measurements to the Default Output Folder (filename prefix `microchamber`) and saves outline/overlay images.
