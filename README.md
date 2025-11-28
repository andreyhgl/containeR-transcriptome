[![R](https://img.shields.io/badge/-script-276DC3.svg?style=flat&logo=R)](https://cran.r-project.org)
[![run with singularity](https://img.shields.io/badge/run%20with-singularity-1d355c.svg?labelColor=000000)](https://sylabs.io/docs/)

# README

Singularity image with pre-installed libraries for running RNA-seq analysis in [`R`](https://www.r-project.org/).

The included libraries:

#### Visualisation

+ ggplot2
+ ggrepel
+ ggvenn
+ ggsignif
+ cowplot
+ RColorBrewer
+ patchwork
+ ComplexHeatmap
+ [gt](https://gt.rstudio.com/reference/index.html)

#### Differential gene expression analysis

+ edgeR
+ DESeq2

#### Gene and genome annotation

+ [clusterProfiler](https://www.bioconductor.org/packages/release/bioc/html/clusterProfiler.html)
+ [ReactomePA](https://bioconductor.org/packages/release/bioc/html/ReactomePA.html)
+ biomaRt
+ [org.Mm.eg.db](https://bioconductor.org/packages/release/data/annotation/html/org.Mm.eg.db.html)
+ [org.Hs.eg.db](https://bioconductor.org/packages/release/data/annotation/html/org.Hs.eg.db.html)
+ tximport

#### Utility

+ gtools
+ tools
+ scales
+ data.table
+ forcats
+ openxlsx
+ readr
+ dplyr
+ reshape2 (included with other packages)

## Build

Use the definition file to build locally:

```sh
apptainer build RNAseq.sif RNAseq.def
```

> [!TIP]
> Use a non-interactive install by adding `-y`
>
> ```sh
> %post
>   apt-get update
>
>   # Install less and qpdf
>   apt-get install -y less
>   apt-get install -y qpdf
> ```

## Deploy

Pre-build image can be downloaded from the [Cloud Library](https://cloud.sylabs.io/library):

```sh
apptainer pull library://andreyhgl/singularity-r/rnaseq:latest
```

> [!TIP]
> If apptainer/singularity is not working, try [adding the remote host manually](https://apptainer.org/docs/user/latest/endpoint.html#restoring-pre-apptainer-library-behavior)
>
> ```sh
> # list the remote URI
> singuliarty remote list
>
> # add singularity cloud URI
> apptainer remote add --no-login SylabsCloud cloud.sycloud.io
> ```

## Execute scripts

In order to fully utilise the singularity image make sure a shebang is included in the script file `#!/usr/bin/env Rscript`.

```R
#!/usr/bin/env Rscript

suppressPackageStartupMessages({
  library(edgeR)
  library(gtools)
})

...

```

Also make the script file executable. 

```sh
chmod +x script-file.R
```

The singularity image expects a script file on `exec`.

```sh
apptainer exec library://andreyhgl/singularity-r/rnaseq:latest script-file.R
```
