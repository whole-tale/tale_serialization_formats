# Overview

This repository is for the documentation and design about the Tale's export structure and metadata format. There are many different specifications and custom ways to accomplish each; this document focuses on RDF in JSON-LD as the Tale metadata format and [BagIt-RO](https://github.com/ResearchObject/bagit-ro/) as the export standard. 

[metadata_formats](https://github.com/whole-tale/tale_serialization_formats/tree/master/metadata_formats): contains examples using both the RO and schema.org metadata formats. The RO examples illustrate difference between locally and externally referenced data.

[export_formats](https://github.com/whole-tale/tale_serialization_formats/tree/master/export_formats): contains examples of Tales exported with different specifications

***
# Metadata Format
When exporting and publishing a Tale, enough information needs to be saved such that the Tale can be brought back into Whole Tale and reconstructed. There are many different formats for storing this information ranging from text, yaml, xml, and JSON-LD. Each format has a number of strengths and weaknesses however, this document only considers JSON-LD under a number of different vocabularies.


### Strengths
Tightly structured representation

Opens doors for linked data

Gives the ability to use established vocabularies

Compatible with file structure formats such as bagit-ro

Opens potential for tighter integration with publishers


### Weaknesses
Difficult/time consuming to maintain

Whole Tale doesn't have a persistent URI space for commons objects (Tale, Author, Environment, etc)

There (currently) aren't any applications for using a Tale's JSON-LD representation

### Schema.org
The schema.org vocabulary is standard for describing elements/objects on webpages. It provides a basic set of terms for common web elements such as `datasets`, `author`, `organization`, etc... Although the vocabulary spans a number of domains, it fails to provide a concrete way of aggregating resources and fails to provide a vocabulary to describe features of software&data (eg file paths). Some of the definitions (see [Entrypoint](https://schema.org/EntryPoint)) are also geared more towards web applications than raw data.

Instead of using _only_ schema.org, it's more convenient to use it among other vocabularies, shown in the RO Bundle section. 


#### Example: 
A Tale described in schema.org can be found in [metadata_formats/schema_org](https://github.com/whole-tale/tale_serialization_formats/tree/master/metadata_formats/schema_org)


### Research Object Bundle 1.0 + Schema.org
Many of shortcomings in schema.org can be addressed by introducing the [Research Object Bundle]() vocabulary, which also imports a number of other vocabularies. It provides terms that are geared towards research artifacts, adding terms such as `orcid` and `path`. The bagit-ro directory specification also uses this format, which allows us to couple the two. In this case, the metadata document follows the `OAI-ORE` specification.

#### Differences from schema.org
1. `@id` is replaced with `uri`
2. `path` is defined for files
3. Addition of `orcid` (when available)
4. Addition of `aggregates` (Files are now aggregated by the metadata document)

#### Examples: 
RO examples can be found in [metadata_formats/ro](https://github.com/whole-tale/tale_serialization_formats/tree/master/metadata_formats/schema_org)

***
# Export Format:
When a Tale is exported to disk, we have a number of ways to structure the data. This document discusses using BagIt and bagit-ro as the specification.

### Strengths
Standards-based

Gives us an “archival” and “metadata” face

It’s just a zip file

### Weaknesses
For export, the researcher doesn’t care that it’s a BagIt

Complicated for the researcher to understand, if they look at it

Standard but not familiar

Lots of features we may not care about

Can’t use fetch because, for example, the URI could be a Globus identifier.

pid-mapping and fetch.txt do not really cover our external data needs.

WT would need to implement PIDs

For the average user “data” (payload) will be as confusing as home/jovyan/work/data

Doesn’t reflect the actual Tale structure. We’ve made a big deal about the UI and in-container structures matching, but for some reason it’s OK for the export to be something totally different.

BagIt is for archive and exchange – we won’t be archiving.

We’re basically using it for download

### BagIt
The BagIt specification can be used as a basic archival format for the Tale. The top level directory has the traditional tag files, and the Tale data goes inside the payload directory.

An example of a Tale that has been exported into a bag with local data can be found in [export_formats/bagit_local](https://github.com/whole-tale/tale_serialization_formats/tree/master/export_formats/bagit_local)


### Bagit-RO
The BagIt model can be expanded by considering the work done by the Research Object group on [BagIt-RO](https://github.com/ResearchObject/bagit-ro). This format adds additional directory structure, such as `metadata` and `provenance`. 

#### Differences from BagIt
1. Addition of the `metadata` and sub-folders

#### Examples:
An example of a Tale with local data can be found in [export_formats/ro_local](https://github.com/whole-tale/tale_serialization_formats/tree/master/export_formats/ro_local)

An example of a Tale with external data can be found in [export_formats/ro_external](https://github.com/whole-tale/tale_serialization_formats/tree/master/export_formats/ro_external)

***
# Relation to Publishing
The export format and metadata format are potentially linked to publishing the following ways:
1. Some publishers allow publishing zipped archives. In this case, the exported Tale is uploaded to the repository
2. Some publishers support custom resource maps. In this case, information from the Tale metadata document should be included in the publisher's resource map.
3. Some publishers support customized provenance. 

## DataONE

### Data Duplication & Transcription Between ORE Files

In order to utilize the publisher's existing metadata system, some of the fields from the Tale's ORE will be transcribed into the publishers' ORE. Because the original Tale metadata document is present in the package, any data that is transcribed, is also duplicated. It was confirmed that adding additional namespaces to the ORE shouldn't be a problem.


##### Transcriptions (Tale ORE -> Publisher ORE)
    1. @uri will need to be mapped from a file path to the URI that the publisher assigned
    2. Provenance statements should be transcribed from the metadata document to the DataONE ORE
    

