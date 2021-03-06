# Module 3: Transcriptome Assembly Submissions

## Introduction

Transcriptome assemblies can be submitted to the European Nucleotide Archive (ENA) 
using the [Webin command line submission interface](cli_01.html). 
 
A transcriptome assembly consists of:
- General assembly information
   - Study accession or unique name (alias)
   - Sample accession or unique name (alias)
   - Assembly program
   - Sequencing platform
- Sequences
- Functional annotation (optional)

The following picture illustrates the stages of the transcriptome assembly submission process:

![Submission process](images/webin-cli_01.png)

## Stage 1: Pre-register study and sample

Each submission must be associated with a pre-registered study and a sample. The study and sample 
accessions or unique names (aliases) are provided in an `info` file associated with the submission. 

Instructions for interactive submitters:
- [Register a Study](mod_02.html)
- [Register a Sample](mod_03.html)

Instructions for programmatic submitters:
- [Register a Study](prog_02.html)
- [Register a Sample](prog_03.html)

## Stage 2: Prepare the files

The set of files that are part of the submission are specified using a manifest file.
The manifest file is specified using the `-manifest <filename>` option.

A transcriptome assembly submission consists of the following files:

- 1 manifest file
- 1 assembly info file
- 0-1 fasta files
- 0-1 flat files

The following files are mandatory:

- 1 manifest file must be provided.
- 1 assembly info file must be provided.
- 1 fasta or 1 flat file must be provided.

### Sequence names

Sequences must have a unique name within the submission that is provided in the fasta or flat files. 

### Manifest file

The manifest file has two columns separated by a tab (or any whitespace characters):
- File type (first column): case insensitive file type   
- File path (second column): the path to the file

For example, the following manifest file represents a transcriptome assembly consisting of an info file 
and a fasta file:

```
INFO    transcriptome.info.gz
FASTA   transcriptome.fasta.gz
``` 

The following case-insensitive file types are supported for transcriptome assemblies:

- INFO: assembly info file
- FASTA: sequences in fasta format
- FLATFILE: sequences in EMBL-Bank flat file format 

### Assembly info file

The assembly info file is a text file (USASCII7) containing general assembly information.

The file has two columns separated by a tab (or any whitespace characters):
- Field name (first column)
- Field value (second column)

The following fields must be provided:
- STUDY: Study accession or unique name (alias) 
- SAMPLE: Sample accession or unique name (alias)
- ASSEMBLYNAME: The unique assembly name.
- PROGRAM: The assembly program.
- PLATFORM: The sequencing platform.

An example of an assembly info file:

```
STUDY   TODO
SAMPLE  TODO
ASSEMBLYNAME    TODO
PROGRAM TODO
PLATFORM    TODO
```

### Fasta file

Unannotated sequences should be submitted as a Fasta file.

The sequence name is extracted from the fasta header. For example the following header 
contains the name 'contig1':

`>contig1`

### Flat file	

Annotated sequences must be submitted using an EMBL-Bank flat file.

The sequence name is extracted from the AC * line and must be prefixed with a '_'.
For example the following AC * line defines name 'contig1':

`AC * _contig1`

## Stage 3: Validate and submit the files

Files are validated, uploaded and submitted using the [Webin command line submission interface](cli_01.html). 
Please refer to the [Webin command line submission interface](cli_01.html) documentation for more information 
about the submission process.

## Assigned accession numbers

Once the transcriptome assembly has been submitted a analysis (ERZ) accession number is immediately assigned and 
returned to the submitter by the Webin command line submission interface. 

The purpose of the ERZ accession number is for the submitter to be able to refer to their submission within the 
Webin submission service. For example, the submitter can retrieve the assigned sequence accessions 
from the [Webin XML and reports portal](prog_11.html) or from the [Webin reports service](prog_10.html) using
the ERZ accession number.

For transcriptome assemblies, long term stable accession numbers that can be used in publications are:

- Study accession (PRJ) assigned at time of study registration.
- Sample accession (SAM) assigned at time of study registration.
- Sequence accession(s) assigned once the transcriptome assembly submission has been fully processed by ENA.

Submitters can retrieve the sequence accession numbers from the [Webin XML and reports portal](prog_11.html) 
or from the [Webin reports service](prog_10.html). These accession numbers are also send to the submitters by
e-mail.

## Validation rules

### Sequence validation rules

Sequences must:
- have unique names within an assembly
- be at least  200bp long
- not have terminal Ns
- consist of bases: 'a','c','g','t','u','b','d','h','k','m','n','r','s','v','w','y'
