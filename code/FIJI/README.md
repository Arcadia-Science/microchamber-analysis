# Fiji / ImageJ macros

These ImageJ macros pre-process raw timelapse movies before quantification. They were run with **Fiji / ImageJ2 version 2.3.0/1.53q (build d544a3f481)** and require the **Bio-Formats** importer (bundled with Fiji) plus, for `colpoda_serieslabel_concatanate.ijm`, the **Series Labeler** plugin.

Run a macro from Fiji via `Plugins > Macros > Run...` and select the `.ijm` file.

## `batch_framesubtraction.ijm`
Prepares the *Chlamydomonas* swimming movies that feed the `chlamy_swim_track.cppipe` CellProfiler pipeline.

- **Inputs:** When run, the macro prompts for an *input directory*, an *output directory*, and a *file suffix* (default `.nd2`). It recursively scans the input directory for movies matching the suffix. Input paths are expected to contain a `raw` folder; the path segment after `raw/` is used to build matching output subfolders.
- **What it does:** For each movie it scales by 0.5, computes a standard-deviation Z-projection (to visualize swim tracks), and performs frame subtraction (frame *t* minus frame *t−11*) starting at frame 12.
- **Outputs:** Per input movie, creates `STD/`, `subtract/`, and `frames/` subfolders in the output directory containing 8-bit TIFFs. The `subtract/` TIFFs are the frame-subtracted images used as CellProfiler input.

## `colpoda_serieslabel_concatanate.ijm`
A figure/movie-annotation helper for *Colpoda* timelapse series (used for presentation rather than as input to the analysis pipeline).

- **Inputs:** Prompts for a directory and processes every `.tif` file in it.
- **What it does:** Adds time labels (hours and seconds, using the Series Labeler plugin) and a scale bar to each stack.
- **Outputs:** Saves an annotated copy of each image as `<basename>concat.tif` in the same directory.
