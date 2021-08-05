cola Report for Hierarchical Partitioning - 'TCGA_KICH_methylation'
==================

**Date**: 2021-07-22 15:45:06 CEST, **cola version**: 1.9.4

----------------------------------------------------------------

<style type='text/css'>

body, td, th {
   font-family: Arial,Helvetica,sans-serif;
   background-color: white;
   font-size: 13px;
  max-width: 800px;
  margin: auto;
  margin-left:210px;
  padding: 0px 10px 0px 10px;
  border-left: 1px solid #EEEEEE;
  line-height: 150%;
}

tt, code, pre {
   font-family: 'DejaVu Sans Mono', 'Droid Sans Mono', 'Lucida Console', Consolas, Monaco, 

monospace;
}

h1 {
   font-size:2.2em;
}

h2 {
   font-size:1.8em;
}

h3 {
   font-size:1.4em;
}

h4 {
   font-size:1.0em;
}

h5 {
   font-size:0.9em;
}

h6 {
   font-size:0.8em;
}

a {
  text-decoration: none;
  color: #0366d6;
}

a:hover {
  text-decoration: underline;
}

a:visited {
   color: #0366d6;
}

pre, img {
  max-width: 100%;
}
pre {
  overflow-x: auto;
}
pre code {
   display: block; padding: 0.5em;
}

code {
  font-size: 92%;
  border: 1px solid #ccc;
}

code[class] {
  background-color: #F8F8F8;
}

table, td, th {
  border: 1px solid #ccc;
}

blockquote {
   color:#666666;
   margin:0;
   padding-left: 1em;
   border-left: 0.5em #EEE solid;
}

hr {
   height: 0px;
   border-bottom: none;
   border-top-width: thin;
   border-top-style: dotted;
   border-top-color: #999999;
}

@media print {
   * {
      background: transparent !important;
      color: black !important;
      filter:none !important;
      -ms-filter: none !important;
   }

   body {
      font-size:12pt;
      max-width:100%;
   }

   a, a:visited {
      text-decoration: underline;
   }

   hr {
      visibility: hidden;
      page-break-before: always;
   }

   pre, blockquote {
      padding-right: 1em;
      page-break-inside: avoid;
   }

   tr, img {
      page-break-inside: avoid;
   }

   img {
      max-width: 100% !important;
   }

   @page :left {
      margin: 15mm 20mm 15mm 10mm;
   }

   @page :right {
      margin: 15mm 10mm 15mm 20mm;
   }

   p, h2, h3 {
      orphans: 3; widows: 3;
   }

   h2, h3 {
      page-break-after: avoid;
   }
}
</style>




## Summary



First the variable is renamed to `res_rh`.


```r
res_rh = rh
```



The partition hierarchy and all available functions which can be applied to `res_rh` object.


```r
res_rh
```

```
#> A 'HierarchicalPartition' object with 4 combinations of top-value methods and partitioning methods.
#>   On a matrix with 375860 rows and 66 columns.
#>   Performed in total 15400 partitions.
#>   There are 8 groups under the following parameters:
#>     - min_samples: 6
#>     - mean_silhouette_cutoff: 0.9
#>     - min_n_signatures: 1000 (signatures are selected based on:)
#>       - fdr_cutoff: 0.05
#>       - group_diff: 0.25
#> 
#> Hierarchy of the partition:
#>   0, 66 cols
#>   |-- 01, 8 cols (b)
#>   |-- 02, 45 cols, 9467 signatures
#>   |   |-- 021, 8 cols (b)
#>   |   |-- 022, 22 cols, 1384 signatures
#>   |   |   |-- 0221, 10 cols (b)
#>   |   |   |-- 0222, 7 cols (b)
#>   |   |   |-- 0223, 3 cols (b)
#>   |   |   `-- 0224, 2 cols (b)
#>   |   `-- 023, 15 cols, 335 signatures (c)
#>   `-- 03, 13 cols, 580 signatures (c)
#> Stop reason:
#>   b) Subgroup had too few columns.
#>   c) There were too few signatures.
#> 
#> Following methods can be applied to this 'HierarchicalPartition' object:
#>  [1] "all_leaves"            "all_nodes"             "cola_report"           "collect_classes"      
#>  [5] "colnames"              "compare_signatures"    "dimension_reduction"   "functional_enrichment"
#>  [9] "get_anno_col"          "get_anno"              "get_children_nodes"    "get_classes"          
#> [13] "get_matrix"            "get_signatures"        "is_leaf_node"          "max_depth"            
#> [17] "merge_node"            "ncol"                  "node_info"             "node_level"           
#> [21] "nrow"                  "rownames"              "show"                  "split_node"           
#> [25] "suggest_best_k"        "test_to_known_factors" "top_rows_heatmap"      "top_rows_overlap"     
#> 
#> You can get result for a single node by e.g. object["01"]
```

The call of `hierarchical_partition()` was:


```
#> hierarchical_partition(data = mat, top_n = 1000, top_value_method = c("SD", "ATC"), 
#>     partition_method = c("kmeans", "skmeans"), subset = 500, group_diff = 0.25, min_n_signatures = 1000, 
#>     filter_fun = function(mat) {
#>         s = rowSds(mat)
#>         order(-s)[1:30000]
#>     }, max_k = 8, scale_rows = FALSE, cores = 4)
```

Dimension of the input matrix:


```r
mat = get_matrix(res_rh)
dim(mat)
```

```
#> [1] 375860     66
```

All the methods that were tried:


```r
res_rh@param$combination_method
```

```
#> [[1]]
#> [1] "SD"     "kmeans"
#> 
#> [[2]]
#> [1] "ATC"    "kmeans"
#> 
#> [[3]]
#> [1] "SD"      "skmeans"
#> 
#> [[4]]
#> [1] "ATC"     "skmeans"
```

### Density distribution

The density distribution for each sample is visualized as one column in the following heatmap.
The clustering is based on the distance which is the Kolmogorov-Smirnov statistic between two distributions.




```r
library(ComplexHeatmap)
densityHeatmap(mat, ylab = "value", cluster_columns = TRUE, show_column_names = FALSE,
    mc.cores = 1)
```

![plot of chunk density-heatmap](figure_cola/density-heatmap-1.png)



Some values about the hierarchy:


```r
all_nodes(res_rh)
```

```
#>  [1] "0"    "01"   "02"   "021"  "022"  "0221" "0222" "0223" "0224" "023"  "03"
```

```r
all_leaves(res_rh)
```

```
#> [1] "01"   "021"  "0221" "0222" "0223" "0224" "023"  "03"
```

```r
node_info(res_rh)
```

```
#>      id best_method depth best_k n_columns n_signatures p_signatures is_leaf
#> 1     0 ATC:skmeans     1      3        66         9645     0.025661   FALSE
#> 2    01 not applied     2     NA         8           NA           NA    TRUE
#> 3    02  ATC:kmeans     2      3        45         9467     0.025188   FALSE
#> 4   021 not applied     3     NA         8           NA           NA    TRUE
#> 5   022 ATC:skmeans     3      4        22         1384     0.003682   FALSE
#> 6  0221 not applied     4     NA        10           NA           NA    TRUE
#> 7  0222 not applied     4     NA         7           NA           NA    TRUE
#> 8  0223 not applied     4     NA         3           NA           NA    TRUE
#> 9  0224 not applied     4     NA         2           NA           NA    TRUE
#> 10  023  ATC:kmeans     3      2        15          335     0.000891    TRUE
#> 11   03 ATC:skmeans     2      2        13          580     0.001543    TRUE
```

In the output from `node_info()`, there are the following columns:

- `id`: The node id.
- `best_method`: The best method selected.
- `depth`: Depth of the node in the hierarchy.
- `best_k`: Best number of groups of the partition on that node.
- `n_columns`: Number of columns in the submatrix.
- `n_signatures`: Number of signatures with the `best_k`.
- `p_signatures`: Proportion of hte signatures in total number of rows in the matrix.
- `is_leaf`: Whether the node is a leaf.

Labels of nodes are encoded in a special way. The number of digits
correspond to the depth of the node in the hierarchy and the value of the
digits correspond to the index of the subgroup in the current node, E.g. a label
of “012” means the node is the second subgroup of the partition which is the
first subgroup of the root node.

### Suggest the best k



Following table shows the best `k` (number of partitions) for each node in the
partition hierarchy. Clicking on the node name in the table goes to the
corresponding section for the partitioning on that node.

[The cola vignette](https://jokergoo.github.io/cola_vignettes/cola.html#toc_13)
explains the definition of the metrics used for determining the best
number of partitions.



```r
suggest_best_k(res_rh)
```


|Node                |Best method                                         |Is leaf   |Best k |1-PAC |Mean silhouette |Concordance | #samples|   |
|:-------------------|:---------------------------------------------------|:---------|:------|:-----|:---------------|:-----------|--------:|:--|
|[Node0](#Node0)     |ATC:skmeans                                         |          |3      |1.00  |1.00            |1.00        |       66|** |
|Node01-leaf         |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |        8|   |
|[Node02](#Node02)   |ATC:kmeans                                          |          |3      |1.00  |0.98            |0.99        |       45|** |
|Node021-leaf        |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |        8|   |
|[Node022](#Node022) |ATC:skmeans                                         |          |4      |1.00  |0.99            |1.00        |       22|** |
|Node0221-leaf       |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |       10|   |
|Node0222-leaf       |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |        7|   |
|Node0223-leaf       |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |        3|   |
|Node0224-leaf       |<span style='color:grey;'><i>not applied</i></span> |✓ (b)     |       |      |                |            |        2|   |
|Node023-leaf        |ATC:kmeans                                          |✓ (&#99;) |2      |1.00  |1.00            |1.00        |       15|** |
|Node03-leaf         |ATC:skmeans                                         |✓ (&#99;) |2      |1.00  |1.00            |1.00        |       13|** |


Stop reason: b) Subgroup had too few columns. c) There were too few signatures. 

\*\*: 1-PAC > 0.95, \*: 1-PAC > 0.9


### Partition hierarchy

The nodes of the hierarchy can be merged by setting the `merge_node` parameters. Here we 
control the hierarchy with the `min_n_signatures` parameter. The value of `min_n_signatures` is
from `node_info()`.





<style type='text/css'>



.ui-helper-hidden {
	display: none;
}
.ui-helper-hidden-accessible {
	border: 0;
	clip: rect(0 0 0 0);
	height: 1px;
	margin: -1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	width: 1px;
}
.ui-helper-reset {
	margin: 0;
	padding: 0;
	border: 0;
	outline: 0;
	line-height: 1.3;
	text-decoration: none;
	font-size: 100%;
	list-style: none;
}
.ui-helper-clearfix:before,
.ui-helper-clearfix:after {
	content: "";
	display: table;
	border-collapse: collapse;
}
.ui-helper-clearfix:after {
	clear: both;
}
.ui-helper-zfix {
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	position: absolute;
	opacity: 0;
	filter:Alpha(Opacity=0); 
}

.ui-front {
	z-index: 100;
}



.ui-state-disabled {
	cursor: default !important;
	pointer-events: none;
}



.ui-icon {
	display: inline-block;
	vertical-align: middle;
	margin-top: -.25em;
	position: relative;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
}

.ui-widget-icon-block {
	left: 50%;
	margin-left: -8px;
	display: block;
}




.ui-widget-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
.ui-accordion .ui-accordion-header {
	display: block;
	cursor: pointer;
	position: relative;
	margin: 2px 0 0 0;
	padding: .5em .5em .5em .7em;
	font-size: 100%;
}
.ui-accordion .ui-accordion-content {
	padding: 1em 2.2em;
	border-top: 0;
	overflow: auto;
}
.ui-autocomplete {
	position: absolute;
	top: 0;
	left: 0;
	cursor: default;
}
.ui-menu {
	list-style: none;
	padding: 0;
	margin: 0;
	display: block;
	outline: 0;
}
.ui-menu .ui-menu {
	position: absolute;
}
.ui-menu .ui-menu-item {
	margin: 0;
	cursor: pointer;
	
	list-style-image: url("data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7");
}
.ui-menu .ui-menu-item-wrapper {
	position: relative;
	padding: 3px 1em 3px .4em;
}
.ui-menu .ui-menu-divider {
	margin: 5px 0;
	height: 0;
	font-size: 0;
	line-height: 0;
	border-width: 1px 0 0 0;
}
.ui-menu .ui-state-focus,
.ui-menu .ui-state-active {
	margin: -1px;
}


.ui-menu-icons {
	position: relative;
}
.ui-menu-icons .ui-menu-item-wrapper {
	padding-left: 2em;
}


.ui-menu .ui-icon {
	position: absolute;
	top: 0;
	bottom: 0;
	left: .2em;
	margin: auto 0;
}


.ui-menu .ui-menu-icon {
	left: auto;
	right: 0;
}
.ui-button {
	padding: .4em 1em;
	display: inline-block;
	position: relative;
	line-height: normal;
	margin-right: .1em;
	cursor: pointer;
	vertical-align: middle;
	text-align: center;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;

	
	overflow: visible;
}

.ui-button,
.ui-button:link,
.ui-button:visited,
.ui-button:hover,
.ui-button:active {
	text-decoration: none;
}


.ui-button-icon-only {
	width: 2em;
	box-sizing: border-box;
	text-indent: -9999px;
	white-space: nowrap;
}


input.ui-button.ui-button-icon-only {
	text-indent: 0;
}


.ui-button-icon-only .ui-icon {
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -8px;
	margin-left: -8px;
}

.ui-button.ui-icon-notext .ui-icon {
	padding: 0;
	width: 2.1em;
	height: 2.1em;
	text-indent: -9999px;
	white-space: nowrap;

}

input.ui-button.ui-icon-notext .ui-icon {
	width: auto;
	height: auto;
	text-indent: 0;
	white-space: normal;
	padding: .4em 1em;
}



input.ui-button::-moz-focus-inner,
button.ui-button::-moz-focus-inner {
	border: 0;
	padding: 0;
}
.ui-controlgroup {
	vertical-align: middle;
	display: inline-block;
}
.ui-controlgroup > .ui-controlgroup-item {
	float: left;
	margin-left: 0;
	margin-right: 0;
}
.ui-controlgroup > .ui-controlgroup-item:focus,
.ui-controlgroup > .ui-controlgroup-item.ui-visual-focus {
	z-index: 9999;
}
.ui-controlgroup-vertical > .ui-controlgroup-item {
	display: block;
	float: none;
	width: 100%;
	margin-top: 0;
	margin-bottom: 0;
	text-align: left;
}
.ui-controlgroup-vertical .ui-controlgroup-item {
	box-sizing: border-box;
}
.ui-controlgroup .ui-controlgroup-label {
	padding: .4em 1em;
}
.ui-controlgroup .ui-controlgroup-label span {
	font-size: 80%;
}
.ui-controlgroup-horizontal .ui-controlgroup-label + .ui-controlgroup-item {
	border-left: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label + .ui-controlgroup-item {
	border-top: none;
}
.ui-controlgroup-horizontal .ui-controlgroup-label.ui-widget-content {
	border-right: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label.ui-widget-content {
	border-bottom: none;
}


.ui-controlgroup-vertical .ui-spinner-input {

	
	width: 75%;
	width: calc( 100% - 2.4em );
}
.ui-controlgroup-vertical .ui-spinner .ui-spinner-up {
	border-top-style: solid;
}

.ui-checkboxradio-label .ui-icon-background {
	box-shadow: inset 1px 1px 1px #ccc;
	border-radius: .12em;
	border: none;
}
.ui-checkboxradio-radio-label .ui-icon-background {
	width: 16px;
	height: 16px;
	border-radius: 1em;
	overflow: visible;
	border: none;
}
.ui-checkboxradio-radio-label.ui-checkboxradio-checked .ui-icon,
.ui-checkboxradio-radio-label.ui-checkboxradio-checked:hover .ui-icon {
	background-image: none;
	width: 8px;
	height: 8px;
	border-width: 4px;
	border-style: solid;
}
.ui-checkboxradio-disabled {
	pointer-events: none;
}
.ui-datepicker {
	width: 17em;
	padding: .2em .2em 0;
	display: none;
}
.ui-datepicker .ui-datepicker-header {
	position: relative;
	padding: .2em 0;
}
.ui-datepicker .ui-datepicker-prev,
.ui-datepicker .ui-datepicker-next {
	position: absolute;
	top: 2px;
	width: 1.8em;
	height: 1.8em;
}
.ui-datepicker .ui-datepicker-prev-hover,
.ui-datepicker .ui-datepicker-next-hover {
	top: 1px;
}
.ui-datepicker .ui-datepicker-prev {
	left: 2px;
}
.ui-datepicker .ui-datepicker-next {
	right: 2px;
}
.ui-datepicker .ui-datepicker-prev-hover {
	left: 1px;
}
.ui-datepicker .ui-datepicker-next-hover {
	right: 1px;
}
.ui-datepicker .ui-datepicker-prev span,
.ui-datepicker .ui-datepicker-next span {
	display: block;
	position: absolute;
	left: 50%;
	margin-left: -8px;
	top: 50%;
	margin-top: -8px;
}
.ui-datepicker .ui-datepicker-title {
	margin: 0 2.3em;
	line-height: 1.8em;
	text-align: center;
}
.ui-datepicker .ui-datepicker-title select {
	font-size: 1em;
	margin: 1px 0;
}
.ui-datepicker select.ui-datepicker-month,
.ui-datepicker select.ui-datepicker-year {
	width: 45%;
}
.ui-datepicker table {
	width: 100%;
	font-size: .9em;
	border-collapse: collapse;
	margin: 0 0 .4em;
}
.ui-datepicker th {
	padding: .7em .3em;
	text-align: center;
	font-weight: bold;
	border: 0;
}
.ui-datepicker td {
	border: 0;
	padding: 1px;
}
.ui-datepicker td span,
.ui-datepicker td a {
	display: block;
	padding: .2em;
	text-align: right;
	text-decoration: none;
}
.ui-datepicker .ui-datepicker-buttonpane {
	background-image: none;
	margin: .7em 0 0 0;
	padding: 0 .2em;
	border-left: 0;
	border-right: 0;
	border-bottom: 0;
}
.ui-datepicker .ui-datepicker-buttonpane button {
	float: right;
	margin: .5em .2em .4em;
	cursor: pointer;
	padding: .2em .6em .3em .6em;
	width: auto;
	overflow: visible;
}
.ui-datepicker .ui-datepicker-buttonpane button.ui-datepicker-current {
	float: left;
}


.ui-datepicker.ui-datepicker-multi {
	width: auto;
}
.ui-datepicker-multi .ui-datepicker-group {
	float: left;
}
.ui-datepicker-multi .ui-datepicker-group table {
	width: 95%;
	margin: 0 auto .4em;
}
.ui-datepicker-multi-2 .ui-datepicker-group {
	width: 50%;
}
.ui-datepicker-multi-3 .ui-datepicker-group {
	width: 33.3%;
}
.ui-datepicker-multi-4 .ui-datepicker-group {
	width: 25%;
}
.ui-datepicker-multi .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-multi .ui-datepicker-group-middle .ui-datepicker-header {
	border-left-width: 0;
}
.ui-datepicker-multi .ui-datepicker-buttonpane {
	clear: left;
}
.ui-datepicker-row-break {
	clear: both;
	width: 100%;
	font-size: 0;
}


.ui-datepicker-rtl {
	direction: rtl;
}
.ui-datepicker-rtl .ui-datepicker-prev {
	right: 2px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next {
	left: 2px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-prev:hover {
	right: 1px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next:hover {
	left: 1px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane {
	clear: right;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button {
	float: left;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button.ui-datepicker-current,
.ui-datepicker-rtl .ui-datepicker-group {
	float: right;
}
.ui-datepicker-rtl .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-rtl .ui-datepicker-group-middle .ui-datepicker-header {
	border-right-width: 0;
	border-left-width: 1px;
}


.ui-datepicker .ui-icon {
	display: block;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
	left: .5em;
	top: .3em;
}
.ui-dialog {
	position: absolute;
	top: 0;
	left: 0;
	padding: .2em;
	outline: 0;
}
.ui-dialog .ui-dialog-titlebar {
	padding: .4em 1em;
	position: relative;
}
.ui-dialog .ui-dialog-title {
	float: left;
	margin: .1em 0;
	white-space: nowrap;
	width: 90%;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-dialog .ui-dialog-titlebar-close {
	position: absolute;
	right: .3em;
	top: 50%;
	width: 20px;
	margin: -10px 0 0 0;
	padding: 1px;
	height: 20px;
}
.ui-dialog .ui-dialog-content {
	position: relative;
	border: 0;
	padding: .5em 1em;
	background: none;
	overflow: auto;
}
.ui-dialog .ui-dialog-buttonpane {
	text-align: left;
	border-width: 1px 0 0 0;
	background-image: none;
	margin-top: .5em;
	padding: .3em 1em .5em .4em;
}
.ui-dialog .ui-dialog-buttonpane .ui-dialog-buttonset {
	float: right;
}
.ui-dialog .ui-dialog-buttonpane button {
	margin: .5em .4em .5em 0;
	cursor: pointer;
}
.ui-dialog .ui-resizable-n {
	height: 2px;
	top: 0;
}
.ui-dialog .ui-resizable-e {
	width: 2px;
	right: 0;
}
.ui-dialog .ui-resizable-s {
	height: 2px;
	bottom: 0;
}
.ui-dialog .ui-resizable-w {
	width: 2px;
	left: 0;
}
.ui-dialog .ui-resizable-se,
.ui-dialog .ui-resizable-sw,
.ui-dialog .ui-resizable-ne,
.ui-dialog .ui-resizable-nw {
	width: 7px;
	height: 7px;
}
.ui-dialog .ui-resizable-se {
	right: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-sw {
	left: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-ne {
	right: 0;
	top: 0;
}
.ui-dialog .ui-resizable-nw {
	left: 0;
	top: 0;
}
.ui-draggable .ui-dialog-titlebar {
	cursor: move;
}
.ui-draggable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable {
	position: relative;
}
.ui-resizable-handle {
	position: absolute;
	font-size: 0.1px;
	display: block;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable-disabled .ui-resizable-handle,
.ui-resizable-autohide .ui-resizable-handle {
	display: none;
}
.ui-resizable-n {
	cursor: n-resize;
	height: 7px;
	width: 100%;
	top: -5px;
	left: 0;
}
.ui-resizable-s {
	cursor: s-resize;
	height: 7px;
	width: 100%;
	bottom: -5px;
	left: 0;
}
.ui-resizable-e {
	cursor: e-resize;
	width: 7px;
	right: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-w {
	cursor: w-resize;
	width: 7px;
	left: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-se {
	cursor: se-resize;
	width: 12px;
	height: 12px;
	right: 1px;
	bottom: 1px;
}
.ui-resizable-sw {
	cursor: sw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	bottom: -5px;
}
.ui-resizable-nw {
	cursor: nw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	top: -5px;
}
.ui-resizable-ne {
	cursor: ne-resize;
	width: 9px;
	height: 9px;
	right: -5px;
	top: -5px;
}
.ui-progressbar {
	height: 2em;
	text-align: left;
	overflow: hidden;
}
.ui-progressbar .ui-progressbar-value {
	margin: -1px;
	height: 100%;
}
.ui-progressbar .ui-progressbar-overlay {
	background: url("data:image/gif;base64,R0lGODlhKAAoAIABAAAAAP///yH/C05FVFNDQVBFMi4wAwEAAAAh+QQJAQABACwAAAAAKAAoAAACkYwNqXrdC52DS06a7MFZI+4FHBCKoDeWKXqymPqGqxvJrXZbMx7Ttc+w9XgU2FB3lOyQRWET2IFGiU9m1frDVpxZZc6bfHwv4c1YXP6k1Vdy292Fb6UkuvFtXpvWSzA+HycXJHUXiGYIiMg2R6W459gnWGfHNdjIqDWVqemH2ekpObkpOlppWUqZiqr6edqqWQAAIfkECQEAAQAsAAAAACgAKAAAApSMgZnGfaqcg1E2uuzDmmHUBR8Qil95hiPKqWn3aqtLsS18y7G1SzNeowWBENtQd+T1JktP05nzPTdJZlR6vUxNWWjV+vUWhWNkWFwxl9VpZRedYcflIOLafaa28XdsH/ynlcc1uPVDZxQIR0K25+cICCmoqCe5mGhZOfeYSUh5yJcJyrkZWWpaR8doJ2o4NYq62lAAACH5BAkBAAEALAAAAAAoACgAAAKVDI4Yy22ZnINRNqosw0Bv7i1gyHUkFj7oSaWlu3ovC8GxNso5fluz3qLVhBVeT/Lz7ZTHyxL5dDalQWPVOsQWtRnuwXaFTj9jVVh8pma9JjZ4zYSj5ZOyma7uuolffh+IR5aW97cHuBUXKGKXlKjn+DiHWMcYJah4N0lYCMlJOXipGRr5qdgoSTrqWSq6WFl2ypoaUAAAIfkECQEAAQAsAAAAACgAKAAAApaEb6HLgd/iO7FNWtcFWe+ufODGjRfoiJ2akShbueb0wtI50zm02pbvwfWEMWBQ1zKGlLIhskiEPm9R6vRXxV4ZzWT2yHOGpWMyorblKlNp8HmHEb/lCXjcW7bmtXP8Xt229OVWR1fod2eWqNfHuMjXCPkIGNileOiImVmCOEmoSfn3yXlJWmoHGhqp6ilYuWYpmTqKUgAAIfkECQEAAQAsAAAAACgAKAAAApiEH6kb58biQ3FNWtMFWW3eNVcojuFGfqnZqSebuS06w5V80/X02pKe8zFwP6EFWOT1lDFk8rGERh1TTNOocQ61Hm4Xm2VexUHpzjymViHrFbiELsefVrn6XKfnt2Q9G/+Xdie499XHd2g4h7ioOGhXGJboGAnXSBnoBwKYyfioubZJ2Hn0RuRZaflZOil56Zp6iioKSXpUAAAh+QQJAQABACwAAAAAKAAoAAACkoQRqRvnxuI7kU1a1UU5bd5tnSeOZXhmn5lWK3qNTWvRdQxP8qvaC+/yaYQzXO7BMvaUEmJRd3TsiMAgswmNYrSgZdYrTX6tSHGZO73ezuAw2uxuQ+BbeZfMxsexY35+/Qe4J1inV0g4x3WHuMhIl2jXOKT2Q+VU5fgoSUI52VfZyfkJGkha6jmY+aaYdirq+lQAACH5BAkBAAEALAAAAAAoACgAAAKWBIKpYe0L3YNKToqswUlvznigd4wiR4KhZrKt9Upqip61i9E3vMvxRdHlbEFiEXfk9YARYxOZZD6VQ2pUunBmtRXo1Lf8hMVVcNl8JafV38aM2/Fu5V16Bn63r6xt97j09+MXSFi4BniGFae3hzbH9+hYBzkpuUh5aZmHuanZOZgIuvbGiNeomCnaxxap2upaCZsq+1kAACH5BAkBAAEALAAAAAAoACgAAAKXjI8By5zf4kOxTVrXNVlv1X0d8IGZGKLnNpYtm8Lr9cqVeuOSvfOW79D9aDHizNhDJidFZhNydEahOaDH6nomtJjp1tutKoNWkvA6JqfRVLHU/QUfau9l2x7G54d1fl995xcIGAdXqMfBNadoYrhH+Mg2KBlpVpbluCiXmMnZ2Sh4GBqJ+ckIOqqJ6LmKSllZmsoq6wpQAAAh+QQJAQABACwAAAAAKAAoAAAClYx/oLvoxuJDkU1a1YUZbJ59nSd2ZXhWqbRa2/gF8Gu2DY3iqs7yrq+xBYEkYvFSM8aSSObE+ZgRl1BHFZNr7pRCavZ5BW2142hY3AN/zWtsmf12p9XxxFl2lpLn1rseztfXZjdIWIf2s5dItwjYKBgo9yg5pHgzJXTEeGlZuenpyPmpGQoKOWkYmSpaSnqKileI2FAAACH5BAkBAAEALAAAAAAoACgAAAKVjB+gu+jG4kORTVrVhRlsnn2dJ3ZleFaptFrb+CXmO9OozeL5VfP99HvAWhpiUdcwkpBH3825AwYdU8xTqlLGhtCosArKMpvfa1mMRae9VvWZfeB2XfPkeLmm18lUcBj+p5dnN8jXZ3YIGEhYuOUn45aoCDkp16hl5IjYJvjWKcnoGQpqyPlpOhr3aElaqrq56Bq7VAAAOw==");
	height: 100%;
	filter: alpha(opacity=25); 
	opacity: 0.25;
}
.ui-progressbar-indeterminate .ui-progressbar-value {
	background-image: none;
}
.ui-selectable {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-selectable-helper {
	position: absolute;
	z-index: 100;
	border: 1px dotted black;
}
.ui-selectmenu-menu {
	padding: 0;
	margin: 0;
	position: absolute;
	top: 0;
	left: 0;
	display: none;
}
.ui-selectmenu-menu .ui-menu {
	overflow: auto;
	overflow-x: hidden;
	padding-bottom: 1px;
}
.ui-selectmenu-menu .ui-menu .ui-selectmenu-optgroup {
	font-size: 1em;
	font-weight: bold;
	line-height: 1.5;
	padding: 2px 0.4em;
	margin: 0.5em 0 0 0;
	height: auto;
	border: 0;
}
.ui-selectmenu-open {
	display: block;
}
.ui-selectmenu-text {
	display: block;
	margin-right: 20px;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-selectmenu-button.ui-button {
	text-align: left;
	white-space: nowrap;
	width: 14em;
}
.ui-selectmenu-icon.ui-icon {
	float: right;
	margin-top: 0;
}
.ui-slider {
	position: relative;
	text-align: left;
}
.ui-slider .ui-slider-handle {
	position: absolute;
	z-index: 2;
	width: 1.2em;
	height: 1.2em;
	cursor: default;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-slider .ui-slider-range {
	position: absolute;
	z-index: 1;
	font-size: .7em;
	display: block;
	border: 0;
	background-position: 0 0;
}


.ui-slider.ui-state-disabled .ui-slider-handle,
.ui-slider.ui-state-disabled .ui-slider-range {
	filter: inherit;
}

.ui-slider-horizontal {
	height: .8em;
}
.ui-slider-horizontal .ui-slider-handle {
	top: -.3em;
	margin-left: -.6em;
}
.ui-slider-horizontal .ui-slider-range {
	top: 0;
	height: 100%;
}
.ui-slider-horizontal .ui-slider-range-min {
	left: 0;
}
.ui-slider-horizontal .ui-slider-range-max {
	right: 0;
}

.ui-slider-vertical {
	width: .8em;
	height: 100px;
}
.ui-slider-vertical .ui-slider-handle {
	left: -.3em;
	margin-left: 0;
	margin-bottom: -.6em;
}
.ui-slider-vertical .ui-slider-range {
	left: 0;
	width: 100%;
}
.ui-slider-vertical .ui-slider-range-min {
	bottom: 0;
}
.ui-slider-vertical .ui-slider-range-max {
	top: 0;
}
.ui-sortable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-spinner {
	position: relative;
	display: inline-block;
	overflow: hidden;
	padding: 0;
	vertical-align: middle;
}
.ui-spinner-input {
	border: none;
	background: none;
	color: inherit;
	padding: .222em 0;
	margin: .2em 0;
	vertical-align: middle;
	margin-left: .4em;
	margin-right: 2em;
}
.ui-spinner-button {
	width: 1.6em;
	height: 50%;
	font-size: .5em;
	padding: 0;
	margin: 0;
	text-align: center;
	position: absolute;
	cursor: default;
	display: block;
	overflow: hidden;
	right: 0;
}

.ui-spinner a.ui-spinner-button {
	border-top-style: none;
	border-bottom-style: none;
	border-right-style: none;
}
.ui-spinner-up {
	top: 0;
}
.ui-spinner-down {
	bottom: 0;
}
.ui-tabs {
	position: relative;
	padding: .2em;
}
.ui-tabs .ui-tabs-nav {
	margin: 0;
	padding: .2em .2em 0;
}
.ui-tabs .ui-tabs-nav li {
	list-style: none;
	float: left;
	position: relative;
	top: 0;
	margin: 1px .2em 0 0;
	border-bottom-width: 0;
	padding: 0;
	white-space: nowrap;
}
.ui-tabs .ui-tabs-nav .ui-tabs-anchor {
	float: left;
	padding: .5em 1em;
	text-decoration: none;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active {
	margin-bottom: -1px;
	padding-bottom: 1px;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-state-disabled .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-tabs-loading .ui-tabs-anchor {
	cursor: text;
}
.ui-tabs-collapsible .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor {
	cursor: pointer;
}
.ui-tabs .ui-tabs-panel {
	display: block;
	border-width: 0;
	padding: 1em 1.4em;
	background: none;
}
.ui-tooltip {
	padding: 8px;
	position: absolute;
	z-index: 9999;
	max-width: 300px;
}
body .ui-tooltip {
	border-width: 2px;
}

.ui-widget {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget .ui-widget {
	font-size: 1em;
}
.ui-widget input,
.ui-widget select,
.ui-widget textarea,
.ui-widget button {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget.ui-widget-content {
	border: 1px solid #c5c5c5;
}
.ui-widget-content {
	border: 1px solid #dddddd;
	background: #ffffff;
	color: #333333;
}
.ui-widget-content a {
	color: #333333;
}
.ui-widget-header {
	border: 1px solid #dddddd;
	background: #e9e9e9;
	color: #333333;
	font-weight: bold;
}
.ui-widget-header a {
	color: #333333;
}


.ui-state-default,
.ui-widget-content .ui-state-default,
.ui-widget-header .ui-state-default,
.ui-button,


html .ui-button.ui-state-disabled:hover,
html .ui-button.ui-state-disabled:active {
	border: 1px solid #c5c5c5;
	background: #f6f6f6;
	font-weight: normal;
	color: #454545;
}
.ui-state-default a,
.ui-state-default a:link,
.ui-state-default a:visited,
a.ui-button,
a:link.ui-button,
a:visited.ui-button,
.ui-button {
	color: #454545;
	text-decoration: none;
}
.ui-state-hover,
.ui-widget-content .ui-state-hover,
.ui-widget-header .ui-state-hover,
.ui-state-focus,
.ui-widget-content .ui-state-focus,
.ui-widget-header .ui-state-focus,
.ui-button:hover,
.ui-button:focus {
	border: 1px solid #cccccc;
	background: #ededed;
	font-weight: normal;
	color: #2b2b2b;
}
.ui-state-hover a,
.ui-state-hover a:hover,
.ui-state-hover a:link,
.ui-state-hover a:visited,
.ui-state-focus a,
.ui-state-focus a:hover,
.ui-state-focus a:link,
.ui-state-focus a:visited,
a.ui-button:hover,
a.ui-button:focus {
	color: #2b2b2b;
	text-decoration: none;
}

.ui-visual-focus {
	box-shadow: 0 0 3px 1px rgb(94, 158, 214);
}
.ui-state-active,
.ui-widget-content .ui-state-active,
.ui-widget-header .ui-state-active,
a.ui-button:active,
.ui-button:active,
.ui-button.ui-state-active:hover {
	border: 1px solid #003eff;
	background: #007fff;
	font-weight: normal;
	color: #ffffff;
}
.ui-icon-background,
.ui-state-active .ui-icon-background {
	border: #003eff;
	background-color: #ffffff;
}
.ui-state-active a,
.ui-state-active a:link,
.ui-state-active a:visited {
	color: #ffffff;
	text-decoration: none;
}


.ui-state-highlight,
.ui-widget-content .ui-state-highlight,
.ui-widget-header .ui-state-highlight {
	border: 1px solid #dad55e;
	background: #fffa90;
	color: #777620;
}
.ui-state-checked {
	border: 1px solid #dad55e;
	background: #fffa90;
}
.ui-state-highlight a,
.ui-widget-content .ui-state-highlight a,
.ui-widget-header .ui-state-highlight a {
	color: #777620;
}
.ui-state-error,
.ui-widget-content .ui-state-error,
.ui-widget-header .ui-state-error {
	border: 1px solid #f1a899;
	background: #fddfdf;
	color: #5f3f3f;
}
.ui-state-error a,
.ui-widget-content .ui-state-error a,
.ui-widget-header .ui-state-error a {
	color: #5f3f3f;
}
.ui-state-error-text,
.ui-widget-content .ui-state-error-text,
.ui-widget-header .ui-state-error-text {
	color: #5f3f3f;
}
.ui-priority-primary,
.ui-widget-content .ui-priority-primary,
.ui-widget-header .ui-priority-primary {
	font-weight: bold;
}
.ui-priority-secondary,
.ui-widget-content .ui-priority-secondary,
.ui-widget-header .ui-priority-secondary {
	opacity: .7;
	filter:Alpha(Opacity=70); 
	font-weight: normal;
}
.ui-state-disabled,
.ui-widget-content .ui-state-disabled,
.ui-widget-header .ui-state-disabled {
	opacity: .35;
	filter:Alpha(Opacity=35); 
	background-image: none;
}
.ui-state-disabled .ui-icon {
	filter:Alpha(Opacity=35); 
}




.ui-icon {
	width: 16px;
	height: 16px;
}
.ui-icon,
.ui-widget-content .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-widget-header .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-state-hover .ui-icon,
.ui-state-focus .ui-icon,
.ui-button:hover .ui-icon,
.ui-button:focus .ui-icon {
	background-image: url("images/ui-icons_555555_256x240.png");
}
.ui-state-active .ui-icon,
.ui-button:active .ui-icon {
	background-image: url("images/ui-icons_ffffff_256x240.png");
}
.ui-state-highlight .ui-icon,
.ui-button .ui-state-highlight.ui-icon {
	background-image: url("images/ui-icons_777620_256x240.png");
}
.ui-state-error .ui-icon,
.ui-state-error-text .ui-icon {
	background-image: url("images/ui-icons_cc0000_256x240.png");
}
.ui-button .ui-icon {
	background-image: url("images/ui-icons_777777_256x240.png");
}


.ui-icon-blank { background-position: 16px 16px; }
.ui-icon-caret-1-n { background-position: 0 0; }
.ui-icon-caret-1-ne { background-position: -16px 0; }
.ui-icon-caret-1-e { background-position: -32px 0; }
.ui-icon-caret-1-se { background-position: -48px 0; }
.ui-icon-caret-1-s { background-position: -65px 0; }
.ui-icon-caret-1-sw { background-position: -80px 0; }
.ui-icon-caret-1-w { background-position: -96px 0; }
.ui-icon-caret-1-nw { background-position: -112px 0; }
.ui-icon-caret-2-n-s { background-position: -128px 0; }
.ui-icon-caret-2-e-w { background-position: -144px 0; }
.ui-icon-triangle-1-n { background-position: 0 -16px; }
.ui-icon-triangle-1-ne { background-position: -16px -16px; }
.ui-icon-triangle-1-e { background-position: -32px -16px; }
.ui-icon-triangle-1-se { background-position: -48px -16px; }
.ui-icon-triangle-1-s { background-position: -65px -16px; }
.ui-icon-triangle-1-sw { background-position: -80px -16px; }
.ui-icon-triangle-1-w { background-position: -96px -16px; }
.ui-icon-triangle-1-nw { background-position: -112px -16px; }
.ui-icon-triangle-2-n-s { background-position: -128px -16px; }
.ui-icon-triangle-2-e-w { background-position: -144px -16px; }
.ui-icon-arrow-1-n { background-position: 0 -32px; }
.ui-icon-arrow-1-ne { background-position: -16px -32px; }
.ui-icon-arrow-1-e { background-position: -32px -32px; }
.ui-icon-arrow-1-se { background-position: -48px -32px; }
.ui-icon-arrow-1-s { background-position: -65px -32px; }
.ui-icon-arrow-1-sw { background-position: -80px -32px; }
.ui-icon-arrow-1-w { background-position: -96px -32px; }
.ui-icon-arrow-1-nw { background-position: -112px -32px; }
.ui-icon-arrow-2-n-s { background-position: -128px -32px; }
.ui-icon-arrow-2-ne-sw { background-position: -144px -32px; }
.ui-icon-arrow-2-e-w { background-position: -160px -32px; }
.ui-icon-arrow-2-se-nw { background-position: -176px -32px; }
.ui-icon-arrowstop-1-n { background-position: -192px -32px; }
.ui-icon-arrowstop-1-e { background-position: -208px -32px; }
.ui-icon-arrowstop-1-s { background-position: -224px -32px; }
.ui-icon-arrowstop-1-w { background-position: -240px -32px; }
.ui-icon-arrowthick-1-n { background-position: 1px -48px; }
.ui-icon-arrowthick-1-ne { background-position: -16px -48px; }
.ui-icon-arrowthick-1-e { background-position: -32px -48px; }
.ui-icon-arrowthick-1-se { background-position: -48px -48px; }
.ui-icon-arrowthick-1-s { background-position: -64px -48px; }
.ui-icon-arrowthick-1-sw { background-position: -80px -48px; }
.ui-icon-arrowthick-1-w { background-position: -96px -48px; }
.ui-icon-arrowthick-1-nw { background-position: -112px -48px; }
.ui-icon-arrowthick-2-n-s { background-position: -128px -48px; }
.ui-icon-arrowthick-2-ne-sw { background-position: -144px -48px; }
.ui-icon-arrowthick-2-e-w { background-position: -160px -48px; }
.ui-icon-arrowthick-2-se-nw { background-position: -176px -48px; }
.ui-icon-arrowthickstop-1-n { background-position: -192px -48px; }
.ui-icon-arrowthickstop-1-e { background-position: -208px -48px; }
.ui-icon-arrowthickstop-1-s { background-position: -224px -48px; }
.ui-icon-arrowthickstop-1-w { background-position: -240px -48px; }
.ui-icon-arrowreturnthick-1-w { background-position: 0 -64px; }
.ui-icon-arrowreturnthick-1-n { background-position: -16px -64px; }
.ui-icon-arrowreturnthick-1-e { background-position: -32px -64px; }
.ui-icon-arrowreturnthick-1-s { background-position: -48px -64px; }
.ui-icon-arrowreturn-1-w { background-position: -64px -64px; }
.ui-icon-arrowreturn-1-n { background-position: -80px -64px; }
.ui-icon-arrowreturn-1-e { background-position: -96px -64px; }
.ui-icon-arrowreturn-1-s { background-position: -112px -64px; }
.ui-icon-arrowrefresh-1-w { background-position: -128px -64px; }
.ui-icon-arrowrefresh-1-n { background-position: -144px -64px; }
.ui-icon-arrowrefresh-1-e { background-position: -160px -64px; }
.ui-icon-arrowrefresh-1-s { background-position: -176px -64px; }
.ui-icon-arrow-4 { background-position: 0 -80px; }
.ui-icon-arrow-4-diag { background-position: -16px -80px; }
.ui-icon-extlink { background-position: -32px -80px; }
.ui-icon-newwin { background-position: -48px -80px; }
.ui-icon-refresh { background-position: -64px -80px; }
.ui-icon-shuffle { background-position: -80px -80px; }
.ui-icon-transfer-e-w { background-position: -96px -80px; }
.ui-icon-transferthick-e-w { background-position: -112px -80px; }
.ui-icon-folder-collapsed { background-position: 0 -96px; }
.ui-icon-folder-open { background-position: -16px -96px; }
.ui-icon-document { background-position: -32px -96px; }
.ui-icon-document-b { background-position: -48px -96px; }
.ui-icon-note { background-position: -64px -96px; }
.ui-icon-mail-closed { background-position: -80px -96px; }
.ui-icon-mail-open { background-position: -96px -96px; }
.ui-icon-suitcase { background-position: -112px -96px; }
.ui-icon-comment { background-position: -128px -96px; }
.ui-icon-person { background-position: -144px -96px; }
.ui-icon-print { background-position: -160px -96px; }
.ui-icon-trash { background-position: -176px -96px; }
.ui-icon-locked { background-position: -192px -96px; }
.ui-icon-unlocked { background-position: -208px -96px; }
.ui-icon-bookmark { background-position: -224px -96px; }
.ui-icon-tag { background-position: -240px -96px; }
.ui-icon-home { background-position: 0 -112px; }
.ui-icon-flag { background-position: -16px -112px; }
.ui-icon-calendar { background-position: -32px -112px; }
.ui-icon-cart { background-position: -48px -112px; }
.ui-icon-pencil { background-position: -64px -112px; }
.ui-icon-clock { background-position: -80px -112px; }
.ui-icon-disk { background-position: -96px -112px; }
.ui-icon-calculator { background-position: -112px -112px; }
.ui-icon-zoomin { background-position: -128px -112px; }
.ui-icon-zoomout { background-position: -144px -112px; }
.ui-icon-search { background-position: -160px -112px; }
.ui-icon-wrench { background-position: -176px -112px; }
.ui-icon-gear { background-position: -192px -112px; }
.ui-icon-heart { background-position: -208px -112px; }
.ui-icon-star { background-position: -224px -112px; }
.ui-icon-link { background-position: -240px -112px; }
.ui-icon-cancel { background-position: 0 -128px; }
.ui-icon-plus { background-position: -16px -128px; }
.ui-icon-plusthick { background-position: -32px -128px; }
.ui-icon-minus { background-position: -48px -128px; }
.ui-icon-minusthick { background-position: -64px -128px; }
.ui-icon-close { background-position: -80px -128px; }
.ui-icon-closethick { background-position: -96px -128px; }
.ui-icon-key { background-position: -112px -128px; }
.ui-icon-lightbulb { background-position: -128px -128px; }
.ui-icon-scissors { background-position: -144px -128px; }
.ui-icon-clipboard { background-position: -160px -128px; }
.ui-icon-copy { background-position: -176px -128px; }
.ui-icon-contact { background-position: -192px -128px; }
.ui-icon-image { background-position: -208px -128px; }
.ui-icon-video { background-position: -224px -128px; }
.ui-icon-script { background-position: -240px -128px; }
.ui-icon-alert { background-position: 0 -144px; }
.ui-icon-info { background-position: -16px -144px; }
.ui-icon-notice { background-position: -32px -144px; }
.ui-icon-help { background-position: -48px -144px; }
.ui-icon-check { background-position: -64px -144px; }
.ui-icon-bullet { background-position: -80px -144px; }
.ui-icon-radio-on { background-position: -96px -144px; }
.ui-icon-radio-off { background-position: -112px -144px; }
.ui-icon-pin-w { background-position: -128px -144px; }
.ui-icon-pin-s { background-position: -144px -144px; }
.ui-icon-play { background-position: 0 -160px; }
.ui-icon-pause { background-position: -16px -160px; }
.ui-icon-seek-next { background-position: -32px -160px; }
.ui-icon-seek-prev { background-position: -48px -160px; }
.ui-icon-seek-end { background-position: -64px -160px; }
.ui-icon-seek-start { background-position: -80px -160px; }

.ui-icon-seek-first { background-position: -80px -160px; }
.ui-icon-stop { background-position: -96px -160px; }
.ui-icon-eject { background-position: -112px -160px; }
.ui-icon-volume-off { background-position: -128px -160px; }
.ui-icon-volume-on { background-position: -144px -160px; }
.ui-icon-power { background-position: 0 -176px; }
.ui-icon-signal-diag { background-position: -16px -176px; }
.ui-icon-signal { background-position: -32px -176px; }
.ui-icon-battery-0 { background-position: -48px -176px; }
.ui-icon-battery-1 { background-position: -64px -176px; }
.ui-icon-battery-2 { background-position: -80px -176px; }
.ui-icon-battery-3 { background-position: -96px -176px; }
.ui-icon-circle-plus { background-position: 0 -192px; }
.ui-icon-circle-minus { background-position: -16px -192px; }
.ui-icon-circle-close { background-position: -32px -192px; }
.ui-icon-circle-triangle-e { background-position: -48px -192px; }
.ui-icon-circle-triangle-s { background-position: -64px -192px; }
.ui-icon-circle-triangle-w { background-position: -80px -192px; }
.ui-icon-circle-triangle-n { background-position: -96px -192px; }
.ui-icon-circle-arrow-e { background-position: -112px -192px; }
.ui-icon-circle-arrow-s { background-position: -128px -192px; }
.ui-icon-circle-arrow-w { background-position: -144px -192px; }
.ui-icon-circle-arrow-n { background-position: -160px -192px; }
.ui-icon-circle-zoomin { background-position: -176px -192px; }
.ui-icon-circle-zoomout { background-position: -192px -192px; }
.ui-icon-circle-check { background-position: -208px -192px; }
.ui-icon-circlesmall-plus { background-position: 0 -208px; }
.ui-icon-circlesmall-minus { background-position: -16px -208px; }
.ui-icon-circlesmall-close { background-position: -32px -208px; }
.ui-icon-squaresmall-plus { background-position: -48px -208px; }
.ui-icon-squaresmall-minus { background-position: -64px -208px; }
.ui-icon-squaresmall-close { background-position: -80px -208px; }
.ui-icon-grip-dotted-vertical { background-position: 0 -224px; }
.ui-icon-grip-dotted-horizontal { background-position: -16px -224px; }
.ui-icon-grip-solid-vertical { background-position: -32px -224px; }
.ui-icon-grip-solid-horizontal { background-position: -48px -224px; }
.ui-icon-gripsmall-diagonal-se { background-position: -64px -224px; }
.ui-icon-grip-diagonal-se { background-position: -80px -224px; }





.ui-corner-all,
.ui-corner-top,
.ui-corner-left,
.ui-corner-tl {
	border-top-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-top,
.ui-corner-right,
.ui-corner-tr {
	border-top-right-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-left,
.ui-corner-bl {
	border-bottom-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-right,
.ui-corner-br {
	border-bottom-right-radius: 3px;
}


.ui-widget-overlay {
	background: #aaaaaa;
	opacity: .3;
	filter: Alpha(Opacity=30); 
}
.ui-widget-shadow {
	-webkit-box-shadow: 0px 0px 5px #666666;
	box-shadow: 0px 0px 5px #666666;
} 
</style>
<script src='js/jquery-1.12.4.js'></script>
<script src='js/jquery-ui.js'></script>

<script>
$( function() {
	$( '#tabs-collect-classes-from-hierarchical-partition' ).tabs();
} );
</script>
<div id='tabs-collect-classes-from-hierarchical-partition'>
<ul>
<li><a href='#tab-collect-classes-from-hierarchical-partition-1'>n_signatures ≥ 1384</a></li>
<li><a href='#tab-collect-classes-from-hierarchical-partition-2'>n_signatures ≥ 9467</a></li>
<li><a href='#tab-collect-classes-from-hierarchical-partition-3'>n_signatures ≥ 9645</a></li>
</ul>
<div id='tab-collect-classes-from-hierarchical-partition-1'>
<pre><code class="r">collect_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 1384))
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-hierarchical-partition-1-1.png" alt="plot of chunk tab-collect-classes-from-hierarchical-partition-1"/></p>

</div>
<div id='tab-collect-classes-from-hierarchical-partition-2'>
<pre><code class="r">collect_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 9467))
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-hierarchical-partition-2-1.png" alt="plot of chunk tab-collect-classes-from-hierarchical-partition-2"/></p>

</div>
<div id='tab-collect-classes-from-hierarchical-partition-3'>
<pre><code class="r">collect_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 9645))
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-hierarchical-partition-3-1.png" alt="plot of chunk tab-collect-classes-from-hierarchical-partition-3"/></p>

</div>
</div>

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it).


<script>
$( function() {
	$( '#tabs-get-classes-from-hierarchical-partition' ).tabs();
} );
</script>
<div id='tabs-get-classes-from-hierarchical-partition'>
<ul>
<li><a href='#tab-get-classes-from-hierarchical-partition-1'>n_signatures ≥ 1384</a></li>
<li><a href='#tab-get-classes-from-hierarchical-partition-2'>n_signatures ≥ 9467</a></li>
<li><a href='#tab-get-classes-from-hierarchical-partition-3'>n_signatures ≥ 9645</a></li>
</ul>

<div id='tab-get-classes-from-hierarchical-partition-1'>
<p><a id='tab-get-classes-from-hierarchical-partition-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">get_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 1384))
</code></pre>

<pre><code>#&gt; TCGA.KL.8323.01 TCGA.KL.8332.01 TCGA.KL.8330.01 TCGA.KM.8443.01 TCGA.KL.8339.01 TCGA.KN.8428.01 
#&gt;            &quot;03&quot;           &quot;023&quot;          &quot;0224&quot;            &quot;03&quot;          &quot;0223&quot;           &quot;023&quot; 
#&gt; TCGA.KL.8326.01 TCGA.KM.8476.01 TCGA.KN.8429.01 TCGA.KO.8408.01 TCGA.KN.8425.01 TCGA.KO.8414.01 
#&gt;           &quot;023&quot;            &quot;01&quot;          &quot;0221&quot;          &quot;0222&quot;            &quot;03&quot;            &quot;03&quot; 
#&gt; TCGA.KN.8436.01 TCGA.KL.8342.01 TCGA.KM.8440.01 TCGA.KO.8410.01 TCGA.KL.8325.01 TCGA.KL.8340.01 
#&gt;          &quot;0224&quot;            &quot;01&quot;          &quot;0221&quot;           &quot;023&quot;            &quot;03&quot;          &quot;0221&quot; 
#&gt; TCGA.KL.8327.01 TCGA.KN.8437.01 TCGA.KL.8344.01 TCGA.KN.8435.01 TCGA.KO.8415.01 TCGA.KO.8411.01 
#&gt;            &quot;01&quot;           &quot;021&quot;           &quot;023&quot;          &quot;0223&quot;            &quot;03&quot;            &quot;01&quot; 
#&gt; TCGA.KO.8404.01 TCGA.KN.8427.01 TCGA.KN.8423.01 TCGA.KL.8337.01 TCGA.KO.8405.01 TCGA.KN.8424.01 
#&gt;           &quot;021&quot;           &quot;021&quot;           &quot;023&quot;           &quot;023&quot;           &quot;023&quot;          &quot;0221&quot; 
#&gt; TCGA.KN.8426.01 TCGA.KM.8442.01 TCGA.KM.8441.01 TCGA.KM.8477.01 TCGA.KM.8439.01 TCGA.KL.8346.01 
#&gt;          &quot;0222&quot;            &quot;03&quot;           &quot;021&quot;           &quot;023&quot;           &quot;021&quot;            &quot;03&quot; 
#&gt; TCGA.KL.8335.01 TCGA.KM.8438.01 TCGA.KO.8413.01 TCGA.KL.8331.01 TCGA.KL.8345.01 TCGA.KN.8432.01 
#&gt;          &quot;0222&quot;          &quot;0221&quot;           &quot;023&quot;          &quot;0222&quot;            &quot;01&quot;           &quot;023&quot; 
#&gt; TCGA.KM.8639.01 TCGA.KN.8419.01 TCGA.KN.8421.01 TCGA.KO.8403.01 TCGA.KL.8336.01 TCGA.KL.8334.01 
#&gt;           &quot;021&quot;            &quot;01&quot;           &quot;023&quot;            &quot;01&quot;          &quot;0222&quot;           &quot;023&quot; 
#&gt; TCGA.KO.8409.01 TCGA.KO.8407.01 TCGA.KN.8422.01 TCGA.KN.8418.01 TCGA.KO.8406.01 TCGA.KO.8417.01 
#&gt;            &quot;03&quot;           &quot;023&quot;          &quot;0221&quot;          &quot;0221&quot;            &quot;01&quot;            &quot;03&quot; 
#&gt; TCGA.KL.8343.01 TCGA.KN.8430.01 TCGA.KL.8341.01 TCGA.KL.8328.01 TCGA.KN.8434.01 TCGA.KL.8324.01 
#&gt;            &quot;03&quot;          &quot;0222&quot;          &quot;0223&quot;          &quot;0222&quot;            &quot;03&quot;          &quot;0221&quot; 
#&gt; TCGA.KO.8416.01 TCGA.KL.8333.01 TCGA.KL.8329.01 TCGA.KL.8338.01 TCGA.KN.8433.01 TCGA.KN.8431.01 
#&gt;            &quot;03&quot;           &quot;021&quot;          &quot;0221&quot;           &quot;023&quot;           &quot;021&quot;          &quot;0221&quot;
</code></pre>

<script>
$('#tab-get-classes-from-hierarchical-partition-1-a').parent().next().next().hide();
$('#tab-get-classes-from-hierarchical-partition-1-a').click(function(){
  $('#tab-get-classes-from-hierarchical-partition-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-get-classes-from-hierarchical-partition-2'>
<p><a id='tab-get-classes-from-hierarchical-partition-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">get_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 9467))
</code></pre>

<pre><code>#&gt; TCGA.KL.8323.01 TCGA.KL.8332.01 TCGA.KL.8330.01 TCGA.KM.8443.01 TCGA.KL.8339.01 TCGA.KN.8428.01 
#&gt;            &quot;03&quot;           &quot;023&quot;           &quot;022&quot;            &quot;03&quot;           &quot;022&quot;           &quot;023&quot; 
#&gt; TCGA.KL.8326.01 TCGA.KM.8476.01 TCGA.KN.8429.01 TCGA.KO.8408.01 TCGA.KN.8425.01 TCGA.KO.8414.01 
#&gt;           &quot;023&quot;            &quot;01&quot;           &quot;022&quot;           &quot;022&quot;            &quot;03&quot;            &quot;03&quot; 
#&gt; TCGA.KN.8436.01 TCGA.KL.8342.01 TCGA.KM.8440.01 TCGA.KO.8410.01 TCGA.KL.8325.01 TCGA.KL.8340.01 
#&gt;           &quot;022&quot;            &quot;01&quot;           &quot;022&quot;           &quot;023&quot;            &quot;03&quot;           &quot;022&quot; 
#&gt; TCGA.KL.8327.01 TCGA.KN.8437.01 TCGA.KL.8344.01 TCGA.KN.8435.01 TCGA.KO.8415.01 TCGA.KO.8411.01 
#&gt;            &quot;01&quot;           &quot;021&quot;           &quot;023&quot;           &quot;022&quot;            &quot;03&quot;            &quot;01&quot; 
#&gt; TCGA.KO.8404.01 TCGA.KN.8427.01 TCGA.KN.8423.01 TCGA.KL.8337.01 TCGA.KO.8405.01 TCGA.KN.8424.01 
#&gt;           &quot;021&quot;           &quot;021&quot;           &quot;023&quot;           &quot;023&quot;           &quot;023&quot;           &quot;022&quot; 
#&gt; TCGA.KN.8426.01 TCGA.KM.8442.01 TCGA.KM.8441.01 TCGA.KM.8477.01 TCGA.KM.8439.01 TCGA.KL.8346.01 
#&gt;           &quot;022&quot;            &quot;03&quot;           &quot;021&quot;           &quot;023&quot;           &quot;021&quot;            &quot;03&quot; 
#&gt; TCGA.KL.8335.01 TCGA.KM.8438.01 TCGA.KO.8413.01 TCGA.KL.8331.01 TCGA.KL.8345.01 TCGA.KN.8432.01 
#&gt;           &quot;022&quot;           &quot;022&quot;           &quot;023&quot;           &quot;022&quot;            &quot;01&quot;           &quot;023&quot; 
#&gt; TCGA.KM.8639.01 TCGA.KN.8419.01 TCGA.KN.8421.01 TCGA.KO.8403.01 TCGA.KL.8336.01 TCGA.KL.8334.01 
#&gt;           &quot;021&quot;            &quot;01&quot;           &quot;023&quot;            &quot;01&quot;           &quot;022&quot;           &quot;023&quot; 
#&gt; TCGA.KO.8409.01 TCGA.KO.8407.01 TCGA.KN.8422.01 TCGA.KN.8418.01 TCGA.KO.8406.01 TCGA.KO.8417.01 
#&gt;            &quot;03&quot;           &quot;023&quot;           &quot;022&quot;           &quot;022&quot;            &quot;01&quot;            &quot;03&quot; 
#&gt; TCGA.KL.8343.01 TCGA.KN.8430.01 TCGA.KL.8341.01 TCGA.KL.8328.01 TCGA.KN.8434.01 TCGA.KL.8324.01 
#&gt;            &quot;03&quot;           &quot;022&quot;           &quot;022&quot;           &quot;022&quot;            &quot;03&quot;           &quot;022&quot; 
#&gt; TCGA.KO.8416.01 TCGA.KL.8333.01 TCGA.KL.8329.01 TCGA.KL.8338.01 TCGA.KN.8433.01 TCGA.KN.8431.01 
#&gt;            &quot;03&quot;           &quot;021&quot;           &quot;022&quot;           &quot;023&quot;           &quot;021&quot;           &quot;022&quot;
</code></pre>

<script>
$('#tab-get-classes-from-hierarchical-partition-2-a').parent().next().next().hide();
$('#tab-get-classes-from-hierarchical-partition-2-a').click(function(){
  $('#tab-get-classes-from-hierarchical-partition-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-get-classes-from-hierarchical-partition-3'>
<p><a id='tab-get-classes-from-hierarchical-partition-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">get_classes(res_rh, merge_node = merge_node_param(min_n_signatures = 9645))
</code></pre>

<pre><code>#&gt; TCGA.KL.8323.01 TCGA.KL.8332.01 TCGA.KL.8330.01 TCGA.KM.8443.01 TCGA.KL.8339.01 TCGA.KN.8428.01 
#&gt;            &quot;03&quot;            &quot;02&quot;            &quot;02&quot;            &quot;03&quot;            &quot;02&quot;            &quot;02&quot; 
#&gt; TCGA.KL.8326.01 TCGA.KM.8476.01 TCGA.KN.8429.01 TCGA.KO.8408.01 TCGA.KN.8425.01 TCGA.KO.8414.01 
#&gt;            &quot;02&quot;            &quot;01&quot;            &quot;02&quot;            &quot;02&quot;            &quot;03&quot;            &quot;03&quot; 
#&gt; TCGA.KN.8436.01 TCGA.KL.8342.01 TCGA.KM.8440.01 TCGA.KO.8410.01 TCGA.KL.8325.01 TCGA.KL.8340.01 
#&gt;            &quot;02&quot;            &quot;01&quot;            &quot;02&quot;            &quot;02&quot;            &quot;03&quot;            &quot;02&quot; 
#&gt; TCGA.KL.8327.01 TCGA.KN.8437.01 TCGA.KL.8344.01 TCGA.KN.8435.01 TCGA.KO.8415.01 TCGA.KO.8411.01 
#&gt;            &quot;01&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;            &quot;03&quot;            &quot;01&quot; 
#&gt; TCGA.KO.8404.01 TCGA.KN.8427.01 TCGA.KN.8423.01 TCGA.KL.8337.01 TCGA.KO.8405.01 TCGA.KN.8424.01 
#&gt;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot; 
#&gt; TCGA.KN.8426.01 TCGA.KM.8442.01 TCGA.KM.8441.01 TCGA.KM.8477.01 TCGA.KM.8439.01 TCGA.KL.8346.01 
#&gt;            &quot;02&quot;            &quot;03&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;            &quot;03&quot; 
#&gt; TCGA.KL.8335.01 TCGA.KM.8438.01 TCGA.KO.8413.01 TCGA.KL.8331.01 TCGA.KL.8345.01 TCGA.KN.8432.01 
#&gt;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;            &quot;01&quot;            &quot;02&quot; 
#&gt; TCGA.KM.8639.01 TCGA.KN.8419.01 TCGA.KN.8421.01 TCGA.KO.8403.01 TCGA.KL.8336.01 TCGA.KL.8334.01 
#&gt;            &quot;02&quot;            &quot;01&quot;            &quot;02&quot;            &quot;01&quot;            &quot;02&quot;            &quot;02&quot; 
#&gt; TCGA.KO.8409.01 TCGA.KO.8407.01 TCGA.KN.8422.01 TCGA.KN.8418.01 TCGA.KO.8406.01 TCGA.KO.8417.01 
#&gt;            &quot;03&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;            &quot;01&quot;            &quot;03&quot; 
#&gt; TCGA.KL.8343.01 TCGA.KN.8430.01 TCGA.KL.8341.01 TCGA.KL.8328.01 TCGA.KN.8434.01 TCGA.KL.8324.01 
#&gt;            &quot;03&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;            &quot;03&quot;            &quot;02&quot; 
#&gt; TCGA.KO.8416.01 TCGA.KL.8333.01 TCGA.KL.8329.01 TCGA.KL.8338.01 TCGA.KN.8433.01 TCGA.KN.8431.01 
#&gt;            &quot;03&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;            &quot;02&quot;
</code></pre>

<script>
$('#tab-get-classes-from-hierarchical-partition-3-a').parent().next().next().hide();
$('#tab-get-classes-from-hierarchical-partition-3-a').click(function(){
  $('#tab-get-classes-from-hierarchical-partition-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>



### Top rows heatmap

Heatmaps of the top rows:





```r
top_rows_heatmap(res_rh)
```

![plot of chunk top-rows-heatmap](figure_cola/top-rows-heatmap-1.png)

```
#> Error in h(simpleError(msg, call)) : 
#>   error in evaluating the argument 'object' in selecting a method for function 'draw': no applicable method for 'height' applied to an object of class "list"
```

Top rows on each node:


```r
top_rows_overlap(res_rh, method = "upset")
```

![plot of chunk top-rows-overlap](figure_cola/top-rows-overlap-1.png)


### UMAP plot

UMAP plot which shows how samples are separated.




<script>
$( function() {
	$( '#tabs-dimension-reduction-by-depth' ).tabs();
} );
</script>
<div id='tabs-dimension-reduction-by-depth'>
<ul>
<li><a href='#tab-dimension-reduction-by-depth-1'>n_signatures ≥ 1384</a></li>
<li><a href='#tab-dimension-reduction-by-depth-2'>n_signatures ≥ 9467</a></li>
<li><a href='#tab-dimension-reduction-by-depth-3'>n_signatures ≥ 9645</a></li>
</ul>
<div id='tab-dimension-reduction-by-depth-1'>
<pre><code class="r">par(mfrow = c(1, 2))
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 1384),
    method = &quot;UMAP&quot;, top_value_method = &quot;SD&quot;, top_n = 40000, scale_rows = FALSE)
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 1384),
    method = &quot;UMAP&quot;, top_value_method = &quot;ATC&quot;, top_n = 40000, scale_rows = TRUE)
</code></pre>

<p><img src="figure_cola/tab-dimension-reduction-by-depth-1-1.png" title="plot of chunk tab-dimension-reduction-by-depth-1" alt="plot of chunk tab-dimension-reduction-by-depth-1" width="100%" /></p>

</div>
<div id='tab-dimension-reduction-by-depth-2'>
<pre><code class="r">par(mfrow = c(1, 2))
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 9467),
    method = &quot;UMAP&quot;, top_value_method = &quot;SD&quot;, top_n = 40000, scale_rows = FALSE)
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 9467),
    method = &quot;UMAP&quot;, top_value_method = &quot;ATC&quot;, top_n = 40000, scale_rows = TRUE)
</code></pre>

<p><img src="figure_cola/tab-dimension-reduction-by-depth-2-1.png" title="plot of chunk tab-dimension-reduction-by-depth-2" alt="plot of chunk tab-dimension-reduction-by-depth-2" width="100%" /></p>

</div>
<div id='tab-dimension-reduction-by-depth-3'>
<pre><code class="r">par(mfrow = c(1, 2))
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 9645),
    method = &quot;UMAP&quot;, top_value_method = &quot;SD&quot;, top_n = 40000, scale_rows = FALSE)
dimension_reduction(res_rh, merge_node = merge_node_param(min_n_signatures = 9645),
    method = &quot;UMAP&quot;, top_value_method = &quot;ATC&quot;, top_n = 40000, scale_rows = TRUE)
</code></pre>

<p><img src="figure_cola/tab-dimension-reduction-by-depth-3-1.png" title="plot of chunk tab-dimension-reduction-by-depth-3" alt="plot of chunk tab-dimension-reduction-by-depth-3" width="100%" /></p>

</div>
</div>




### Signature heatmap

Signatures on the heatmap are the union of all signatures found on every node
on the hierarchy. The number of k-means on rows are automatically selected by the function.




<script>
$( function() {
	$( '#tabs-get-signatures-from-hierarchical-partition' ).tabs();
} );
</script>
<div id='tabs-get-signatures-from-hierarchical-partition'>
<ul>
<li><a href='#tab-get-signatures-from-hierarchical-partition-1'>n_signatures ≥ 1384</a></li>
<li><a href='#tab-get-signatures-from-hierarchical-partition-2'>n_signatures ≥ 9467</a></li>
<li><a href='#tab-get-signatures-from-hierarchical-partition-3'>n_signatures ≥ 9645</a></li>
</ul>
<div id='tab-get-signatures-from-hierarchical-partition-1'>
<pre><code class="r">get_signatures(res_rh, merge_node = merge_node_param(min_n_signatures = 1384))
</code></pre>

<p><img src="figure_cola/tab-get-signatures-from-hierarchical-partition-1-1.png" alt="plot of chunk tab-get-signatures-from-hierarchical-partition-1"/></p>

</div>
<div id='tab-get-signatures-from-hierarchical-partition-2'>
<pre><code class="r">get_signatures(res_rh, merge_node = merge_node_param(min_n_signatures = 9467))
</code></pre>

<p><img src="figure_cola/tab-get-signatures-from-hierarchical-partition-2-1.png" alt="plot of chunk tab-get-signatures-from-hierarchical-partition-2"/></p>

</div>
<div id='tab-get-signatures-from-hierarchical-partition-3'>
<pre><code class="r">get_signatures(res_rh, merge_node = merge_node_param(min_n_signatures = 9645))
</code></pre>

<p><img src="figure_cola/tab-get-signatures-from-hierarchical-partition-3-1.png" alt="plot of chunk tab-get-signatures-from-hierarchical-partition-3"/></p>

</div>
</div>




Compare signatures from different nodes:


```r
compare_signatures(res_rh, verbose = FALSE)
```

![plot of chunk unnamed-chunk-24](figure_cola/unnamed-chunk-24-1.png)

If there are too many signatures, `top_signatures = ...` can be set to only show the 
signatures with the highest FDRs. Note it only works on every node and the final signatures
are the union of all signatures of all nodes.


```r
# code only for demonstration
# e.g. to show the top 500 most significant rows on each node.
tb = get_signature(res_rh, top_signatures = 500)
```


## Results for each node


---------------------------------------------------




### Node0


Child nodes: 
                Node01-leaf
        ,
                [Node02](#Node02)
        ,
                Node03-leaf
        .







The object with results only for a single top-value method and a single partitioning method 
can be extracted as:

```r
res = res_rh["0"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6, 7, 8.
#>   On a matrix with 30000 rows and 66 columns.
#>   Top rows (1000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 350 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_partitions"     
#>  [7] "compare_signatures"      "consensus_heatmap"       "dimension_reduction"    
#> [10] "functional_enrichment"   "get_anno_col"            "get_anno"               
#> [13] "get_classes"             "get_consensus"           "get_matrix"             
#> [16] "get_membership"          "get_param"               "get_signatures"         
#> [19] "get_stats"               "is_best_k"               "is_stable_k"            
#> [22] "membership_heatmap"      "ncol"                    "nrow"                   
#> [25] "plot_ecdf"               "predict_classes"         "rownames"               
#> [28] "select_partition_number" "show"                    "suggest_best_k"         
#> [31] "test_to_known_factors"   "top_rows_heatmap"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of subgroups)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk node-0-collect-plots](figure_cola/node-0-collect-plots-1.png)

The plots are:

- The first row: a plot of the eCDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- eCDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus subgroup labels in all
  partitions.
- Area increased. Denote $A_k$ as the area under the eCDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](https://jokergoo.github.io/cola_vignettes/cola.html#toc_13).

Generally speaking, higher 1-PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk node-0-select-partition-number](figure_cola/node-0-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.2171 0.784   0.784
#> 3 3 1.000           0.999       0.999         1.2576 0.727   0.652
#> 4 4 0.847           0.890       0.946         0.3343 0.837   0.681
#> 5 5 0.827           0.850       0.925         0.0448 0.990   0.971
#> 6 6 0.759           0.683       0.868         0.0325 0.975   0.926
#> 7 7 0.733           0.659       0.845         0.0316 0.941   0.824
#> 8 8 0.716           0.629       0.822         0.0277 0.918   0.735
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following is the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall subgroup
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-node-0-get-classes' ).tabs();
} );
</script>
<div id='tabs-node-0-get-classes'>
<ul>
<li><a href='#tab-node-0-get-classes-1'>k = 2</a></li>
<li><a href='#tab-node-0-get-classes-2'>k = 3</a></li>
<li><a href='#tab-node-0-get-classes-3'>k = 4</a></li>
<li><a href='#tab-node-0-get-classes-4'>k = 5</a></li>
<li><a href='#tab-node-0-get-classes-5'>k = 6</a></li>
<li><a href='#tab-node-0-get-classes-6'>k = 7</a></li>
<li><a href='#tab-node-0-get-classes-7'>k = 8</a></li>
</ul>

<div id='tab-node-0-get-classes-1'>
<p><a id='tab-node-0-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette p1 p2
#&gt; TCGA.KL.8323.01     2       0          1  0  1
#&gt; TCGA.KL.8332.01     2       0          1  0  1
#&gt; TCGA.KL.8330.01     2       0          1  0  1
#&gt; TCGA.KM.8443.01     2       0          1  0  1
#&gt; TCGA.KL.8339.01     2       0          1  0  1
#&gt; TCGA.KN.8428.01     2       0          1  0  1
#&gt; TCGA.KL.8326.01     2       0          1  0  1
#&gt; TCGA.KM.8476.01     1       0          1  1  0
#&gt; TCGA.KN.8429.01     2       0          1  0  1
#&gt; TCGA.KO.8408.01     2       0          1  0  1
#&gt; TCGA.KN.8425.01     2       0          1  0  1
#&gt; TCGA.KO.8414.01     2       0          1  0  1
#&gt; TCGA.KN.8436.01     2       0          1  0  1
#&gt; TCGA.KL.8342.01     1       0          1  1  0
#&gt; TCGA.KM.8440.01     2       0          1  0  1
#&gt; TCGA.KO.8410.01     2       0          1  0  1
#&gt; TCGA.KL.8325.01     2       0          1  0  1
#&gt; TCGA.KL.8340.01     2       0          1  0  1
#&gt; TCGA.KL.8327.01     1       0          1  1  0
#&gt; TCGA.KN.8437.01     2       0          1  0  1
#&gt; TCGA.KL.8344.01     2       0          1  0  1
#&gt; TCGA.KN.8435.01     2       0          1  0  1
#&gt; TCGA.KO.8415.01     2       0          1  0  1
#&gt; TCGA.KO.8411.01     1       0          1  1  0
#&gt; TCGA.KO.8404.01     2       0          1  0  1
#&gt; TCGA.KN.8427.01     2       0          1  0  1
#&gt; TCGA.KN.8423.01     2       0          1  0  1
#&gt; TCGA.KL.8337.01     2       0          1  0  1
#&gt; TCGA.KO.8405.01     2       0          1  0  1
#&gt; TCGA.KN.8424.01     2       0          1  0  1
#&gt; TCGA.KN.8426.01     2       0          1  0  1
#&gt; TCGA.KM.8442.01     2       0          1  0  1
#&gt; TCGA.KM.8441.01     2       0          1  0  1
#&gt; TCGA.KM.8477.01     2       0          1  0  1
#&gt; TCGA.KM.8439.01     2       0          1  0  1
#&gt; TCGA.KL.8346.01     2       0          1  0  1
#&gt; TCGA.KL.8335.01     2       0          1  0  1
#&gt; TCGA.KM.8438.01     2       0          1  0  1
#&gt; TCGA.KO.8413.01     2       0          1  0  1
#&gt; TCGA.KL.8331.01     2       0          1  0  1
#&gt; TCGA.KL.8345.01     1       0          1  1  0
#&gt; TCGA.KN.8432.01     2       0          1  0  1
#&gt; TCGA.KM.8639.01     2       0          1  0  1
#&gt; TCGA.KN.8419.01     1       0          1  1  0
#&gt; TCGA.KN.8421.01     2       0          1  0  1
#&gt; TCGA.KO.8403.01     1       0          1  1  0
#&gt; TCGA.KL.8336.01     2       0          1  0  1
#&gt; TCGA.KL.8334.01     2       0          1  0  1
#&gt; TCGA.KO.8409.01     2       0          1  0  1
#&gt; TCGA.KO.8407.01     2       0          1  0  1
#&gt; TCGA.KN.8422.01     2       0          1  0  1
#&gt; TCGA.KN.8418.01     2       0          1  0  1
#&gt; TCGA.KO.8406.01     1       0          1  1  0
#&gt; TCGA.KO.8417.01     2       0          1  0  1
#&gt; TCGA.KL.8343.01     2       0          1  0  1
#&gt; TCGA.KN.8430.01     2       0          1  0  1
#&gt; TCGA.KL.8341.01     2       0          1  0  1
#&gt; TCGA.KL.8328.01     2       0          1  0  1
#&gt; TCGA.KN.8434.01     2       0          1  0  1
#&gt; TCGA.KL.8324.01     2       0          1  0  1
#&gt; TCGA.KO.8416.01     2       0          1  0  1
#&gt; TCGA.KL.8333.01     2       0          1  0  1
#&gt; TCGA.KL.8329.01     2       0          1  0  1
#&gt; TCGA.KL.8338.01     2       0          1  0  1
#&gt; TCGA.KN.8433.01     2       0          1  0  1
#&gt; TCGA.KN.8431.01     2       0          1  0  1
</code></pre>

<script>
$('#tab-node-0-get-classes-1-a').parent().next().next().hide();
$('#tab-node-0-get-classes-1-a').click(function(){
  $('#tab-node-0-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-0-get-classes-2'>
<p><a id='tab-node-0-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette p1   p2   p3
#&gt; TCGA.KL.8323.01     3   0.000      1.000  0 0.00 1.00
#&gt; TCGA.KL.8332.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8330.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KM.8443.01     3   0.000      1.000  0 0.00 1.00
#&gt; TCGA.KL.8339.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KN.8428.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8326.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KM.8476.01     1   0.000      1.000  1 0.00 0.00
#&gt; TCGA.KN.8429.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KO.8408.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KN.8425.01     3   0.000      1.000  0 0.00 1.00
#&gt; TCGA.KO.8414.01     3   0.000      1.000  0 0.00 1.00
#&gt; TCGA.KN.8436.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8342.01     1   0.000      1.000  1 0.00 0.00
#&gt; TCGA.KM.8440.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KO.8410.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8325.01     3   0.000      1.000  0 0.00 1.00
#&gt; TCGA.KL.8340.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8327.01     1   0.000      1.000  1 0.00 0.00
#&gt; TCGA.KN.8437.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8344.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KN.8435.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KO.8415.01     3   0.000      1.000  0 0.00 1.00
#&gt; TCGA.KO.8411.01     1   0.000      1.000  1 0.00 0.00
#&gt; TCGA.KO.8404.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KN.8427.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KN.8423.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8337.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KO.8405.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KN.8424.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KN.8426.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KM.8442.01     3   0.000      1.000  0 0.00 1.00
#&gt; TCGA.KM.8441.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KM.8477.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KM.8439.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8346.01     3   0.000      1.000  0 0.00 1.00
#&gt; TCGA.KL.8335.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KM.8438.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KO.8413.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8331.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8345.01     1   0.000      1.000  1 0.00 0.00
#&gt; TCGA.KN.8432.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KM.8639.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KN.8419.01     1   0.000      1.000  1 0.00 0.00
#&gt; TCGA.KN.8421.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KO.8403.01     1   0.000      1.000  1 0.00 0.00
#&gt; TCGA.KL.8336.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8334.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KO.8409.01     3   0.000      1.000  0 0.00 1.00
#&gt; TCGA.KO.8407.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KN.8422.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KN.8418.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KO.8406.01     1   0.000      1.000  1 0.00 0.00
#&gt; TCGA.KO.8417.01     3   0.000      1.000  0 0.00 1.00
#&gt; TCGA.KL.8343.01     3   0.000      1.000  0 0.00 1.00
#&gt; TCGA.KN.8430.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8341.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8328.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KN.8434.01     3   0.000      1.000  0 0.00 1.00
#&gt; TCGA.KL.8324.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KO.8416.01     3   0.000      1.000  0 0.00 1.00
#&gt; TCGA.KL.8333.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8329.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KL.8338.01     2   0.000      0.999  0 1.00 0.00
#&gt; TCGA.KN.8433.01     2   0.153      0.957  0 0.96 0.04
#&gt; TCGA.KN.8431.01     2   0.000      0.999  0 1.00 0.00
</code></pre>

<script>
$('#tab-node-0-get-classes-2-a').parent().next().next().hide();
$('#tab-node-0-get-classes-2-a').click(function(){
  $('#tab-node-0-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-0-get-classes-3'>
<p><a id='tab-node-0-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette p1   p2   p3   p4
#&gt; TCGA.KL.8323.01     3  0.0707     0.8682  0 0.00 0.98 0.02
#&gt; TCGA.KL.8332.01     2  0.3610     0.7612  0 0.80 0.00 0.20
#&gt; TCGA.KL.8330.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KM.8443.01     3  0.0000     0.8738  0 0.00 1.00 0.00
#&gt; TCGA.KL.8339.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KN.8428.01     2  0.4994    -0.0418  0 0.52 0.00 0.48
#&gt; TCGA.KL.8326.01     2  0.3801     0.7360  0 0.78 0.00 0.22
#&gt; TCGA.KM.8476.01     1  0.0000     1.0000  1 0.00 0.00 0.00
#&gt; TCGA.KN.8429.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KO.8408.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KN.8425.01     3  0.3400     0.8095  0 0.00 0.82 0.18
#&gt; TCGA.KO.8414.01     3  0.4079     0.8010  0 0.02 0.80 0.18
#&gt; TCGA.KN.8436.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KL.8342.01     1  0.0000     1.0000  1 0.00 0.00 0.00
#&gt; TCGA.KM.8440.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KO.8410.01     4  0.4522     0.5348  0 0.32 0.00 0.68
#&gt; TCGA.KL.8325.01     3  0.0000     0.8738  0 0.00 1.00 0.00
#&gt; TCGA.KL.8340.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KL.8327.01     1  0.0000     1.0000  1 0.00 0.00 0.00
#&gt; TCGA.KN.8437.01     4  0.1211     0.9392  0 0.04 0.00 0.96
#&gt; TCGA.KL.8344.01     2  0.2647     0.8493  0 0.88 0.00 0.12
#&gt; TCGA.KN.8435.01     2  0.0707     0.9318  0 0.98 0.00 0.02
#&gt; TCGA.KO.8415.01     3  0.0707     0.8682  0 0.00 0.98 0.02
#&gt; TCGA.KO.8411.01     1  0.0000     1.0000  1 0.00 0.00 0.00
#&gt; TCGA.KO.8404.01     4  0.1211     0.9392  0 0.04 0.00 0.96
#&gt; TCGA.KN.8427.01     4  0.0707     0.9258  0 0.02 0.00 0.98
#&gt; TCGA.KN.8423.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KL.8337.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KO.8405.01     4  0.1211     0.9392  0 0.04 0.00 0.96
#&gt; TCGA.KN.8424.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KN.8426.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KM.8442.01     3  0.0000     0.8738  0 0.00 1.00 0.00
#&gt; TCGA.KM.8441.01     4  0.1211     0.9392  0 0.04 0.00 0.96
#&gt; TCGA.KM.8477.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KM.8439.01     4  0.1211     0.9392  0 0.04 0.00 0.96
#&gt; TCGA.KL.8346.01     3  0.5062     0.5256  0 0.30 0.68 0.02
#&gt; TCGA.KL.8335.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KM.8438.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KO.8413.01     2  0.3801     0.7357  0 0.78 0.00 0.22
#&gt; TCGA.KL.8331.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KL.8345.01     1  0.0000     1.0000  1 0.00 0.00 0.00
#&gt; TCGA.KN.8432.01     2  0.1211     0.9197  0 0.96 0.00 0.04
#&gt; TCGA.KM.8639.01     4  0.1211     0.9392  0 0.04 0.00 0.96
#&gt; TCGA.KN.8419.01     1  0.0000     1.0000  1 0.00 0.00 0.00
#&gt; TCGA.KN.8421.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KO.8403.01     1  0.0000     1.0000  1 0.00 0.00 0.00
#&gt; TCGA.KL.8336.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KL.8334.01     2  0.3172     0.8104  0 0.84 0.00 0.16
#&gt; TCGA.KO.8409.01     3  0.0000     0.8738  0 0.00 1.00 0.00
#&gt; TCGA.KO.8407.01     2  0.3400     0.7871  0 0.82 0.00 0.18
#&gt; TCGA.KN.8422.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KN.8418.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KO.8406.01     1  0.0000     1.0000  1 0.00 0.00 0.00
#&gt; TCGA.KO.8417.01     3  0.3335     0.8388  0 0.02 0.86 0.12
#&gt; TCGA.KL.8343.01     3  0.3400     0.8095  0 0.00 0.82 0.18
#&gt; TCGA.KN.8430.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KL.8341.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KL.8328.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KN.8434.01     3  0.4553     0.7843  0 0.04 0.78 0.18
#&gt; TCGA.KL.8324.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KO.8416.01     3  0.0000     0.8738  0 0.00 1.00 0.00
#&gt; TCGA.KL.8333.01     4  0.0707     0.9258  0 0.02 0.00 0.98
#&gt; TCGA.KL.8329.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KL.8338.01     2  0.0000     0.9467  0 1.00 0.00 0.00
#&gt; TCGA.KN.8433.01     4  0.0707     0.9258  0 0.02 0.00 0.98
#&gt; TCGA.KN.8431.01     2  0.0000     0.9467  0 1.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-0-get-classes-3-a').parent().next().next().hide();
$('#tab-node-0-get-classes-3-a').click(function(){
  $('#tab-node-0-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-0-get-classes-4'>
<p><a id='tab-node-0-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette p1   p2   p3   p4   p5
#&gt; TCGA.KL.8323.01     5  0.1732      1.000  0 0.00 0.08 0.00 0.92
#&gt; TCGA.KL.8332.01     2  0.4872      0.721  0 0.72 0.16 0.12 0.00
#&gt; TCGA.KL.8330.01     2  0.1410      0.894  0 0.94 0.06 0.00 0.00
#&gt; TCGA.KM.8443.01     3  0.3796      0.588  0 0.00 0.70 0.00 0.30
#&gt; TCGA.KL.8339.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KN.8428.01     2  0.4227      0.287  0 0.58 0.00 0.42 0.00
#&gt; TCGA.KL.8326.01     2  0.5273      0.666  0 0.68 0.16 0.16 0.00
#&gt; TCGA.KM.8476.01     1  0.0000      1.000  1 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8429.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KO.8408.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KN.8425.01     3  0.2012      0.734  0 0.00 0.92 0.06 0.02
#&gt; TCGA.KO.8414.01     3  0.1043      0.741  0 0.00 0.96 0.04 0.00
#&gt; TCGA.KN.8436.01     2  0.1732      0.884  0 0.92 0.08 0.00 0.00
#&gt; TCGA.KL.8342.01     1  0.0000      1.000  1 0.00 0.00 0.00 0.00
#&gt; TCGA.KM.8440.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KO.8410.01     4  0.3796      0.415  0 0.30 0.00 0.70 0.00
#&gt; TCGA.KL.8325.01     3  0.2929      0.739  0 0.00 0.82 0.00 0.18
#&gt; TCGA.KL.8340.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KL.8327.01     1  0.0000      1.000  1 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8437.01     4  0.0000      0.936  0 0.00 0.00 1.00 0.00
#&gt; TCGA.KL.8344.01     2  0.3319      0.814  0 0.82 0.16 0.02 0.00
#&gt; TCGA.KN.8435.01     2  0.2516      0.844  0 0.86 0.14 0.00 0.00
#&gt; TCGA.KO.8415.01     5  0.1732      1.000  0 0.00 0.08 0.00 0.92
#&gt; TCGA.KO.8411.01     1  0.0000      1.000  1 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8404.01     4  0.0000      0.936  0 0.00 0.00 1.00 0.00
#&gt; TCGA.KN.8427.01     4  0.0000      0.936  0 0.00 0.00 1.00 0.00
#&gt; TCGA.KN.8423.01     2  0.0609      0.913  0 0.98 0.02 0.00 0.00
#&gt; TCGA.KL.8337.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KO.8405.01     4  0.0000      0.936  0 0.00 0.00 1.00 0.00
#&gt; TCGA.KN.8424.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KN.8426.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KM.8442.01     3  0.2732      0.745  0 0.00 0.84 0.00 0.16
#&gt; TCGA.KM.8441.01     4  0.0000      0.936  0 0.00 0.00 1.00 0.00
#&gt; TCGA.KM.8477.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KM.8439.01     4  0.0000      0.936  0 0.00 0.00 1.00 0.00
#&gt; TCGA.KL.8346.01     3  0.5599      0.301  0 0.26 0.62 0.00 0.12
#&gt; TCGA.KL.8335.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KM.8438.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KO.8413.01     2  0.5680      0.571  0 0.62 0.14 0.24 0.00
#&gt; TCGA.KL.8331.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KL.8345.01     1  0.0000      1.000  1 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8432.01     2  0.2732      0.829  0 0.84 0.16 0.00 0.00
#&gt; TCGA.KM.8639.01     4  0.0000      0.936  0 0.00 0.00 1.00 0.00
#&gt; TCGA.KN.8419.01     1  0.0000      1.000  1 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8421.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KO.8403.01     1  0.0000      1.000  1 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8336.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KL.8334.01     2  0.4075      0.780  0 0.78 0.16 0.06 0.00
#&gt; TCGA.KO.8409.01     3  0.2929      0.739  0 0.00 0.82 0.00 0.18
#&gt; TCGA.KO.8407.01     2  0.5245      0.598  0 0.64 0.28 0.08 0.00
#&gt; TCGA.KN.8422.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KN.8418.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KO.8406.01     1  0.0000      1.000  1 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8417.01     3  0.0000      0.745  0 0.00 1.00 0.00 0.00
#&gt; TCGA.KL.8343.01     3  0.5136      0.516  0 0.00 0.66 0.26 0.08
#&gt; TCGA.KN.8430.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KL.8341.01     2  0.1410      0.893  0 0.94 0.06 0.00 0.00
#&gt; TCGA.KL.8328.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KN.8434.01     3  0.1043      0.741  0 0.00 0.96 0.04 0.00
#&gt; TCGA.KL.8324.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KO.8416.01     3  0.2516      0.738  0 0.00 0.86 0.00 0.14
#&gt; TCGA.KL.8333.01     4  0.0000      0.936  0 0.00 0.00 1.00 0.00
#&gt; TCGA.KL.8329.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KL.8338.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
#&gt; TCGA.KN.8433.01     4  0.0000      0.936  0 0.00 0.00 1.00 0.00
#&gt; TCGA.KN.8431.01     2  0.0000      0.921  0 1.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-0-get-classes-4-a').parent().next().next().hide();
$('#tab-node-0-get-classes-4-a').click(function(){
  $('#tab-node-0-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-0-get-classes-5'>
<p><a id='tab-node-0-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6
#&gt; TCGA.KL.8323.01     5  0.3351     0.9441 0.00 0.00 0.16 0.00 0.80 0.04
#&gt; TCGA.KL.8332.01     2  0.6394    -0.0384 0.00 0.40 0.02 0.36 0.00 0.22
#&gt; TCGA.KL.8330.01     2  0.1556     0.7806 0.00 0.92 0.00 0.00 0.00 0.08
#&gt; TCGA.KM.8443.01     3  0.3523     0.3217 0.00 0.00 0.78 0.00 0.18 0.04
#&gt; TCGA.KL.8339.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8428.01     2  0.3828     0.1537 0.00 0.56 0.00 0.44 0.00 0.00
#&gt; TCGA.KL.8326.01     2  0.6539    -0.0697 0.00 0.40 0.04 0.38 0.00 0.18
#&gt; TCGA.KM.8476.01     1  0.0000     0.9779 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8429.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8408.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8425.01     3  0.5419     0.5394 0.00 0.00 0.58 0.22 0.00 0.20
#&gt; TCGA.KO.8414.01     3  0.5530     0.5199 0.00 0.00 0.56 0.22 0.00 0.22
#&gt; TCGA.KN.8436.01     2  0.2048     0.7449 0.00 0.88 0.00 0.00 0.00 0.12
#&gt; TCGA.KL.8342.01     1  0.0000     0.9779 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KM.8440.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8410.01     4  0.3198     0.5043 0.00 0.26 0.00 0.74 0.00 0.00
#&gt; TCGA.KL.8325.01     3  0.1556     0.5217 0.00 0.00 0.92 0.00 0.00 0.08
#&gt; TCGA.KL.8340.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8327.01     1  0.0000     0.9779 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8437.01     4  0.0937     0.8493 0.00 0.04 0.00 0.96 0.00 0.00
#&gt; TCGA.KL.8344.01     2  0.6002     0.2653 0.00 0.54 0.02 0.24 0.00 0.20
#&gt; TCGA.KN.8435.01     2  0.5261     0.5056 0.00 0.68 0.02 0.08 0.02 0.20
#&gt; TCGA.KO.8415.01     5  0.2631     0.9444 0.00 0.00 0.18 0.00 0.82 0.00
#&gt; TCGA.KO.8411.01     1  0.0000     0.9779 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8404.01     4  0.1807     0.7390 0.00 0.00 0.00 0.92 0.02 0.06
#&gt; TCGA.KN.8427.01     4  0.1807     0.7390 0.00 0.00 0.00 0.92 0.02 0.06
#&gt; TCGA.KN.8423.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8337.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8405.01     4  0.0937     0.8493 0.00 0.04 0.00 0.96 0.00 0.00
#&gt; TCGA.KN.8424.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8426.01     2  0.0547     0.8161 0.00 0.98 0.00 0.00 0.00 0.02
#&gt; TCGA.KM.8442.01     3  0.1814     0.5574 0.00 0.00 0.90 0.00 0.00 0.10
#&gt; TCGA.KM.8441.01     4  0.0937     0.8493 0.00 0.04 0.00 0.96 0.00 0.00
#&gt; TCGA.KM.8477.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KM.8439.01     4  0.0937     0.8493 0.00 0.04 0.00 0.96 0.00 0.00
#&gt; TCGA.KL.8346.01     6  0.6658     0.0000 0.00 0.16 0.10 0.02 0.14 0.58
#&gt; TCGA.KL.8335.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KM.8438.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8413.01     4  0.5906     0.1878 0.00 0.32 0.02 0.52 0.00 0.14
#&gt; TCGA.KL.8331.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8345.01     1  0.0000     0.9779 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8432.01     2  0.5748     0.3406 0.00 0.58 0.02 0.16 0.00 0.24
#&gt; TCGA.KM.8639.01     4  0.0937     0.8493 0.00 0.04 0.00 0.96 0.00 0.00
#&gt; TCGA.KN.8419.01     1  0.3258     0.8290 0.84 0.00 0.00 0.04 0.02 0.10
#&gt; TCGA.KN.8421.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8403.01     1  0.0000     0.9779 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8336.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8334.01     2  0.5919     0.2601 0.00 0.54 0.02 0.28 0.00 0.16
#&gt; TCGA.KO.8409.01     3  0.0000     0.5727 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.KO.8407.01     2  0.7679    -0.2821 0.00 0.30 0.20 0.24 0.00 0.26
#&gt; TCGA.KN.8422.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8418.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8406.01     1  0.0000     0.9779 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8417.01     3  0.4247     0.5559 0.00 0.00 0.70 0.06 0.00 0.24
#&gt; TCGA.KL.8343.01     3  0.5626     0.4352 0.00 0.00 0.54 0.34 0.02 0.10
#&gt; TCGA.KN.8430.01     2  0.1480     0.7942 0.00 0.94 0.00 0.00 0.02 0.04
#&gt; TCGA.KL.8341.01     2  0.2728     0.7218 0.00 0.86 0.00 0.04 0.00 0.10
#&gt; TCGA.KL.8328.01     2  0.0547     0.8167 0.00 0.98 0.00 0.00 0.00 0.02
#&gt; TCGA.KN.8434.01     3  0.6002     0.4890 0.00 0.02 0.54 0.24 0.00 0.20
#&gt; TCGA.KL.8324.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8416.01     3  0.0547     0.5774 0.00 0.00 0.98 0.00 0.00 0.02
#&gt; TCGA.KL.8333.01     4  0.0937     0.8493 0.00 0.04 0.00 0.96 0.00 0.00
#&gt; TCGA.KL.8329.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8338.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8433.01     4  0.1092     0.8275 0.00 0.02 0.00 0.96 0.02 0.00
#&gt; TCGA.KN.8431.01     2  0.0000     0.8270 0.00 1.00 0.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-0-get-classes-5-a').parent().next().next().hide();
$('#tab-node-0-get-classes-5-a').click(function(){
  $('#tab-node-0-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-0-get-classes-6'>
<p><a id='tab-node-0-get-classes-6-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 7), get_membership(res, k = 7))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette  p1   p2   p3   p4   p5   p6   p7
#&gt; TCGA.KL.8323.01     5  0.0504     0.9091 0.0 0.00 0.02 0.00 0.98 0.00 0.00
#&gt; TCGA.KL.8332.01     4  0.6400     0.0582 0.0 0.02 0.28 0.36 0.00 0.02 0.32
#&gt; TCGA.KL.8330.01     7  0.3350     0.7621 0.0 0.02 0.12 0.02 0.00 0.02 0.82
#&gt; TCGA.KM.8443.01     3  0.6187     0.2704 0.0 0.28 0.48 0.00 0.16 0.08 0.00
#&gt; TCGA.KL.8339.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KN.8428.01     7  0.3294     0.4542 0.0 0.00 0.00 0.34 0.00 0.00 0.66
#&gt; TCGA.KL.8326.01     4  0.6292     0.1942 0.0 0.02 0.28 0.48 0.00 0.04 0.18
#&gt; TCGA.KM.8476.01     1  0.0000     0.9283 1.0 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8429.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KO.8408.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KN.8425.01     3  0.3734     0.4747 0.0 0.04 0.78 0.14 0.00 0.04 0.00
#&gt; TCGA.KO.8414.01     3  0.3396     0.4591 0.0 0.02 0.80 0.14 0.00 0.00 0.04
#&gt; TCGA.KN.8436.01     7  0.3864     0.7021 0.0 0.02 0.18 0.02 0.00 0.02 0.76
#&gt; TCGA.KL.8342.01     1  0.0000     0.9283 1.0 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KM.8440.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KO.8410.01     4  0.2945     0.4895 0.0 0.00 0.00 0.74 0.00 0.00 0.26
#&gt; TCGA.KL.8325.01     3  0.5731     0.2821 0.0 0.32 0.50 0.00 0.04 0.14 0.00
#&gt; TCGA.KL.8340.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KL.8327.01     1  0.0000     0.9283 1.0 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8437.01     4  0.0504     0.7154 0.0 0.00 0.00 0.98 0.00 0.00 0.02
#&gt; TCGA.KL.8344.01     7  0.6183     0.1053 0.0 0.02 0.22 0.28 0.00 0.02 0.46
#&gt; TCGA.KN.8435.01     7  0.4107     0.6280 0.0 0.00 0.24 0.04 0.00 0.02 0.70
#&gt; TCGA.KO.8415.01     5  0.1433     0.9093 0.0 0.08 0.00 0.00 0.92 0.00 0.00
#&gt; TCGA.KO.8411.01     1  0.0000     0.9283 1.0 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8404.01     4  0.3139     0.4471 0.0 0.30 0.00 0.70 0.00 0.00 0.00
#&gt; TCGA.KN.8427.01     4  0.3047     0.4624 0.0 0.28 0.00 0.72 0.00 0.00 0.00
#&gt; TCGA.KN.8423.01     7  0.1664     0.8444 0.0 0.00 0.06 0.00 0.00 0.02 0.92
#&gt; TCGA.KL.8337.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KO.8405.01     4  0.1006     0.7082 0.0 0.00 0.00 0.96 0.00 0.02 0.02
#&gt; TCGA.KN.8424.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KN.8426.01     7  0.0504     0.8775 0.0 0.00 0.00 0.00 0.00 0.02 0.98
#&gt; TCGA.KM.8442.01     3  0.4055     0.4539 0.0 0.18 0.74 0.00 0.04 0.04 0.00
#&gt; TCGA.KM.8441.01     4  0.0504     0.7154 0.0 0.00 0.00 0.98 0.00 0.00 0.02
#&gt; TCGA.KM.8477.01     7  0.1671     0.8162 0.0 0.00 0.00 0.10 0.00 0.00 0.90
#&gt; TCGA.KM.8439.01     4  0.0504     0.7154 0.0 0.00 0.00 0.98 0.00 0.00 0.02
#&gt; TCGA.KL.8346.01     6  0.2016     0.0000 0.0 0.00 0.06 0.00 0.00 0.90 0.04
#&gt; TCGA.KL.8335.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KM.8438.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KO.8413.01     4  0.5951     0.2996 0.0 0.02 0.22 0.56 0.00 0.04 0.16
#&gt; TCGA.KL.8331.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KL.8345.01     1  0.0000     0.9283 1.0 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8432.01     7  0.5822     0.3153 0.0 0.02 0.30 0.14 0.00 0.02 0.52
#&gt; TCGA.KM.8639.01     4  0.0504     0.7154 0.0 0.00 0.00 0.98 0.00 0.00 0.02
#&gt; TCGA.KN.8419.01     1  0.3994     0.2724 0.5 0.48 0.00 0.00 0.00 0.02 0.00
#&gt; TCGA.KN.8421.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KO.8403.01     1  0.0000     0.9283 1.0 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8336.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KL.8334.01     7  0.5604     0.0784 0.0 0.00 0.16 0.34 0.00 0.02 0.48
#&gt; TCGA.KO.8409.01     3  0.4305     0.4194 0.0 0.28 0.66 0.00 0.04 0.02 0.00
#&gt; TCGA.KO.8407.01     3  0.6464    -0.0099 0.0 0.04 0.42 0.32 0.00 0.02 0.20
#&gt; TCGA.KN.8422.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KN.8418.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KO.8406.01     1  0.0000     0.9283 1.0 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8417.01     3  0.3000     0.4491 0.0 0.06 0.86 0.04 0.00 0.02 0.02
#&gt; TCGA.KL.8343.01     3  0.6717     0.2240 0.0 0.06 0.40 0.38 0.08 0.08 0.00
#&gt; TCGA.KN.8430.01     7  0.1166     0.8585 0.0 0.00 0.00 0.00 0.00 0.06 0.94
#&gt; TCGA.KL.8341.01     7  0.3000     0.7848 0.0 0.00 0.10 0.04 0.00 0.02 0.84
#&gt; TCGA.KL.8328.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KN.8434.01     3  0.3991     0.4189 0.0 0.00 0.72 0.22 0.00 0.02 0.04
#&gt; TCGA.KL.8324.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KO.8416.01     3  0.5025     0.4182 0.0 0.22 0.64 0.00 0.10 0.04 0.00
#&gt; TCGA.KL.8333.01     4  0.0504     0.7154 0.0 0.00 0.00 0.98 0.00 0.00 0.02
#&gt; TCGA.KL.8329.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KL.8338.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
#&gt; TCGA.KN.8433.01     4  0.0000     0.6981 0.0 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.KN.8431.01     7  0.0000     0.8875 0.0 0.00 0.00 0.00 0.00 0.00 1.00
</code></pre>

<script>
$('#tab-node-0-get-classes-6-a').parent().next().next().hide();
$('#tab-node-0-get-classes-6-a').click(function(){
  $('#tab-node-0-get-classes-6-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-0-get-classes-7'>
<p><a id='tab-node-0-get-classes-7-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 8), get_membership(res, k = 8))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6   p7   p8
#&gt; TCGA.KL.8323.01     5  0.1091    0.75410 0.00 0.00 0.00 0.00 0.94 0.00 0.00 0.06
#&gt; TCGA.KL.8332.01     3  0.5386    0.51670 0.00 0.02 0.48 0.22 0.00 0.00 0.28 0.00
#&gt; TCGA.KL.8330.01     7  0.3744    0.62933 0.00 0.06 0.18 0.00 0.00 0.02 0.74 0.00
#&gt; TCGA.KM.8443.01     8  0.3763    0.06538 0.00 0.08 0.02 0.00 0.10 0.02 0.00 0.78
#&gt; TCGA.KL.8339.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KN.8428.01     7  0.4105    0.10798 0.00 0.02 0.00 0.42 0.00 0.02 0.54 0.00
#&gt; TCGA.KL.8326.01     3  0.5455    0.47635 0.00 0.02 0.46 0.28 0.00 0.00 0.24 0.00
#&gt; TCGA.KM.8476.01     1  0.0000    0.93837 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8429.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KO.8408.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KN.8425.01     3  0.5292   -0.14092 0.00 0.00 0.44 0.16 0.02 0.00 0.00 0.38
#&gt; TCGA.KO.8414.01     3  0.5025   -0.00229 0.00 0.04 0.56 0.10 0.00 0.00 0.00 0.30
#&gt; TCGA.KN.8436.01     7  0.4233    0.29775 0.00 0.04 0.34 0.00 0.00 0.02 0.60 0.00
#&gt; TCGA.KL.8342.01     1  0.0000    0.93837 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KM.8440.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KO.8410.01     4  0.2267    0.58730 0.00 0.00 0.00 0.82 0.00 0.00 0.18 0.00
#&gt; TCGA.KL.8325.01     2  0.5683    0.00000 0.00 0.42 0.16 0.00 0.02 0.02 0.00 0.38
#&gt; TCGA.KL.8340.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KL.8327.01     1  0.0000    0.93837 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8437.01     4  0.0000    0.86606 0.00 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8344.01     3  0.4554    0.35986 0.00 0.00 0.48 0.10 0.00 0.00 0.42 0.00
#&gt; TCGA.KN.8435.01     7  0.5018    0.04671 0.00 0.04 0.38 0.00 0.00 0.04 0.52 0.02
#&gt; TCGA.KO.8415.01     5  0.4204    0.75633 0.00 0.12 0.04 0.00 0.72 0.00 0.00 0.12
#&gt; TCGA.KO.8411.01     1  0.0000    0.93837 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8404.01     4  0.2165    0.78170 0.00 0.06 0.06 0.88 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8427.01     4  0.2165    0.78170 0.00 0.06 0.06 0.88 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8423.01     7  0.2404    0.73891 0.00 0.00 0.14 0.02 0.00 0.00 0.84 0.00
#&gt; TCGA.KL.8337.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KO.8405.01     4  0.0471    0.85510 0.00 0.00 0.02 0.98 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8424.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KN.8426.01     7  0.0941    0.86659 0.00 0.02 0.02 0.00 0.00 0.00 0.96 0.00
#&gt; TCGA.KM.8442.01     8  0.3913    0.31356 0.00 0.04 0.16 0.00 0.00 0.06 0.00 0.74
#&gt; TCGA.KM.8441.01     4  0.0000    0.86606 0.00 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KM.8477.01     7  0.0471    0.87739 0.00 0.00 0.00 0.02 0.00 0.00 0.98 0.00
#&gt; TCGA.KM.8439.01     4  0.0000    0.86606 0.00 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8346.01     6  0.1607    0.00000 0.00 0.00 0.04 0.00 0.00 0.92 0.00 0.04
#&gt; TCGA.KL.8335.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KM.8438.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KO.8413.01     4  0.4897   -0.07669 0.00 0.00 0.28 0.52 0.00 0.00 0.20 0.00
#&gt; TCGA.KL.8331.01     7  0.0471    0.87894 0.00 0.02 0.00 0.00 0.00 0.00 0.98 0.00
#&gt; TCGA.KL.8345.01     1  0.0000    0.93837 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8432.01     3  0.4607    0.30293 0.00 0.00 0.50 0.06 0.00 0.02 0.42 0.00
#&gt; TCGA.KM.8639.01     4  0.0000    0.86606 0.00 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8419.01     1  0.5266    0.39478 0.56 0.30 0.08 0.00 0.04 0.02 0.00 0.00
#&gt; TCGA.KN.8421.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KO.8403.01     1  0.0000    0.93837 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8336.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KL.8334.01     3  0.5073    0.37838 0.00 0.00 0.40 0.20 0.00 0.00 0.40 0.00
#&gt; TCGA.KO.8409.01     8  0.4031    0.32622 0.00 0.10 0.16 0.00 0.00 0.02 0.00 0.72
#&gt; TCGA.KO.8407.01     3  0.4939    0.47775 0.00 0.00 0.62 0.16 0.00 0.04 0.18 0.00
#&gt; TCGA.KN.8422.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KN.8418.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KO.8406.01     1  0.0000    0.93837 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8417.01     3  0.4754   -0.10269 0.00 0.04 0.62 0.02 0.00 0.04 0.00 0.28
#&gt; TCGA.KL.8343.01     3  0.6982   -0.27806 0.00 0.06 0.32 0.26 0.02 0.04 0.00 0.30
#&gt; TCGA.KN.8430.01     7  0.3483    0.64448 0.00 0.02 0.18 0.00 0.00 0.04 0.76 0.00
#&gt; TCGA.KL.8341.01     7  0.4661    0.56599 0.00 0.06 0.16 0.04 0.00 0.04 0.70 0.00
#&gt; TCGA.KL.8328.01     7  0.0471    0.88075 0.00 0.02 0.00 0.00 0.00 0.00 0.98 0.00
#&gt; TCGA.KN.8434.01     3  0.3856    0.14889 0.00 0.00 0.70 0.10 0.00 0.00 0.00 0.20
#&gt; TCGA.KL.8324.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KO.8416.01     8  0.4995    0.39424 0.00 0.06 0.28 0.00 0.04 0.02 0.00 0.60
#&gt; TCGA.KL.8333.01     4  0.0000    0.86606 0.00 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8329.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
#&gt; TCGA.KL.8338.01     7  0.0471    0.87507 0.00 0.00 0.00 0.02 0.00 0.00 0.98 0.00
#&gt; TCGA.KN.8433.01     4  0.0471    0.85791 0.00 0.02 0.00 0.98 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8431.01     7  0.0000    0.89064 0.00 0.00 0.00 0.00 0.00 0.00 1.00 0.00
</code></pre>

<script>
$('#tab-node-0-get-classes-7-a').parent().next().next().hide();
$('#tab-node-0-get-classes-7-a').click(function(){
  $('#tab-node-0-get-classes-7-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.




<script>
$( function() {
	$( '#tabs-node-0-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-0-consensus-heatmap'>
<ul>
<li><a href='#tab-node-0-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-0-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-0-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-0-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-0-consensus-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-0-consensus-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-0-consensus-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-0-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-1-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-1"/></p>

</div>
<div id='tab-node-0-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-2-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-2"/></p>

</div>
<div id='tab-node-0-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-3-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-3"/></p>

</div>
<div id='tab-node-0-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-4-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-4"/></p>

</div>
<div id='tab-node-0-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-5-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-5"/></p>

</div>
<div id='tab-node-0-consensus-heatmap-6'>
<pre><code class="r">consensus_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-6-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-6"/></p>

</div>
<div id='tab-node-0-consensus-heatmap-7'>
<pre><code class="r">consensus_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-0-consensus-heatmap-7-1.png" alt="plot of chunk tab-node-0-consensus-heatmap-7"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:





<script>
$( function() {
	$( '#tabs-node-0-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-0-membership-heatmap'>
<ul>
<li><a href='#tab-node-0-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-0-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-0-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-0-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-0-membership-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-0-membership-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-0-membership-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-0-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-1-1.png" alt="plot of chunk tab-node-0-membership-heatmap-1"/></p>

</div>
<div id='tab-node-0-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-2-1.png" alt="plot of chunk tab-node-0-membership-heatmap-2"/></p>

</div>
<div id='tab-node-0-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-3-1.png" alt="plot of chunk tab-node-0-membership-heatmap-3"/></p>

</div>
<div id='tab-node-0-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-4-1.png" alt="plot of chunk tab-node-0-membership-heatmap-4"/></p>

</div>
<div id='tab-node-0-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-5-1.png" alt="plot of chunk tab-node-0-membership-heatmap-5"/></p>

</div>
<div id='tab-node-0-membership-heatmap-6'>
<pre><code class="r">membership_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-6-1.png" alt="plot of chunk tab-node-0-membership-heatmap-6"/></p>

</div>
<div id='tab-node-0-membership-heatmap-7'>
<pre><code class="r">membership_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-0-membership-heatmap-7-1.png" alt="plot of chunk tab-node-0-membership-heatmap-7"/></p>

</div>
</div>

As soon as the classes for columns are determined, the signatures
that are significantly different between subgroups can be looked for. 
Following are the heatmaps for signatures.






<script>
$( function() {
	$( '#tabs-node-0-get-signatures' ).tabs();
} );
</script>
<div id='tabs-node-0-get-signatures'>
<ul>
<li><a href='#tab-node-0-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-node-0-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-node-0-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-node-0-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-node-0-get-signatures-5'>k = 6</a></li>
<li><a href='#tab-node-0-get-signatures-6'>k = 7</a></li>
<li><a href='#tab-node-0-get-signatures-7'>k = 8</a></li>
</ul>
<div id='tab-node-0-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-1-1.png" alt="plot of chunk tab-node-0-get-signatures-1"/></p>

</div>
<div id='tab-node-0-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-2-1.png" alt="plot of chunk tab-node-0-get-signatures-2"/></p>

</div>
<div id='tab-node-0-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-3-1.png" alt="plot of chunk tab-node-0-get-signatures-3"/></p>

</div>
<div id='tab-node-0-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-4-1.png" alt="plot of chunk tab-node-0-get-signatures-4"/></p>

</div>
<div id='tab-node-0-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-5-1.png" alt="plot of chunk tab-node-0-get-signatures-5"/></p>

</div>
<div id='tab-node-0-get-signatures-6'>
<pre><code class="r">get_signatures(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-6-1.png" alt="plot of chunk tab-node-0-get-signatures-6"/></p>

</div>
<div id='tab-node-0-get-signatures-7'>
<pre><code class="r">get_signatures(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-0-get-signatures-7-1.png" alt="plot of chunk tab-node-0-get-signatures-7"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk node-0-signature_compare](figure_cola/node-0-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. To get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows (which is done by automatically selecting number of clusters).

If there are too many signatures, `top_signatures = ...` can be set to only show the 
signatures with the highest FDRs:

```r
# code only for demonstration
# e.g. to show the top 500 most significant rows
tb = get_signature(res, k = ..., top_signatures = 500)
```

If the signatures are defined as these which are uniquely high in current group, `diff_method` argument
can be set to `"uniquely_high_in_one_group"`:

```r
# code only for demonstration
tb = get_signature(res, k = ..., diff_method = "uniquely_high_in_one_group")
```




UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-node-0-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-node-0-dimension-reduction'>
<ul>
<li><a href='#tab-node-0-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-node-0-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-node-0-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-node-0-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-node-0-dimension-reduction-5'>k = 6</a></li>
<li><a href='#tab-node-0-dimension-reduction-6'>k = 7</a></li>
<li><a href='#tab-node-0-dimension-reduction-7'>k = 8</a></li>
</ul>
<div id='tab-node-0-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-1-1.png" alt="plot of chunk tab-node-0-dimension-reduction-1"/></p>

</div>
<div id='tab-node-0-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-2-1.png" alt="plot of chunk tab-node-0-dimension-reduction-2"/></p>

</div>
<div id='tab-node-0-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-3-1.png" alt="plot of chunk tab-node-0-dimension-reduction-3"/></p>

</div>
<div id='tab-node-0-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-4-1.png" alt="plot of chunk tab-node-0-dimension-reduction-4"/></p>

</div>
<div id='tab-node-0-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-5-1.png" alt="plot of chunk tab-node-0-dimension-reduction-5"/></p>

</div>
<div id='tab-node-0-dimension-reduction-6'>
<pre><code class="r">dimension_reduction(res, k = 7, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-6-1.png" alt="plot of chunk tab-node-0-dimension-reduction-6"/></p>

</div>
<div id='tab-node-0-dimension-reduction-7'>
<pre><code class="r">dimension_reduction(res, k = 8, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-0-dimension-reduction-7-1.png" alt="plot of chunk tab-node-0-dimension-reduction-7"/></p>

</div>
</div>



Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk node-0-collect-classes](figure_cola/node-0-collect-classes-1.png)



If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](https://jokergoo.github.io/cola_vignettes/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### Node02


Parent node: [Node0](#Node0).
Child nodes: 
                Node021-leaf
        ,
                [Node022](#Node022)
        ,
                Node023-leaf
        .







The object with results only for a single top-value method and a single partitioning method 
can be extracted as:

```r
res = res_rh["02"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6, 7, 8.
#>   On a matrix with 30000 rows and 45 columns.
#>   Top rows (1000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 350 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_partitions"     
#>  [7] "compare_signatures"      "consensus_heatmap"       "dimension_reduction"    
#> [10] "functional_enrichment"   "get_anno_col"            "get_anno"               
#> [13] "get_classes"             "get_consensus"           "get_matrix"             
#> [16] "get_membership"          "get_param"               "get_signatures"         
#> [19] "get_stats"               "is_best_k"               "is_stable_k"            
#> [22] "membership_heatmap"      "ncol"                    "nrow"                   
#> [25] "plot_ecdf"               "predict_classes"         "rownames"               
#> [28] "select_partition_number" "show"                    "suggest_best_k"         
#> [31] "test_to_known_factors"   "top_rows_heatmap"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of subgroups)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk node-02-collect-plots](figure_cola/node-02-collect-plots-1.png)

The plots are:

- The first row: a plot of the eCDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- eCDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus subgroup labels in all
  partitions.
- Area increased. Denote $A_k$ as the area under the eCDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](https://jokergoo.github.io/cola_vignettes/cola.html#toc_13).

Generally speaking, higher 1-PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk node-02-select-partition-number](figure_cola/node-02-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.2997 0.701   0.701
#> 3 3 1.000           0.975       0.991         1.1192 0.667   0.524
#> 4 4 0.753           0.536       0.813         0.1276 0.960   0.890
#> 5 5 0.709           0.637       0.816         0.0565 0.868   0.626
#> 6 6 0.747           0.706       0.851         0.0467 0.943   0.776
#> 7 7 0.761           0.335       0.776         0.0340 0.958   0.802
#> 8 8 0.792           0.691       0.843         0.0203 0.952   0.764
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following is the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall subgroup
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-node-02-get-classes' ).tabs();
} );
</script>
<div id='tabs-node-02-get-classes'>
<ul>
<li><a href='#tab-node-02-get-classes-1'>k = 2</a></li>
<li><a href='#tab-node-02-get-classes-2'>k = 3</a></li>
<li><a href='#tab-node-02-get-classes-3'>k = 4</a></li>
<li><a href='#tab-node-02-get-classes-4'>k = 5</a></li>
<li><a href='#tab-node-02-get-classes-5'>k = 6</a></li>
<li><a href='#tab-node-02-get-classes-6'>k = 7</a></li>
<li><a href='#tab-node-02-get-classes-7'>k = 8</a></li>
</ul>

<div id='tab-node-02-get-classes-1'>
<p><a id='tab-node-02-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette p1 p2
#&gt; TCGA.KL.8332.01     2       0          1  0  1
#&gt; TCGA.KL.8330.01     2       0          1  0  1
#&gt; TCGA.KL.8339.01     2       0          1  0  1
#&gt; TCGA.KN.8428.01     2       0          1  0  1
#&gt; TCGA.KL.8326.01     2       0          1  0  1
#&gt; TCGA.KN.8429.01     2       0          1  0  1
#&gt; TCGA.KO.8408.01     2       0          1  0  1
#&gt; TCGA.KN.8436.01     2       0          1  0  1
#&gt; TCGA.KM.8440.01     2       0          1  0  1
#&gt; TCGA.KO.8410.01     2       0          1  0  1
#&gt; TCGA.KL.8340.01     2       0          1  0  1
#&gt; TCGA.KN.8437.01     1       0          1  1  0
#&gt; TCGA.KL.8344.01     2       0          1  0  1
#&gt; TCGA.KN.8435.01     2       0          1  0  1
#&gt; TCGA.KO.8404.01     1       0          1  1  0
#&gt; TCGA.KN.8427.01     1       0          1  1  0
#&gt; TCGA.KN.8423.01     2       0          1  0  1
#&gt; TCGA.KL.8337.01     2       0          1  0  1
#&gt; TCGA.KO.8405.01     2       0          1  0  1
#&gt; TCGA.KN.8424.01     2       0          1  0  1
#&gt; TCGA.KN.8426.01     2       0          1  0  1
#&gt; TCGA.KM.8441.01     1       0          1  1  0
#&gt; TCGA.KM.8477.01     2       0          1  0  1
#&gt; TCGA.KM.8439.01     1       0          1  1  0
#&gt; TCGA.KL.8335.01     2       0          1  0  1
#&gt; TCGA.KM.8438.01     2       0          1  0  1
#&gt; TCGA.KO.8413.01     2       0          1  0  1
#&gt; TCGA.KL.8331.01     2       0          1  0  1
#&gt; TCGA.KN.8432.01     2       0          1  0  1
#&gt; TCGA.KM.8639.01     1       0          1  1  0
#&gt; TCGA.KN.8421.01     2       0          1  0  1
#&gt; TCGA.KL.8336.01     2       0          1  0  1
#&gt; TCGA.KL.8334.01     2       0          1  0  1
#&gt; TCGA.KO.8407.01     2       0          1  0  1
#&gt; TCGA.KN.8422.01     2       0          1  0  1
#&gt; TCGA.KN.8418.01     2       0          1  0  1
#&gt; TCGA.KN.8430.01     2       0          1  0  1
#&gt; TCGA.KL.8341.01     2       0          1  0  1
#&gt; TCGA.KL.8328.01     2       0          1  0  1
#&gt; TCGA.KL.8324.01     2       0          1  0  1
#&gt; TCGA.KL.8333.01     1       0          1  1  0
#&gt; TCGA.KL.8329.01     2       0          1  0  1
#&gt; TCGA.KL.8338.01     2       0          1  0  1
#&gt; TCGA.KN.8433.01     1       0          1  1  0
#&gt; TCGA.KN.8431.01     2       0          1  0  1
</code></pre>

<script>
$('#tab-node-02-get-classes-1-a').parent().next().next().hide();
$('#tab-node-02-get-classes-1-a').click(function(){
  $('#tab-node-02-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-02-get-classes-2'>
<p><a id='tab-node-02-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette p1  p2  p3
#&gt; TCGA.KL.8332.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KL.8330.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KL.8339.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KN.8428.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KL.8326.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KN.8429.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KO.8408.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KN.8436.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KM.8440.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KO.8410.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KL.8340.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KN.8437.01     1   0.000      1.000  1 0.0 0.0
#&gt; TCGA.KL.8344.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KN.8435.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KO.8404.01     1   0.000      1.000  1 0.0 0.0
#&gt; TCGA.KN.8427.01     1   0.000      1.000  1 0.0 0.0
#&gt; TCGA.KN.8423.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KL.8337.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KO.8405.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KN.8424.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KN.8426.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KM.8441.01     1   0.000      1.000  1 0.0 0.0
#&gt; TCGA.KM.8477.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KM.8439.01     1   0.000      1.000  1 0.0 0.0
#&gt; TCGA.KL.8335.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KM.8438.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KO.8413.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KL.8331.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KN.8432.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KM.8639.01     1   0.000      1.000  1 0.0 0.0
#&gt; TCGA.KN.8421.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KL.8336.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KL.8334.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KO.8407.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KN.8422.01     2   0.613      0.333  0 0.6 0.4
#&gt; TCGA.KN.8418.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KN.8430.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KL.8341.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KL.8328.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KL.8324.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KL.8333.01     1   0.000      1.000  1 0.0 0.0
#&gt; TCGA.KL.8329.01     2   0.000      0.979  0 1.0 0.0
#&gt; TCGA.KL.8338.01     3   0.000      1.000  0 0.0 1.0
#&gt; TCGA.KN.8433.01     1   0.000      1.000  1 0.0 0.0
#&gt; TCGA.KN.8431.01     2   0.000      0.979  0 1.0 0.0
</code></pre>

<script>
$('#tab-node-02-get-classes-2-a').parent().next().next().hide();
$('#tab-node-02-get-classes-2-a').click(function(){
  $('#tab-node-02-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-02-get-classes-3'>
<p><a id='tab-node-02-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4
#&gt; TCGA.KL.8332.01     3  0.0707      0.924 0.00 0.00 0.98 0.02
#&gt; TCGA.KL.8330.01     4  0.6323      0.932 0.00 0.44 0.06 0.50
#&gt; TCGA.KL.8339.01     2  0.3610      0.492 0.00 0.80 0.00 0.20
#&gt; TCGA.KN.8428.01     3  0.0707      0.924 0.00 0.00 0.98 0.02
#&gt; TCGA.KL.8326.01     3  0.0000      0.924 0.00 0.00 1.00 0.00
#&gt; TCGA.KN.8429.01     2  0.4522     -0.249 0.00 0.68 0.00 0.32
#&gt; TCGA.KO.8408.01     2  0.0000      0.461 0.00 1.00 0.00 0.00
#&gt; TCGA.KN.8436.01     4  0.6005      0.930 0.00 0.46 0.04 0.50
#&gt; TCGA.KM.8440.01     2  0.5713     -0.425 0.00 0.62 0.04 0.34
#&gt; TCGA.KO.8410.01     3  0.1637      0.900 0.00 0.00 0.94 0.06
#&gt; TCGA.KL.8340.01     2  0.6074     -0.475 0.00 0.60 0.06 0.34
#&gt; TCGA.KN.8437.01     1  0.0000      0.967 1.00 0.00 0.00 0.00
#&gt; TCGA.KL.8344.01     3  0.0000      0.924 0.00 0.00 1.00 0.00
#&gt; TCGA.KN.8435.01     2  0.3610      0.492 0.00 0.80 0.00 0.20
#&gt; TCGA.KO.8404.01     1  0.0000      0.967 1.00 0.00 0.00 0.00
#&gt; TCGA.KN.8427.01     1  0.0000      0.967 1.00 0.00 0.00 0.00
#&gt; TCGA.KN.8423.01     3  0.0000      0.924 0.00 0.00 1.00 0.00
#&gt; TCGA.KL.8337.01     3  0.4948      0.351 0.00 0.00 0.56 0.44
#&gt; TCGA.KO.8405.01     3  0.3400      0.819 0.00 0.00 0.82 0.18
#&gt; TCGA.KN.8424.01     2  0.0000      0.461 0.00 1.00 0.00 0.00
#&gt; TCGA.KN.8426.01     2  0.5986     -0.416 0.00 0.62 0.06 0.32
#&gt; TCGA.KM.8441.01     1  0.0000      0.967 1.00 0.00 0.00 0.00
#&gt; TCGA.KM.8477.01     3  0.0000      0.924 0.00 0.00 1.00 0.00
#&gt; TCGA.KM.8439.01     1  0.0000      0.967 1.00 0.00 0.00 0.00
#&gt; TCGA.KL.8335.01     2  0.3610      0.492 0.00 0.80 0.00 0.20
#&gt; TCGA.KM.8438.01     2  0.5619     -0.363 0.00 0.64 0.04 0.32
#&gt; TCGA.KO.8413.01     3  0.1211      0.909 0.00 0.00 0.96 0.04
#&gt; TCGA.KL.8331.01     2  0.3610      0.492 0.00 0.80 0.00 0.20
#&gt; TCGA.KN.8432.01     3  0.2921      0.867 0.00 0.00 0.86 0.14
#&gt; TCGA.KM.8639.01     1  0.0000      0.967 1.00 0.00 0.00 0.00
#&gt; TCGA.KN.8421.01     3  0.3801      0.814 0.00 0.00 0.78 0.22
#&gt; TCGA.KL.8336.01     2  0.0000      0.461 0.00 1.00 0.00 0.00
#&gt; TCGA.KL.8334.01     3  0.0707      0.924 0.00 0.00 0.98 0.02
#&gt; TCGA.KO.8407.01     3  0.0707      0.924 0.00 0.00 0.98 0.02
#&gt; TCGA.KN.8422.01     2  0.7816     -0.572 0.00 0.40 0.26 0.34
#&gt; TCGA.KN.8418.01     2  0.2647      0.489 0.00 0.88 0.00 0.12
#&gt; TCGA.KN.8430.01     2  0.0000      0.461 0.00 1.00 0.00 0.00
#&gt; TCGA.KL.8341.01     2  0.3610      0.492 0.00 0.80 0.00 0.20
#&gt; TCGA.KL.8328.01     2  0.3610      0.492 0.00 0.80 0.00 0.20
#&gt; TCGA.KL.8324.01     2  0.4277     -0.132 0.00 0.72 0.00 0.28
#&gt; TCGA.KL.8333.01     1  0.2921      0.904 0.86 0.00 0.00 0.14
#&gt; TCGA.KL.8329.01     2  0.6074     -0.475 0.00 0.60 0.06 0.34
#&gt; TCGA.KL.8338.01     3  0.0707      0.924 0.00 0.00 0.98 0.02
#&gt; TCGA.KN.8433.01     1  0.3400      0.879 0.82 0.00 0.00 0.18
#&gt; TCGA.KN.8431.01     2  0.6074     -0.475 0.00 0.60 0.06 0.34
</code></pre>

<script>
$('#tab-node-02-get-classes-3-a').parent().next().next().hide();
$('#tab-node-02-get-classes-3-a').click(function(){
  $('#tab-node-02-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-02-get-classes-4'>
<p><a id='tab-node-02-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5
#&gt; TCGA.KL.8332.01     3  0.2610     0.7529 0.00 0.02 0.90 0.06 0.02
#&gt; TCGA.KL.8330.01     2  0.5487     0.2227 0.00 0.62 0.00 0.28 0.10
#&gt; TCGA.KL.8339.01     5  0.3684     0.9624 0.00 0.28 0.00 0.00 0.72
#&gt; TCGA.KN.8428.01     3  0.3348     0.7431 0.00 0.02 0.86 0.08 0.04
#&gt; TCGA.KL.8326.01     3  0.0000     0.7707 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.KN.8429.01     2  0.1648     0.6861 0.00 0.94 0.00 0.02 0.04
#&gt; TCGA.KO.8408.01     2  0.4126     0.0202 0.00 0.62 0.00 0.00 0.38
#&gt; TCGA.KN.8436.01     2  0.5487     0.2227 0.00 0.62 0.00 0.28 0.10
#&gt; TCGA.KM.8440.01     2  0.1820     0.6985 0.00 0.94 0.02 0.02 0.02
#&gt; TCGA.KO.8410.01     3  0.2616     0.7141 0.00 0.00 0.88 0.10 0.02
#&gt; TCGA.KL.8340.01     2  0.1043     0.7035 0.00 0.96 0.04 0.00 0.00
#&gt; TCGA.KN.8437.01     1  0.0000     0.8890 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8344.01     3  0.0000     0.7707 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.KN.8435.01     5  0.3561     0.9459 0.00 0.26 0.00 0.00 0.74
#&gt; TCGA.KO.8404.01     1  0.1043     0.8816 0.96 0.00 0.00 0.00 0.04
#&gt; TCGA.KN.8427.01     1  0.1043     0.8816 0.96 0.00 0.00 0.00 0.04
#&gt; TCGA.KN.8423.01     3  0.1648     0.7560 0.00 0.00 0.94 0.04 0.02
#&gt; TCGA.KL.8337.01     4  0.7973     0.0000 0.00 0.16 0.36 0.36 0.12
#&gt; TCGA.KO.8405.01     3  0.4262     0.1804 0.00 0.00 0.56 0.44 0.00
#&gt; TCGA.KN.8424.01     2  0.4126     0.0202 0.00 0.62 0.00 0.00 0.38
#&gt; TCGA.KN.8426.01     2  0.1043     0.7035 0.00 0.96 0.04 0.00 0.00
#&gt; TCGA.KM.8441.01     1  0.0000     0.8890 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KM.8477.01     3  0.0609     0.7683 0.00 0.00 0.98 0.02 0.00
#&gt; TCGA.KM.8439.01     1  0.0000     0.8890 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8335.01     5  0.3684     0.9624 0.00 0.28 0.00 0.00 0.72
#&gt; TCGA.KM.8438.01     2  0.1648     0.7030 0.00 0.94 0.04 0.02 0.00
#&gt; TCGA.KO.8413.01     3  0.2012     0.7448 0.00 0.00 0.92 0.06 0.02
#&gt; TCGA.KL.8331.01     5  0.3684     0.9624 0.00 0.28 0.00 0.00 0.72
#&gt; TCGA.KN.8432.01     3  0.5525     0.4087 0.00 0.04 0.70 0.18 0.08
#&gt; TCGA.KM.8639.01     1  0.0000     0.8890 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8421.01     3  0.6792    -0.0470 0.00 0.04 0.54 0.28 0.14
#&gt; TCGA.KL.8336.01     2  0.4126     0.0202 0.00 0.62 0.00 0.00 0.38
#&gt; TCGA.KL.8334.01     3  0.2610     0.7529 0.00 0.02 0.90 0.06 0.02
#&gt; TCGA.KO.8407.01     3  0.2610     0.7529 0.00 0.02 0.90 0.06 0.02
#&gt; TCGA.KN.8422.01     2  0.2732     0.5659 0.00 0.84 0.16 0.00 0.00
#&gt; TCGA.KN.8418.01     5  0.4060     0.8243 0.00 0.36 0.00 0.00 0.64
#&gt; TCGA.KN.8430.01     2  0.4126     0.0202 0.00 0.62 0.00 0.00 0.38
#&gt; TCGA.KL.8341.01     5  0.3561     0.9459 0.00 0.26 0.00 0.00 0.74
#&gt; TCGA.KL.8328.01     5  0.3684     0.9624 0.00 0.28 0.00 0.00 0.72
#&gt; TCGA.KL.8324.01     2  0.2331     0.6592 0.00 0.90 0.00 0.02 0.08
#&gt; TCGA.KL.8333.01     1  0.4126     0.6581 0.62 0.00 0.00 0.38 0.00
#&gt; TCGA.KL.8329.01     2  0.1043     0.7035 0.00 0.96 0.04 0.00 0.00
#&gt; TCGA.KL.8338.01     3  0.2610     0.7529 0.00 0.02 0.90 0.06 0.02
#&gt; TCGA.KN.8433.01     1  0.4182     0.6389 0.60 0.00 0.00 0.40 0.00
#&gt; TCGA.KN.8431.01     2  0.1648     0.7030 0.00 0.94 0.04 0.02 0.00
</code></pre>

<script>
$('#tab-node-02-get-classes-4-a').parent().next().next().hide();
$('#tab-node-02-get-classes-4-a').click(function(){
  $('#tab-node-02-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-02-get-classes-5'>
<p><a id='tab-node-02-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6
#&gt; TCGA.KL.8332.01     3  0.2094      0.803 0.00 0.00 0.90 0.02 0.00 0.08
#&gt; TCGA.KL.8330.01     4  0.3916      0.500 0.00 0.30 0.00 0.68 0.02 0.00
#&gt; TCGA.KL.8339.01     5  0.2260      0.880 0.00 0.14 0.00 0.00 0.86 0.00
#&gt; TCGA.KN.8428.01     3  0.3976      0.602 0.00 0.00 0.74 0.02 0.02 0.22
#&gt; TCGA.KL.8326.01     3  0.1267      0.794 0.00 0.00 0.94 0.06 0.00 0.00
#&gt; TCGA.KN.8429.01     2  0.0937      0.875 0.00 0.96 0.00 0.00 0.04 0.00
#&gt; TCGA.KO.8408.01     2  0.2941      0.743 0.00 0.78 0.00 0.00 0.22 0.00
#&gt; TCGA.KN.8436.01     4  0.3916      0.500 0.00 0.30 0.00 0.68 0.02 0.00
#&gt; TCGA.KM.8440.01     2  0.0547      0.866 0.00 0.98 0.00 0.02 0.00 0.00
#&gt; TCGA.KO.8410.01     3  0.0937      0.791 0.00 0.00 0.96 0.00 0.00 0.04
#&gt; TCGA.KL.8340.01     2  0.0547      0.866 0.00 0.98 0.00 0.02 0.00 0.00
#&gt; TCGA.KN.8437.01     1  0.0000      0.850 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8344.01     3  0.1267      0.794 0.00 0.00 0.94 0.06 0.00 0.00
#&gt; TCGA.KN.8435.01     5  0.3544      0.782 0.00 0.08 0.00 0.00 0.80 0.12
#&gt; TCGA.KO.8404.01     1  0.1807      0.831 0.92 0.00 0.00 0.06 0.02 0.00
#&gt; TCGA.KN.8427.01     1  0.1807      0.831 0.92 0.00 0.00 0.06 0.02 0.00
#&gt; TCGA.KN.8423.01     3  0.0000      0.812 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.KL.8337.01     4  0.3324      0.257 0.00 0.08 0.06 0.84 0.00 0.02
#&gt; TCGA.KO.8405.01     3  0.3864     -0.130 0.00 0.00 0.52 0.00 0.00 0.48
#&gt; TCGA.KN.8424.01     2  0.2941      0.743 0.00 0.78 0.00 0.00 0.22 0.00
#&gt; TCGA.KN.8426.01     2  0.0547      0.878 0.00 0.98 0.00 0.00 0.02 0.00
#&gt; TCGA.KM.8441.01     1  0.0000      0.850 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KM.8477.01     3  0.0000      0.812 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.KM.8439.01     1  0.0000      0.850 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8335.01     5  0.2260      0.880 0.00 0.14 0.00 0.00 0.86 0.00
#&gt; TCGA.KM.8438.01     2  0.0000      0.876 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KO.8413.01     3  0.0937      0.791 0.00 0.00 0.96 0.00 0.00 0.04
#&gt; TCGA.KL.8331.01     5  0.2260      0.880 0.00 0.14 0.00 0.00 0.86 0.00
#&gt; TCGA.KN.8432.01     4  0.5361     -0.467 0.00 0.02 0.44 0.48 0.00 0.06
#&gt; TCGA.KM.8639.01     1  0.0000      0.850 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8421.01     6  0.7416      0.000 0.00 0.02 0.32 0.26 0.06 0.34
#&gt; TCGA.KL.8336.01     2  0.2941      0.743 0.00 0.78 0.00 0.00 0.22 0.00
#&gt; TCGA.KL.8334.01     3  0.2474      0.804 0.00 0.00 0.88 0.04 0.00 0.08
#&gt; TCGA.KO.8407.01     3  0.2474      0.804 0.00 0.00 0.88 0.04 0.00 0.08
#&gt; TCGA.KN.8422.01     2  0.1092      0.844 0.00 0.96 0.02 0.02 0.00 0.00
#&gt; TCGA.KN.8418.01     5  0.3647      0.528 0.00 0.36 0.00 0.00 0.64 0.00
#&gt; TCGA.KN.8430.01     2  0.2941      0.743 0.00 0.78 0.00 0.00 0.22 0.00
#&gt; TCGA.KL.8341.01     5  0.3544      0.782 0.00 0.08 0.00 0.00 0.80 0.12
#&gt; TCGA.KL.8328.01     5  0.2260      0.880 0.00 0.14 0.00 0.00 0.86 0.00
#&gt; TCGA.KL.8324.01     2  0.0937      0.875 0.00 0.96 0.00 0.00 0.04 0.00
#&gt; TCGA.KL.8333.01     1  0.3828      0.545 0.56 0.00 0.00 0.00 0.00 0.44
#&gt; TCGA.KL.8329.01     2  0.0000      0.876 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8338.01     3  0.2474      0.804 0.00 0.00 0.88 0.04 0.00 0.08
#&gt; TCGA.KN.8433.01     1  0.3864      0.493 0.52 0.00 0.00 0.00 0.00 0.48
#&gt; TCGA.KN.8431.01     2  0.0547      0.866 0.00 0.98 0.00 0.02 0.00 0.00
</code></pre>

<script>
$('#tab-node-02-get-classes-5-a').parent().next().next().hide();
$('#tab-node-02-get-classes-5-a').click(function(){
  $('#tab-node-02-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-02-get-classes-6'>
<p><a id='tab-node-02-get-classes-6-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 7), get_membership(res, k = 7))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6   p7
#&gt; TCGA.KL.8332.01     3  0.1664     0.7245 0.00 0.00 0.92 0.02 0.00 0.00 0.06
#&gt; TCGA.KL.8330.01     4  0.4969     0.5411 0.00 0.06 0.00 0.66 0.08 0.00 0.20
#&gt; TCGA.KL.8339.01     5  0.3546     0.9109 0.00 0.46 0.00 0.00 0.54 0.00 0.00
#&gt; TCGA.KN.8428.01     3  0.4022     0.5311 0.00 0.02 0.78 0.02 0.10 0.00 0.08
#&gt; TCGA.KL.8326.01     3  0.3199     0.7383 0.00 0.00 0.80 0.06 0.00 0.14 0.00
#&gt; TCGA.KN.8429.01     2  0.3496    -0.6606 0.00 0.58 0.00 0.00 0.00 0.00 0.42
#&gt; TCGA.KO.8408.01     2  0.0000     0.3264 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8436.01     4  0.5046     0.5457 0.00 0.06 0.00 0.66 0.10 0.00 0.18
#&gt; TCGA.KM.8440.01     2  0.3994    -0.8517 0.00 0.50 0.00 0.02 0.00 0.00 0.48
#&gt; TCGA.KO.8410.01     3  0.3186     0.7016 0.00 0.00 0.76 0.02 0.00 0.22 0.00
#&gt; TCGA.KL.8340.01     2  0.3562    -0.8915 0.00 0.50 0.00 0.00 0.00 0.00 0.50
#&gt; TCGA.KN.8437.01     1  0.0000     0.8328 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8344.01     3  0.3199     0.7383 0.00 0.00 0.80 0.06 0.00 0.14 0.00
#&gt; TCGA.KN.8435.01     5  0.4070     0.8161 0.00 0.30 0.00 0.02 0.66 0.00 0.02
#&gt; TCGA.KO.8404.01     1  0.2572     0.8025 0.86 0.00 0.00 0.00 0.06 0.00 0.08
#&gt; TCGA.KN.8427.01     1  0.2572     0.8025 0.86 0.00 0.00 0.00 0.06 0.00 0.08
#&gt; TCGA.KN.8423.01     3  0.2906     0.7375 0.00 0.00 0.80 0.02 0.00 0.18 0.00
#&gt; TCGA.KL.8337.01     4  0.1433     0.4186 0.00 0.00 0.08 0.92 0.00 0.00 0.00
#&gt; TCGA.KO.8405.01     6  0.3294    -0.0595 0.00 0.00 0.34 0.00 0.00 0.66 0.00
#&gt; TCGA.KN.8424.01     2  0.0000     0.3264 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8426.01     2  0.3496    -0.7002 0.00 0.58 0.00 0.00 0.00 0.00 0.42
#&gt; TCGA.KM.8441.01     1  0.0000     0.8328 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KM.8477.01     3  0.2745     0.7459 0.00 0.00 0.82 0.02 0.00 0.16 0.00
#&gt; TCGA.KM.8439.01     1  0.0000     0.8328 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8335.01     5  0.3546     0.9109 0.00 0.46 0.00 0.00 0.54 0.00 0.00
#&gt; TCGA.KM.8438.01     2  0.3994    -0.8517 0.00 0.50 0.00 0.02 0.00 0.00 0.48
#&gt; TCGA.KO.8413.01     3  0.3186     0.7016 0.00 0.00 0.76 0.02 0.00 0.22 0.00
#&gt; TCGA.KL.8331.01     5  0.3546     0.9109 0.00 0.46 0.00 0.00 0.54 0.00 0.00
#&gt; TCGA.KN.8432.01     4  0.6100    -0.2049 0.00 0.00 0.32 0.46 0.02 0.18 0.02
#&gt; TCGA.KM.8639.01     1  0.0504     0.8283 0.98 0.00 0.00 0.00 0.02 0.00 0.00
#&gt; TCGA.KN.8421.01     6  0.7308    -0.0257 0.00 0.00 0.10 0.14 0.08 0.42 0.26
#&gt; TCGA.KL.8336.01     2  0.0000     0.3264 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8334.01     3  0.1664     0.7245 0.00 0.00 0.92 0.02 0.00 0.00 0.06
#&gt; TCGA.KO.8407.01     3  0.1664     0.7245 0.00 0.00 0.92 0.02 0.00 0.00 0.06
#&gt; TCGA.KN.8422.01     7  0.3994     0.0000 0.00 0.48 0.02 0.00 0.00 0.00 0.50
#&gt; TCGA.KN.8418.01     2  0.3815    -0.6693 0.00 0.62 0.00 0.00 0.36 0.00 0.02
#&gt; TCGA.KN.8430.01     2  0.0000     0.3264 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8341.01     5  0.4070     0.8161 0.00 0.30 0.00 0.02 0.66 0.00 0.02
#&gt; TCGA.KL.8328.01     5  0.3546     0.9109 0.00 0.46 0.00 0.00 0.54 0.00 0.00
#&gt; TCGA.KL.8324.01     2  0.2945    -0.1100 0.00 0.74 0.00 0.00 0.00 0.00 0.26
#&gt; TCGA.KL.8333.01     1  0.3525     0.5315 0.56 0.00 0.00 0.00 0.00 0.44 0.00
#&gt; TCGA.KL.8329.01     2  0.3558    -0.8703 0.00 0.52 0.00 0.00 0.00 0.00 0.48
#&gt; TCGA.KL.8338.01     3  0.1664     0.7245 0.00 0.00 0.92 0.02 0.00 0.00 0.06
#&gt; TCGA.KN.8433.01     1  0.3558     0.4748 0.52 0.00 0.00 0.00 0.00 0.48 0.00
#&gt; TCGA.KN.8431.01     2  0.3994    -0.8517 0.00 0.50 0.00 0.02 0.00 0.00 0.48
</code></pre>

<script>
$('#tab-node-02-get-classes-6-a').parent().next().next().hide();
$('#tab-node-02-get-classes-6-a').click(function(){
  $('#tab-node-02-get-classes-6-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-02-get-classes-7'>
<p><a id='tab-node-02-get-classes-7-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 8), get_membership(res, k = 8))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6   p7   p8
#&gt; TCGA.KL.8332.01     3  0.2756      0.644 0.00 0.00 0.74 0.00 0.00 0.00 0.26 0.00
#&gt; TCGA.KL.8330.01     4  0.1887      0.752 0.00 0.06 0.00 0.90 0.00 0.00 0.00 0.04
#&gt; TCGA.KL.8339.01     5  0.0000      0.844 0.00 0.00 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.KN.8428.01     3  0.4955      0.412 0.00 0.04 0.54 0.00 0.00 0.00 0.34 0.08
#&gt; TCGA.KL.8326.01     3  0.0941      0.656 0.00 0.00 0.96 0.02 0.00 0.02 0.00 0.00
#&gt; TCGA.KN.8429.01     2  0.0471      0.834 0.00 0.98 0.00 0.00 0.00 0.00 0.02 0.00
#&gt; TCGA.KO.8408.01     2  0.2650      0.714 0.00 0.76 0.00 0.00 0.24 0.00 0.00 0.00
#&gt; TCGA.KN.8436.01     4  0.1091      0.759 0.00 0.06 0.00 0.94 0.00 0.00 0.00 0.00
#&gt; TCGA.KM.8440.01     2  0.2348      0.824 0.00 0.88 0.00 0.02 0.00 0.00 0.04 0.06
#&gt; TCGA.KO.8410.01     3  0.3314      0.547 0.00 0.00 0.80 0.00 0.00 0.10 0.08 0.02
#&gt; TCGA.KL.8340.01     2  0.2348      0.824 0.00 0.88 0.00 0.02 0.00 0.00 0.04 0.06
#&gt; TCGA.KN.8437.01     1  0.0000      0.905 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8344.01     3  0.0941      0.656 0.00 0.00 0.96 0.02 0.00 0.02 0.00 0.00
#&gt; TCGA.KN.8435.01     5  0.3073      0.741 0.00 0.00 0.00 0.00 0.80 0.00 0.10 0.10
#&gt; TCGA.KO.8404.01     1  0.3444      0.794 0.78 0.00 0.00 0.02 0.00 0.06 0.14 0.00
#&gt; TCGA.KN.8427.01     1  0.3337      0.794 0.78 0.00 0.00 0.02 0.00 0.04 0.16 0.00
#&gt; TCGA.KN.8423.01     3  0.3314      0.547 0.00 0.00 0.80 0.00 0.00 0.10 0.08 0.02
#&gt; TCGA.KL.8337.01     4  0.5454      0.426 0.00 0.02 0.04 0.62 0.00 0.06 0.22 0.04
#&gt; TCGA.KO.8405.01     8  0.2756      0.365 0.00 0.00 0.26 0.00 0.00 0.00 0.00 0.74
#&gt; TCGA.KN.8424.01     2  0.2534      0.733 0.00 0.78 0.00 0.00 0.22 0.00 0.00 0.00
#&gt; TCGA.KN.8426.01     2  0.0000      0.831 0.00 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KM.8441.01     1  0.0000      0.905 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KM.8477.01     3  0.0808      0.654 0.00 0.00 0.96 0.00 0.00 0.00 0.04 0.00
#&gt; TCGA.KM.8439.01     1  0.0000      0.905 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8335.01     5  0.0000      0.844 0.00 0.00 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.KM.8438.01     2  0.2348      0.824 0.00 0.88 0.00 0.02 0.00 0.00 0.04 0.06
#&gt; TCGA.KO.8413.01     3  0.3314      0.547 0.00 0.00 0.80 0.00 0.00 0.10 0.08 0.02
#&gt; TCGA.KL.8331.01     5  0.0000      0.844 0.00 0.00 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.KN.8432.01     7  0.6383      0.000 0.00 0.00 0.30 0.16 0.00 0.10 0.42 0.02
#&gt; TCGA.KM.8639.01     1  0.0000      0.905 1.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8421.01     6  0.1091      0.000 0.00 0.00 0.06 0.00 0.00 0.94 0.00 0.00
#&gt; TCGA.KL.8336.01     2  0.2650      0.714 0.00 0.76 0.00 0.00 0.24 0.00 0.00 0.00
#&gt; TCGA.KL.8334.01     3  0.2756      0.644 0.00 0.00 0.74 0.00 0.00 0.00 0.26 0.00
#&gt; TCGA.KO.8407.01     3  0.2756      0.644 0.00 0.00 0.74 0.00 0.00 0.00 0.26 0.00
#&gt; TCGA.KN.8422.01     2  0.2348      0.824 0.00 0.88 0.00 0.02 0.00 0.00 0.04 0.06
#&gt; TCGA.KN.8418.01     5  0.3015      0.410 0.00 0.32 0.00 0.00 0.68 0.00 0.00 0.00
#&gt; TCGA.KN.8430.01     2  0.2650      0.714 0.00 0.76 0.00 0.00 0.24 0.00 0.00 0.00
#&gt; TCGA.KL.8341.01     5  0.3073      0.741 0.00 0.00 0.00 0.00 0.80 0.00 0.10 0.10
#&gt; TCGA.KL.8328.01     5  0.0000      0.844 0.00 0.00 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.KL.8324.01     2  0.1563      0.807 0.00 0.90 0.00 0.00 0.10 0.00 0.00 0.00
#&gt; TCGA.KL.8333.01     8  0.2852      0.710 0.28 0.00 0.00 0.00 0.00 0.00 0.00 0.72
#&gt; TCGA.KL.8329.01     2  0.0941      0.834 0.00 0.96 0.00 0.00 0.00 0.00 0.02 0.02
#&gt; TCGA.KL.8338.01     3  0.2756      0.644 0.00 0.00 0.74 0.00 0.00 0.00 0.26 0.00
#&gt; TCGA.KN.8433.01     8  0.3291      0.707 0.28 0.00 0.00 0.02 0.00 0.00 0.00 0.70
#&gt; TCGA.KN.8431.01     2  0.2348      0.824 0.00 0.88 0.00 0.02 0.00 0.00 0.04 0.06
</code></pre>

<script>
$('#tab-node-02-get-classes-7-a').parent().next().next().hide();
$('#tab-node-02-get-classes-7-a').click(function(){
  $('#tab-node-02-get-classes-7-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.




<script>
$( function() {
	$( '#tabs-node-02-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-02-consensus-heatmap'>
<ul>
<li><a href='#tab-node-02-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-02-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-02-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-02-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-02-consensus-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-02-consensus-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-02-consensus-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-02-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-1-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-1"/></p>

</div>
<div id='tab-node-02-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-2-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-2"/></p>

</div>
<div id='tab-node-02-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-3-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-3"/></p>

</div>
<div id='tab-node-02-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-4-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-4"/></p>

</div>
<div id='tab-node-02-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-5-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-5"/></p>

</div>
<div id='tab-node-02-consensus-heatmap-6'>
<pre><code class="r">consensus_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-6-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-6"/></p>

</div>
<div id='tab-node-02-consensus-heatmap-7'>
<pre><code class="r">consensus_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-02-consensus-heatmap-7-1.png" alt="plot of chunk tab-node-02-consensus-heatmap-7"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:





<script>
$( function() {
	$( '#tabs-node-02-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-02-membership-heatmap'>
<ul>
<li><a href='#tab-node-02-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-02-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-02-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-02-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-02-membership-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-02-membership-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-02-membership-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-02-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-1-1.png" alt="plot of chunk tab-node-02-membership-heatmap-1"/></p>

</div>
<div id='tab-node-02-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-2-1.png" alt="plot of chunk tab-node-02-membership-heatmap-2"/></p>

</div>
<div id='tab-node-02-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-3-1.png" alt="plot of chunk tab-node-02-membership-heatmap-3"/></p>

</div>
<div id='tab-node-02-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-4-1.png" alt="plot of chunk tab-node-02-membership-heatmap-4"/></p>

</div>
<div id='tab-node-02-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-5-1.png" alt="plot of chunk tab-node-02-membership-heatmap-5"/></p>

</div>
<div id='tab-node-02-membership-heatmap-6'>
<pre><code class="r">membership_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-6-1.png" alt="plot of chunk tab-node-02-membership-heatmap-6"/></p>

</div>
<div id='tab-node-02-membership-heatmap-7'>
<pre><code class="r">membership_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-02-membership-heatmap-7-1.png" alt="plot of chunk tab-node-02-membership-heatmap-7"/></p>

</div>
</div>

As soon as the classes for columns are determined, the signatures
that are significantly different between subgroups can be looked for. 
Following are the heatmaps for signatures.






<script>
$( function() {
	$( '#tabs-node-02-get-signatures' ).tabs();
} );
</script>
<div id='tabs-node-02-get-signatures'>
<ul>
<li><a href='#tab-node-02-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-node-02-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-node-02-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-node-02-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-node-02-get-signatures-5'>k = 6</a></li>
<li><a href='#tab-node-02-get-signatures-6'>k = 7</a></li>
<li><a href='#tab-node-02-get-signatures-7'>k = 8</a></li>
</ul>
<div id='tab-node-02-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-1-1.png" alt="plot of chunk tab-node-02-get-signatures-1"/></p>

</div>
<div id='tab-node-02-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-2-1.png" alt="plot of chunk tab-node-02-get-signatures-2"/></p>

</div>
<div id='tab-node-02-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-3-1.png" alt="plot of chunk tab-node-02-get-signatures-3"/></p>

</div>
<div id='tab-node-02-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-4-1.png" alt="plot of chunk tab-node-02-get-signatures-4"/></p>

</div>
<div id='tab-node-02-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-5-1.png" alt="plot of chunk tab-node-02-get-signatures-5"/></p>

</div>
<div id='tab-node-02-get-signatures-6'>
<pre><code class="r">get_signatures(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-6-1.png" alt="plot of chunk tab-node-02-get-signatures-6"/></p>

</div>
<div id='tab-node-02-get-signatures-7'>
<pre><code class="r">get_signatures(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-02-get-signatures-7-1.png" alt="plot of chunk tab-node-02-get-signatures-7"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk node-02-signature_compare](figure_cola/node-02-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. To get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows (which is done by automatically selecting number of clusters).

If there are too many signatures, `top_signatures = ...` can be set to only show the 
signatures with the highest FDRs:

```r
# code only for demonstration
# e.g. to show the top 500 most significant rows
tb = get_signature(res, k = ..., top_signatures = 500)
```

If the signatures are defined as these which are uniquely high in current group, `diff_method` argument
can be set to `"uniquely_high_in_one_group"`:

```r
# code only for demonstration
tb = get_signature(res, k = ..., diff_method = "uniquely_high_in_one_group")
```




UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-node-02-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-node-02-dimension-reduction'>
<ul>
<li><a href='#tab-node-02-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-node-02-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-node-02-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-node-02-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-node-02-dimension-reduction-5'>k = 6</a></li>
<li><a href='#tab-node-02-dimension-reduction-6'>k = 7</a></li>
<li><a href='#tab-node-02-dimension-reduction-7'>k = 8</a></li>
</ul>
<div id='tab-node-02-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-1-1.png" alt="plot of chunk tab-node-02-dimension-reduction-1"/></p>

</div>
<div id='tab-node-02-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-2-1.png" alt="plot of chunk tab-node-02-dimension-reduction-2"/></p>

</div>
<div id='tab-node-02-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-3-1.png" alt="plot of chunk tab-node-02-dimension-reduction-3"/></p>

</div>
<div id='tab-node-02-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-4-1.png" alt="plot of chunk tab-node-02-dimension-reduction-4"/></p>

</div>
<div id='tab-node-02-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-5-1.png" alt="plot of chunk tab-node-02-dimension-reduction-5"/></p>

</div>
<div id='tab-node-02-dimension-reduction-6'>
<pre><code class="r">dimension_reduction(res, k = 7, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-6-1.png" alt="plot of chunk tab-node-02-dimension-reduction-6"/></p>

</div>
<div id='tab-node-02-dimension-reduction-7'>
<pre><code class="r">dimension_reduction(res, k = 8, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-02-dimension-reduction-7-1.png" alt="plot of chunk tab-node-02-dimension-reduction-7"/></p>

</div>
</div>



Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk node-02-collect-classes](figure_cola/node-02-collect-classes-1.png)



If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](https://jokergoo.github.io/cola_vignettes/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### Node022


Parent node: [Node02](#Node02).
Child nodes: 
                Node0221-leaf
        ,
                Node0222-leaf
        ,
                Node0223-leaf
        ,
                Node0224-leaf
        .







The object with results only for a single top-value method and a single partitioning method 
can be extracted as:

```r
res = res_rh["022"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6, 7, 8.
#>   On a matrix with 30000 rows and 22 columns.
#>   Top rows (1000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 350 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_partitions"     
#>  [7] "compare_signatures"      "consensus_heatmap"       "dimension_reduction"    
#> [10] "functional_enrichment"   "get_anno_col"            "get_anno"               
#> [13] "get_classes"             "get_consensus"           "get_matrix"             
#> [16] "get_membership"          "get_param"               "get_signatures"         
#> [19] "get_stats"               "is_best_k"               "is_stable_k"            
#> [22] "membership_heatmap"      "ncol"                    "nrow"                   
#> [25] "plot_ecdf"               "predict_classes"         "rownames"               
#> [28] "select_partition_number" "show"                    "suggest_best_k"         
#> [31] "test_to_known_factors"   "top_rows_heatmap"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of subgroups)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk node-022-collect-plots](figure_cola/node-022-collect-plots-1.png)

The plots are:

- The first row: a plot of the eCDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- eCDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus subgroup labels in all
  partitions.
- Area increased. Denote $A_k$ as the area under the eCDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](https://jokergoo.github.io/cola_vignettes/cola.html#toc_13).

Generally speaking, higher 1-PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk node-022-select-partition-number](figure_cola/node-022-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.998       0.999         0.5072 0.494   0.494
#> 3 3 0.616           0.814       0.852         0.1659 0.844   0.700
#> 4 4 1.000           0.992       0.996         0.1806 0.913   0.778
#> 5 5 0.874           0.847       0.942         0.0554 0.974   0.914
#> 6 6 0.884           0.763       0.924         0.0317 0.965   0.875
#> 7 7 0.884           0.767       0.918         0.0246 0.978   0.912
#> 8 8 0.827           0.680       0.886         0.0315 0.991   0.962
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following is the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall subgroup
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-node-022-get-classes' ).tabs();
} );
</script>
<div id='tabs-node-022-get-classes'>
<ul>
<li><a href='#tab-node-022-get-classes-1'>k = 2</a></li>
<li><a href='#tab-node-022-get-classes-2'>k = 3</a></li>
<li><a href='#tab-node-022-get-classes-3'>k = 4</a></li>
<li><a href='#tab-node-022-get-classes-4'>k = 5</a></li>
<li><a href='#tab-node-022-get-classes-5'>k = 6</a></li>
<li><a href='#tab-node-022-get-classes-6'>k = 7</a></li>
<li><a href='#tab-node-022-get-classes-7'>k = 8</a></li>
</ul>

<div id='tab-node-022-get-classes-1'>
<p><a id='tab-node-022-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2
#&gt; TCGA.KL.8330.01     1   0.000      0.998 1.00 0.00
#&gt; TCGA.KL.8339.01     2   0.000      1.000 0.00 1.00
#&gt; TCGA.KN.8429.01     1   0.000      0.998 1.00 0.00
#&gt; TCGA.KO.8408.01     2   0.000      1.000 0.00 1.00
#&gt; TCGA.KN.8436.01     1   0.000      0.998 1.00 0.00
#&gt; TCGA.KM.8440.01     1   0.000      0.998 1.00 0.00
#&gt; TCGA.KL.8340.01     1   0.000      0.998 1.00 0.00
#&gt; TCGA.KN.8435.01     2   0.000      1.000 0.00 1.00
#&gt; TCGA.KN.8424.01     1   0.000      0.998 1.00 0.00
#&gt; TCGA.KN.8426.01     1   0.141      0.980 0.98 0.02
#&gt; TCGA.KL.8335.01     2   0.000      1.000 0.00 1.00
#&gt; TCGA.KM.8438.01     1   0.000      0.998 1.00 0.00
#&gt; TCGA.KL.8331.01     2   0.000      1.000 0.00 1.00
#&gt; TCGA.KL.8336.01     2   0.000      1.000 0.00 1.00
#&gt; TCGA.KN.8422.01     1   0.000      0.998 1.00 0.00
#&gt; TCGA.KN.8418.01     1   0.000      0.998 1.00 0.00
#&gt; TCGA.KN.8430.01     2   0.000      1.000 0.00 1.00
#&gt; TCGA.KL.8341.01     2   0.000      1.000 0.00 1.00
#&gt; TCGA.KL.8328.01     2   0.000      1.000 0.00 1.00
#&gt; TCGA.KL.8324.01     1   0.000      0.998 1.00 0.00
#&gt; TCGA.KL.8329.01     1   0.000      0.998 1.00 0.00
#&gt; TCGA.KN.8431.01     1   0.000      0.998 1.00 0.00
</code></pre>

<script>
$('#tab-node-022-get-classes-1-a').parent().next().next().hide();
$('#tab-node-022-get-classes-1-a').click(function(){
  $('#tab-node-022-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-022-get-classes-2'>
<p><a id='tab-node-022-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3
#&gt; TCGA.KL.8330.01     1   0.296      0.463 0.90 0.10 0.00
#&gt; TCGA.KL.8339.01     3   0.000      1.000 0.00 0.00 1.00
#&gt; TCGA.KN.8429.01     1   0.604      0.910 0.62 0.38 0.00
#&gt; TCGA.KO.8408.01     2   0.595      0.776 0.00 0.64 0.36
#&gt; TCGA.KN.8436.01     1   0.296      0.463 0.90 0.10 0.00
#&gt; TCGA.KM.8440.01     1   0.604      0.910 0.62 0.38 0.00
#&gt; TCGA.KL.8340.01     1   0.604      0.910 0.62 0.38 0.00
#&gt; TCGA.KN.8435.01     3   0.000      1.000 0.00 0.00 1.00
#&gt; TCGA.KN.8424.01     1   0.604      0.910 0.62 0.38 0.00
#&gt; TCGA.KN.8426.01     2   0.296      0.501 0.00 0.90 0.10
#&gt; TCGA.KL.8335.01     2   0.571      0.769 0.00 0.68 0.32
#&gt; TCGA.KM.8438.01     1   0.604      0.910 0.62 0.38 0.00
#&gt; TCGA.KL.8331.01     2   0.628      0.651 0.00 0.54 0.46
#&gt; TCGA.KL.8336.01     2   0.613      0.753 0.00 0.60 0.40
#&gt; TCGA.KN.8422.01     1   0.604      0.910 0.62 0.38 0.00
#&gt; TCGA.KN.8418.01     1   0.604      0.910 0.62 0.38 0.00
#&gt; TCGA.KN.8430.01     2   0.624      0.698 0.00 0.56 0.44
#&gt; TCGA.KL.8341.01     3   0.000      1.000 0.00 0.00 1.00
#&gt; TCGA.KL.8328.01     2   0.540      0.736 0.00 0.72 0.28
#&gt; TCGA.KL.8324.01     1   0.604      0.910 0.62 0.38 0.00
#&gt; TCGA.KL.8329.01     1   0.604      0.910 0.62 0.38 0.00
#&gt; TCGA.KN.8431.01     1   0.604      0.910 0.62 0.38 0.00
</code></pre>

<script>
$('#tab-node-022-get-classes-2-a').parent().next().next().hide();
$('#tab-node-022-get-classes-2-a').click(function(){
  $('#tab-node-022-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-022-get-classes-3'>
<p><a id='tab-node-022-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3 p4
#&gt; TCGA.KL.8330.01     4  0.0000      1.000 0.00 0.00 0.00  1
#&gt; TCGA.KL.8339.01     3  0.0000      1.000 0.00 0.00 1.00  0
#&gt; TCGA.KN.8429.01     1  0.0000      0.997 1.00 0.00 0.00  0
#&gt; TCGA.KO.8408.01     2  0.0000      0.989 0.00 1.00 0.00  0
#&gt; TCGA.KN.8436.01     4  0.0000      1.000 0.00 0.00 0.00  1
#&gt; TCGA.KM.8440.01     1  0.0000      0.997 1.00 0.00 0.00  0
#&gt; TCGA.KL.8340.01     1  0.0000      0.997 1.00 0.00 0.00  0
#&gt; TCGA.KN.8435.01     3  0.0000      1.000 0.00 0.00 1.00  0
#&gt; TCGA.KN.8424.01     1  0.0000      0.997 1.00 0.00 0.00  0
#&gt; TCGA.KN.8426.01     2  0.0000      0.989 0.00 1.00 0.00  0
#&gt; TCGA.KL.8335.01     2  0.0000      0.989 0.00 1.00 0.00  0
#&gt; TCGA.KM.8438.01     1  0.0000      0.997 1.00 0.00 0.00  0
#&gt; TCGA.KL.8331.01     2  0.1211      0.958 0.00 0.96 0.04  0
#&gt; TCGA.KL.8336.01     2  0.0000      0.989 0.00 1.00 0.00  0
#&gt; TCGA.KN.8422.01     1  0.0000      0.997 1.00 0.00 0.00  0
#&gt; TCGA.KN.8418.01     1  0.0000      0.997 1.00 0.00 0.00  0
#&gt; TCGA.KN.8430.01     2  0.0707      0.976 0.00 0.98 0.02  0
#&gt; TCGA.KL.8341.01     3  0.0000      1.000 0.00 0.00 1.00  0
#&gt; TCGA.KL.8328.01     2  0.0000      0.989 0.00 1.00 0.00  0
#&gt; TCGA.KL.8324.01     1  0.0000      0.997 1.00 0.00 0.00  0
#&gt; TCGA.KL.8329.01     1  0.0707      0.976 0.98 0.02 0.00  0
#&gt; TCGA.KN.8431.01     1  0.0000      0.997 1.00 0.00 0.00  0
</code></pre>

<script>
$('#tab-node-022-get-classes-3-a').parent().next().next().hide();
$('#tab-node-022-get-classes-3-a').click(function(){
  $('#tab-node-022-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-022-get-classes-4'>
<p><a id='tab-node-022-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3 p4   p5
#&gt; TCGA.KL.8330.01     4   0.000      1.000 0.00 0.00 0.00  1 0.00
#&gt; TCGA.KL.8339.01     3   0.233      0.875 0.00 0.08 0.90  0 0.02
#&gt; TCGA.KN.8429.01     1   0.000      0.971 1.00 0.00 0.00  0 0.00
#&gt; TCGA.KO.8408.01     2   0.000      0.818 0.00 1.00 0.00  0 0.00
#&gt; TCGA.KN.8436.01     4   0.000      1.000 0.00 0.00 0.00  1 0.00
#&gt; TCGA.KM.8440.01     1   0.000      0.971 1.00 0.00 0.00  0 0.00
#&gt; TCGA.KL.8340.01     1   0.000      0.971 1.00 0.00 0.00  0 0.00
#&gt; TCGA.KN.8435.01     3   0.000      0.939 0.00 0.00 1.00  0 0.00
#&gt; TCGA.KN.8424.01     1   0.000      0.971 1.00 0.00 0.00  0 0.00
#&gt; TCGA.KN.8426.01     2   0.413      0.670 0.02 0.72 0.00  0 0.26
#&gt; TCGA.KL.8335.01     2   0.000      0.818 0.00 1.00 0.00  0 0.00
#&gt; TCGA.KM.8438.01     1   0.000      0.971 1.00 0.00 0.00  0 0.00
#&gt; TCGA.KL.8331.01     5   0.233      0.000 0.00 0.08 0.02  0 0.90
#&gt; TCGA.KL.8336.01     2   0.104      0.804 0.00 0.96 0.00  0 0.04
#&gt; TCGA.KN.8422.01     1   0.000      0.971 1.00 0.00 0.00  0 0.00
#&gt; TCGA.KN.8418.01     1   0.000      0.971 1.00 0.00 0.00  0 0.00
#&gt; TCGA.KN.8430.01     2   0.332      0.758 0.00 0.82 0.02  0 0.16
#&gt; TCGA.KL.8341.01     3   0.000      0.939 0.00 0.00 1.00  0 0.00
#&gt; TCGA.KL.8328.01     2   0.398      0.593 0.00 0.66 0.00  0 0.34
#&gt; TCGA.KL.8324.01     1   0.000      0.971 1.00 0.00 0.00  0 0.00
#&gt; TCGA.KL.8329.01     1   0.444      0.675 0.76 0.10 0.00  0 0.14
#&gt; TCGA.KN.8431.01     1   0.000      0.971 1.00 0.00 0.00  0 0.00
</code></pre>

<script>
$('#tab-node-022-get-classes-4-a').parent().next().next().hide();
$('#tab-node-022-get-classes-4-a').click(function(){
  $('#tab-node-022-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-022-get-classes-5'>
<p><a id='tab-node-022-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3 p4   p5   p6
#&gt; TCGA.KL.8330.01     4  0.0000     1.0000 0.00 0.00 0.00  1 0.00 0.00
#&gt; TCGA.KL.8339.01     3  0.2350     0.8491 0.00 0.10 0.88  0 0.00 0.02
#&gt; TCGA.KN.8429.01     1  0.0000     0.9705 1.00 0.00 0.00  0 0.00 0.00
#&gt; TCGA.KO.8408.01     2  0.0937     0.7571 0.00 0.96 0.00  0 0.00 0.04
#&gt; TCGA.KN.8436.01     4  0.0000     1.0000 0.00 0.00 0.00  1 0.00 0.00
#&gt; TCGA.KM.8440.01     1  0.0000     0.9705 1.00 0.00 0.00  0 0.00 0.00
#&gt; TCGA.KL.8340.01     1  0.0000     0.9705 1.00 0.00 0.00  0 0.00 0.00
#&gt; TCGA.KN.8435.01     3  0.0000     0.9265 0.00 0.00 1.00  0 0.00 0.00
#&gt; TCGA.KN.8424.01     1  0.0000     0.9705 1.00 0.00 0.00  0 0.00 0.00
#&gt; TCGA.KN.8426.01     6  0.5447    -0.0546 0.00 0.42 0.00  0 0.12 0.46
#&gt; TCGA.KL.8335.01     2  0.0000     0.7637 0.00 1.00 0.00  0 0.00 0.00
#&gt; TCGA.KM.8438.01     1  0.0000     0.9705 1.00 0.00 0.00  0 0.00 0.00
#&gt; TCGA.KL.8331.01     5  0.0000     0.0000 0.00 0.00 0.00  0 1.00 0.00
#&gt; TCGA.KL.8336.01     2  0.0547     0.7553 0.00 0.98 0.00  0 0.00 0.02
#&gt; TCGA.KN.8422.01     1  0.0000     0.9705 1.00 0.00 0.00  0 0.00 0.00
#&gt; TCGA.KN.8418.01     1  0.0000     0.9705 1.00 0.00 0.00  0 0.00 0.00
#&gt; TCGA.KN.8430.01     2  0.4199     0.2124 0.00 0.60 0.00  0 0.02 0.38
#&gt; TCGA.KL.8341.01     3  0.0000     0.9265 0.00 0.00 1.00  0 0.00 0.00
#&gt; TCGA.KL.8328.01     6  0.4360     0.2476 0.00 0.26 0.00  0 0.06 0.68
#&gt; TCGA.KL.8324.01     1  0.0000     0.9705 1.00 0.00 0.00  0 0.00 0.00
#&gt; TCGA.KL.8329.01     1  0.4444     0.6665 0.74 0.02 0.00  0 0.08 0.16
#&gt; TCGA.KN.8431.01     1  0.0000     0.9705 1.00 0.00 0.00  0 0.00 0.00
</code></pre>

<script>
$('#tab-node-022-get-classes-5-a').parent().next().next().hide();
$('#tab-node-022-get-classes-5-a').click(function(){
  $('#tab-node-022-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-022-get-classes-6'>
<p><a id='tab-node-022-get-classes-6-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 7), get_membership(res, k = 7))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4   p5   p6   p7
#&gt; TCGA.KL.8330.01     4  0.1006      0.967 0.00 0.00 0.00 0.96 0.00 0.02 0.02
#&gt; TCGA.KL.8339.01     3  0.5173      0.588 0.00 0.20 0.64 0.00 0.00 0.06 0.10
#&gt; TCGA.KN.8429.01     1  0.0504      0.946 0.98 0.00 0.00 0.00 0.00 0.02 0.00
#&gt; TCGA.KO.8408.01     2  0.0504      0.943 0.00 0.98 0.00 0.00 0.00 0.00 0.02
#&gt; TCGA.KN.8436.01     4  0.0000      0.967 0.00 0.00 0.00 1.00 0.00 0.00 0.00
#&gt; TCGA.KM.8440.01     1  0.0504      0.945 0.98 0.00 0.00 0.00 0.00 0.00 0.02
#&gt; TCGA.KL.8340.01     1  0.0000      0.950 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8435.01     3  0.0000      0.809 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8424.01     1  0.0504      0.944 0.98 0.00 0.00 0.00 0.00 0.02 0.00
#&gt; TCGA.KN.8426.01     6  0.5462      0.376 0.00 0.22 0.00 0.00 0.06 0.60 0.12
#&gt; TCGA.KL.8335.01     2  0.1363      0.922 0.00 0.94 0.00 0.00 0.00 0.02 0.04
#&gt; TCGA.KM.8438.01     1  0.0863      0.935 0.96 0.00 0.00 0.00 0.00 0.04 0.00
#&gt; TCGA.KL.8331.01     5  0.0000      0.000 0.00 0.00 0.00 0.00 1.00 0.00 0.00
#&gt; TCGA.KL.8336.01     2  0.0000      0.948 0.00 1.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8422.01     1  0.0000      0.950 1.00 0.00 0.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KN.8418.01     1  0.0504      0.946 0.98 0.00 0.00 0.00 0.00 0.02 0.00
#&gt; TCGA.KN.8430.01     6  0.3984      0.443 0.00 0.28 0.02 0.00 0.00 0.68 0.02
#&gt; TCGA.KL.8341.01     3  0.0000      0.809 0.00 0.00 1.00 0.00 0.00 0.00 0.00
#&gt; TCGA.KL.8328.01     7  0.2803      0.000 0.00 0.06 0.00 0.00 0.00 0.10 0.84
#&gt; TCGA.KL.8324.01     1  0.0504      0.945 0.98 0.00 0.00 0.00 0.00 0.00 0.02
#&gt; TCGA.KL.8329.01     1  0.5071      0.595 0.68 0.02 0.00 0.00 0.06 0.18 0.06
#&gt; TCGA.KN.8431.01     1  0.0000      0.950 1.00 0.00 0.00 0.00 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-022-get-classes-6-a').parent().next().next().hide();
$('#tab-node-022-get-classes-6-a').click(function(){
  $('#tab-node-022-get-classes-6-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-node-022-get-classes-7'>
<p><a id='tab-node-022-get-classes-7-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 8), get_membership(res, k = 8))
</code></pre>

<pre><code>#&gt;                 class entropy silhouette   p1   p2   p3   p4 p5   p6   p7   p8
#&gt; TCGA.KL.8330.01     4  0.0000      0.880 0.00 0.00 0.00 1.00  0 0.00 0.00 0.00
#&gt; TCGA.KL.8339.01     8  0.1765      0.000 0.00 0.12 0.00 0.00  0 0.00 0.00 0.88
#&gt; TCGA.KN.8429.01     1  0.0471      0.894 0.98 0.00 0.02 0.00  0 0.00 0.00 0.00
#&gt; TCGA.KO.8408.01     2  0.1557      0.862 0.00 0.92 0.02 0.00  0 0.06 0.00 0.00
#&gt; TCGA.KN.8436.01     4  0.2484      0.880 0.00 0.00 0.10 0.86  0 0.02 0.02 0.00
#&gt; TCGA.KM.8440.01     1  0.1091      0.877 0.94 0.00 0.06 0.00  0 0.00 0.00 0.00
#&gt; TCGA.KL.8340.01     1  0.1341      0.869 0.92 0.00 0.08 0.00  0 0.00 0.00 0.00
#&gt; TCGA.KN.8435.01     3  0.3329      0.969 0.00 0.00 0.52 0.00  0 0.00 0.00 0.48
#&gt; TCGA.KN.8424.01     1  0.2888      0.781 0.80 0.04 0.16 0.00  0 0.00 0.00 0.00
#&gt; TCGA.KN.8426.01     6  0.4963      0.386 0.02 0.06 0.18 0.00  0 0.66 0.08 0.00
#&gt; TCGA.KL.8335.01     2  0.1607      0.844 0.00 0.92 0.04 0.00  0 0.04 0.00 0.00
#&gt; TCGA.KM.8438.01     1  0.0471      0.894 0.98 0.00 0.02 0.00  0 0.00 0.00 0.00
#&gt; TCGA.KL.8331.01     5  0.0000      0.000 0.00 0.00 0.00 0.00  1 0.00 0.00 0.00
#&gt; TCGA.KL.8336.01     2  0.2265      0.830 0.00 0.88 0.02 0.00  0 0.02 0.00 0.08
#&gt; TCGA.KN.8422.01     1  0.0000      0.895 1.00 0.00 0.00 0.00  0 0.00 0.00 0.00
#&gt; TCGA.KN.8418.01     1  0.0808      0.888 0.96 0.00 0.04 0.00  0 0.00 0.00 0.00
#&gt; TCGA.KN.8430.01     6  0.2856      0.400 0.00 0.20 0.00 0.00  0 0.78 0.00 0.02
#&gt; TCGA.KL.8341.01     3  0.3333      0.969 0.00 0.00 0.50 0.00  0 0.00 0.00 0.50
#&gt; TCGA.KL.8328.01     7  0.0471      0.000 0.00 0.02 0.00 0.00  0 0.00 0.98 0.00
#&gt; TCGA.KL.8324.01     1  0.0000      0.895 1.00 0.00 0.00 0.00  0 0.00 0.00 0.00
#&gt; TCGA.KL.8329.01     1  0.6434      0.046 0.42 0.02 0.18 0.00  0 0.28 0.10 0.00
#&gt; TCGA.KN.8431.01     1  0.0000      0.895 1.00 0.00 0.00 0.00  0 0.00 0.00 0.00
</code></pre>

<script>
$('#tab-node-022-get-classes-7-a').parent().next().next().hide();
$('#tab-node-022-get-classes-7-a').click(function(){
  $('#tab-node-022-get-classes-7-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.




<script>
$( function() {
	$( '#tabs-node-022-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-022-consensus-heatmap'>
<ul>
<li><a href='#tab-node-022-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-022-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-022-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-022-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-022-consensus-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-022-consensus-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-022-consensus-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-022-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-022-consensus-heatmap-1-1.png" alt="plot of chunk tab-node-022-consensus-heatmap-1"/></p>

</div>
<div id='tab-node-022-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-022-consensus-heatmap-2-1.png" alt="plot of chunk tab-node-022-consensus-heatmap-2"/></p>

</div>
<div id='tab-node-022-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-022-consensus-heatmap-3-1.png" alt="plot of chunk tab-node-022-consensus-heatmap-3"/></p>

</div>
<div id='tab-node-022-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-022-consensus-heatmap-4-1.png" alt="plot of chunk tab-node-022-consensus-heatmap-4"/></p>

</div>
<div id='tab-node-022-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-022-consensus-heatmap-5-1.png" alt="plot of chunk tab-node-022-consensus-heatmap-5"/></p>

</div>
<div id='tab-node-022-consensus-heatmap-6'>
<pre><code class="r">consensus_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-022-consensus-heatmap-6-1.png" alt="plot of chunk tab-node-022-consensus-heatmap-6"/></p>

</div>
<div id='tab-node-022-consensus-heatmap-7'>
<pre><code class="r">consensus_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-022-consensus-heatmap-7-1.png" alt="plot of chunk tab-node-022-consensus-heatmap-7"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:





<script>
$( function() {
	$( '#tabs-node-022-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-node-022-membership-heatmap'>
<ul>
<li><a href='#tab-node-022-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-node-022-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-node-022-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-node-022-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-node-022-membership-heatmap-5'>k = 6</a></li>
<li><a href='#tab-node-022-membership-heatmap-6'>k = 7</a></li>
<li><a href='#tab-node-022-membership-heatmap-7'>k = 8</a></li>
</ul>
<div id='tab-node-022-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-022-membership-heatmap-1-1.png" alt="plot of chunk tab-node-022-membership-heatmap-1"/></p>

</div>
<div id='tab-node-022-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-022-membership-heatmap-2-1.png" alt="plot of chunk tab-node-022-membership-heatmap-2"/></p>

</div>
<div id='tab-node-022-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-022-membership-heatmap-3-1.png" alt="plot of chunk tab-node-022-membership-heatmap-3"/></p>

</div>
<div id='tab-node-022-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-022-membership-heatmap-4-1.png" alt="plot of chunk tab-node-022-membership-heatmap-4"/></p>

</div>
<div id='tab-node-022-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-022-membership-heatmap-5-1.png" alt="plot of chunk tab-node-022-membership-heatmap-5"/></p>

</div>
<div id='tab-node-022-membership-heatmap-6'>
<pre><code class="r">membership_heatmap(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-022-membership-heatmap-6-1.png" alt="plot of chunk tab-node-022-membership-heatmap-6"/></p>

</div>
<div id='tab-node-022-membership-heatmap-7'>
<pre><code class="r">membership_heatmap(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-022-membership-heatmap-7-1.png" alt="plot of chunk tab-node-022-membership-heatmap-7"/></p>

</div>
</div>

As soon as the classes for columns are determined, the signatures
that are significantly different between subgroups can be looked for. 
Following are the heatmaps for signatures.






<script>
$( function() {
	$( '#tabs-node-022-get-signatures' ).tabs();
} );
</script>
<div id='tabs-node-022-get-signatures'>
<ul>
<li><a href='#tab-node-022-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-node-022-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-node-022-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-node-022-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-node-022-get-signatures-5'>k = 6</a></li>
<li><a href='#tab-node-022-get-signatures-6'>k = 7</a></li>
<li><a href='#tab-node-022-get-signatures-7'>k = 8</a></li>
</ul>
<div id='tab-node-022-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-node-022-get-signatures-1-1.png" alt="plot of chunk tab-node-022-get-signatures-1"/></p>

</div>
<div id='tab-node-022-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-node-022-get-signatures-2-1.png" alt="plot of chunk tab-node-022-get-signatures-2"/></p>

</div>
<div id='tab-node-022-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-node-022-get-signatures-3-1.png" alt="plot of chunk tab-node-022-get-signatures-3"/></p>

</div>
<div id='tab-node-022-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-node-022-get-signatures-4-1.png" alt="plot of chunk tab-node-022-get-signatures-4"/></p>

</div>
<div id='tab-node-022-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-node-022-get-signatures-5-1.png" alt="plot of chunk tab-node-022-get-signatures-5"/></p>

</div>
<div id='tab-node-022-get-signatures-6'>
<pre><code class="r">get_signatures(res, k = 7)
</code></pre>

<p><img src="figure_cola/tab-node-022-get-signatures-6-1.png" alt="plot of chunk tab-node-022-get-signatures-6"/></p>

</div>
<div id='tab-node-022-get-signatures-7'>
<pre><code class="r">get_signatures(res, k = 8)
</code></pre>

<p><img src="figure_cola/tab-node-022-get-signatures-7-1.png" alt="plot of chunk tab-node-022-get-signatures-7"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk node-022-signature_compare](figure_cola/node-022-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. To get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows (which is done by automatically selecting number of clusters).

If there are too many signatures, `top_signatures = ...` can be set to only show the 
signatures with the highest FDRs:

```r
# code only for demonstration
# e.g. to show the top 500 most significant rows
tb = get_signature(res, k = ..., top_signatures = 500)
```

If the signatures are defined as these which are uniquely high in current group, `diff_method` argument
can be set to `"uniquely_high_in_one_group"`:

```r
# code only for demonstration
tb = get_signature(res, k = ..., diff_method = "uniquely_high_in_one_group")
```




UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-node-022-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-node-022-dimension-reduction'>
<ul>
<li><a href='#tab-node-022-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-node-022-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-node-022-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-node-022-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-node-022-dimension-reduction-5'>k = 6</a></li>
<li><a href='#tab-node-022-dimension-reduction-6'>k = 7</a></li>
<li><a href='#tab-node-022-dimension-reduction-7'>k = 8</a></li>
</ul>
<div id='tab-node-022-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-022-dimension-reduction-1-1.png" alt="plot of chunk tab-node-022-dimension-reduction-1"/></p>

</div>
<div id='tab-node-022-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-022-dimension-reduction-2-1.png" alt="plot of chunk tab-node-022-dimension-reduction-2"/></p>

</div>
<div id='tab-node-022-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-022-dimension-reduction-3-1.png" alt="plot of chunk tab-node-022-dimension-reduction-3"/></p>

</div>
<div id='tab-node-022-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-022-dimension-reduction-4-1.png" alt="plot of chunk tab-node-022-dimension-reduction-4"/></p>

</div>
<div id='tab-node-022-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-022-dimension-reduction-5-1.png" alt="plot of chunk tab-node-022-dimension-reduction-5"/></p>

</div>
<div id='tab-node-022-dimension-reduction-6'>
<pre><code class="r">dimension_reduction(res, k = 7, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-022-dimension-reduction-6-1.png" alt="plot of chunk tab-node-022-dimension-reduction-6"/></p>

</div>
<div id='tab-node-022-dimension-reduction-7'>
<pre><code class="r">dimension_reduction(res, k = 8, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-node-022-dimension-reduction-7-1.png" alt="plot of chunk tab-node-022-dimension-reduction-7"/></p>

</div>
</div>



Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk node-022-collect-classes](figure_cola/node-022-collect-classes-1.png)



If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](https://jokergoo.github.io/cola_vignettes/functional_enrichment.html) for more detailed explanations.


 

## Session info


```r
sessionInfo()
```

```
#> R version 4.1.0 (2021-05-18)
#> Platform: x86_64-pc-linux-gnu (64-bit)
#> Running under: CentOS Linux 7 (Core)
#> 
#> Matrix products: default
#> BLAS/LAPACK: /usr/lib64/libopenblas-r0.3.3.so
#> 
#> locale:
#>  [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C               LC_TIME=en_US.UTF-8       
#>  [4] LC_COLLATE=en_US.UTF-8     LC_MONETARY=en_US.UTF-8    LC_MESSAGES=en_US.UTF-8   
#>  [7] LC_PAPER=en_US.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
#> [10] LC_TELEPHONE=C             LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C       
#> 
#> attached base packages:
#> [1] grid      stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] genefilter_1.74.0    ComplexHeatmap_2.8.0 markdown_1.1         knitr_1.33          
#> [5] matrixStats_0.59.0   cola_1.9.4          
#> 
#> loaded via a namespace (and not attached):
#>   [1] bitops_1.0-7           bit64_4.0.5            doParallel_1.0.16      RColorBrewer_1.1-2    
#>   [5] httr_1.4.2             GenomeInfoDb_1.28.1    data.tree_1.0.0        tools_4.1.0           
#>   [9] utf8_1.2.1             R6_2.5.0               irlba_2.3.3            DBI_1.1.1             
#>  [13] BiocGenerics_0.38.0    colorspace_2.0-2       GetoptLong_1.0.5       gridExtra_2.3         
#>  [17] tidyselect_1.1.1       bit_4.0.4              compiler_4.1.0         Biobase_2.52.0        
#>  [21] Cairo_1.5-12.2         xml2_1.3.2             microbenchmark_1.4-7   slam_0.1-48           
#>  [25] scales_1.1.1           askpass_1.1            stringr_1.4.0          digest_0.6.27         
#>  [29] XVector_0.32.0         pkgconfig_2.0.3        umap_0.2.7.0           fastmap_1.1.0         
#>  [33] highr_0.9              rlang_0.4.11           GlobalOptions_0.1.2    rstudioapi_0.13       
#>  [37] RSQLite_2.2.7          impute_1.66.0          generics_0.1.0         shape_1.4.6           
#>  [41] jsonlite_1.7.2         mclust_5.4.7           dplyr_1.0.7            dendextend_1.15.1     
#>  [45] RCurl_1.98-1.3         magrittr_2.0.1         GenomeInfoDbData_1.2.6 Matrix_1.3-4          
#>  [49] fansi_0.5.0            Rcpp_1.0.7             munsell_0.5.0          S4Vectors_0.30.0      
#>  [53] viridis_0.6.1          reticulate_1.20        lifecycle_1.0.0        scatterplot3d_0.3-41  
#>  [57] stringi_1.7.3          zlibbioc_1.38.0        blob_1.2.1             parallel_4.1.0        
#>  [61] crayon_1.4.1           lattice_0.20-44        Biostrings_2.60.1      splines_4.1.0         
#>  [65] annotate_1.70.0        circlize_0.4.13        KEGGREST_1.32.0        polylabelr_0.2.0      
#>  [69] pillar_1.6.1           rjson_0.2.20           codetools_0.2-18       stats4_4.1.0          
#>  [73] XML_3.99-0.6           glue_1.4.2             evaluate_0.14          png_0.1-7             
#>  [77] vctrs_0.3.8            foreach_1.5.1          polyclip_1.10-0        purrr_0.3.4           
#>  [81] gtable_0.3.0           openssl_1.4.4          assertthat_0.2.1       clue_0.3-59           
#>  [85] cachem_1.0.5           ggplot2_3.3.5          xfun_0.24              eulerr_6.1.0          
#>  [89] xtable_1.8-4           skmeans_0.2-13         RSpectra_0.16-0        viridisLite_0.4.0     
#>  [93] survival_3.2-11        tibble_3.1.2           Polychrome_1.3.1       iterators_1.0.13      
#>  [97] AnnotationDbi_1.54.1   memoise_2.0.0          IRanges_2.26.0         cluster_2.1.2         
#> [101] ellipsis_0.3.2         brew_1.0-6
```




