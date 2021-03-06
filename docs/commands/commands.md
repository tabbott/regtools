##Synopsis
To get a list of all available regtools commands run `regtools --help`

The main regtools commands are

- [junctions](#junctions)

##Junctions

The transcriptome structure is often summarized from a RNAseq experiment with a BED file. This BED file contains the exon-exon boundary co-ordinates which are referred to as junctions. For example, TopHat outputs a file called 'junctions.bed' which contains this information. This file is very useful if you are interested in studying which exons/transcripts are expressed, splicing effects etc. On the command line these commands can be accessed using the `regtools junctions` command.

Listed below are links to detailed explanations of the `junctions` sub-commands

- [create](junctions-create.md)
- [annotate](junctions-annotate.md)
