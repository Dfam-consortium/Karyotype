# Karyotype - A SVG visualization of a genome karyotype with hit density overlay

## Introduction

The Karyotype viewer is a primary component of the Dfam.org website.  It displays
a standard Karyotype visual with an annotation density overlay.  

## Data format
Contigs/Chroms are assumed to be in length sorted order ( largest first )

         {
            'singleton_contigs': [{      // A list of chrom/contigs that will be displayed
                    'name': 'chr1',      // Name of chrom/contig
                    'size': 283834921,   // Size (in BP) of chrom/contig
                    'hit_clusters': [            // Precomputed clusters of all hits ( 1based )
                        [3397261, 4529680, 23],  //    [ startPos, endPos, hitCount ]
                        ...
                    ],
                    'nrph_hit_clusters': [    // Precomputed clusters of nrph filtered hits
                        [3397261, 4529680, 23],
                        ...
                    ],
                    'giesma_bands': [   // [optional] List of Giesma Staining Bands (see color chart)
                        [50200000, 55600000, 3],  //   [ startPos, endPos, colorCode ]
                       ...
                    ]
                },
                {
                    'name': 'chr2',
                    'size': 200283321,
                    'hit_clusters': [
                    ],
                    'nrph_hit_clusters': [
                    ]
                }
            ],
            'remaining_genome_contig': undefined,  // Placeholder for future use
        }


 Giesma Staining Color Codes
 ---------------------------
   0   acen    #527280
   1   gneg    #ffffff
   2   gvar    #c8c88c
   3   gpos25  #e6e6e6 
   4   gpos33  #c8c8c8
   5   gpos50  #b4b4b4
   6   gpos66  #8c8c8c
   7   gpos75  #646464
   8   gpos100 #323232
   9   "n/a"   #ffffff
   10  stalk   #823c5a


## Usage Example

HTML code to display a static dataset:

```html
<html>
  <body>
    <div id="karyotype">
    </div>
    <script src='Karyotype.js'></script>
    <script>
        var karyotype_data = { #INSERT_YOUR_JSON_DATASET_HERE# };
        var myKaryotype = new Karyotype( document.getElementById('karyotype'), 
                                         karyotype_data );
    </script>
    <input id="All_Hits" type="button" value="All Hits" onclick="myKaryotype.switchVisualization('all');" />
    <input id="NRPH_Hits" type="button" value="NRPH Hits" onclick="myKaryotype.switchVisualization('nrph');" />
    <input id="Giesma" type="button" value="Giesma" onclick="myKaryotype.switchVisualization('giesma');" />
  </body>
</html>
```
