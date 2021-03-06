#Synopsis
The `junctions create` command is used to extract exon-exon junctions
from an RNAseq BAM file. The output is a BED file, specifically in the BED12 format.

We have tested this command with alignments from TopHat and by comparing the
exon-exon junctions with the `junctions.bed` file produced from TopHat.

#Inputs
This command requires an aligned RNAseq BAM which has been indexed with `samtools index`. We have tested
this command with alignments from TopHat.

#Options

| Option  | Description |
| ------  | ----------- |
| -a      | Minimum anchor length. 8bp by default. Junctions having a minimum overlap of this much on both ends are reported. Note - the required overlap can be observed amongst separate reads, for example one read might have sufficient left overlap and another read might have sufficient right overlap, this is sufficient for the junction to be reported. No mismatches are allowed in the anchor regions.|
| -i      | Minimum intron size. 70bp by default. The intron size is the same as junction.end - junction.start. (Not to be confused with chromStart and chromEnd below, the required blockSizes need to be added/subtracted.)|
| -I      | Maximum intron size. 500,000bp by default. The intron size the same as junction.end - junction.start. (Not to be confused with chromStart and chromEnd below, the required blockSizes need to be added/subtracted.)|
| -o      | File to write output to. STDOUT by default.|
| -r      | Region to extract junctions in. This is specified in the format "chr:start-end" If not specified, junctions are extracted from the entire BAM file.             |
| -h      | Display help message for this command.|

#Output
The output is in the BED12 format which is described in detail [here.](https://genome.ucsc.edu/FAQ/FAQformat.html#format1)
Each line is an exon-exon junction as explained below.

1. **chrom** - The name of the chromosome.
2. **chromStart** - The starting position of the junction-anchor. This includes the maximum overhang for the junction on the left. For the exact junction start add blockSizes[0].
3. **chromEnd** - The ending position of the junction-anchor. This includes the maximum overhang for the juncion on the left. For the exact junction end subtract blockSizes[1].
4. **name** - The name of the junctions, the junctions are just numbered JUNC1 to JUNCn.
5. **score** - The number of reads supporting the junction.
6. **strand** - Defines the strand - either '+' or '-'. This is calculated using the XS tag in the BAM file.
7. **thickStart** - Same as chromStart.
8. **thickEnd** - Same as chromEnd.
9. **itemRgb** - RGB value - "255,0,0" by default.
10. **blockCount** - The number of blocks, 2 by default.
11. **blockSizes** - A comma-separated list of the block sizes. The number of items in this list should correspond to blockCount.
12. **blockStarts** - A comma-separated list of block starts. All of the blockStart positions should be calculated relative to chromStart. The number of items in this list should correspond to blockCount.
