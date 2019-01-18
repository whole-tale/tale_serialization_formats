# A Tale Described with Research Object

There are two examples of the `LIGO Tutorial` Tale represented as JSON-LD using the RO vocabulary with schema.org.
For examples of how RO fits in with baggit, navigate to the [export_formats](https://github.com/whole-tale/tale_serialization_formats/tree/master/export_formats) directory from the root.
### local_data
This is an example of a Tale that has all of the data within Whole Tale. This data is exported to disk in `data/workspace` and is described at the top level with `tale.json`. 


### remote_data
This is the same LIGO Tale as the one in `local_data`, but it is assumed that the data was never downloaded into Whole Tale. To compensate for this, the remote files are described in the file aggregation portion in `tale.json`.


![linked_data](https://github.com/whole-tale/tale_serialization_formats/blob/master/metadata_formats/ro/images/ld_visual.png)

### Other Notes

There are a number of additional properties that can be added to the resource maps however, aren't essential for Tale ingestion. Examples include adding
1. `mediatype` to each aggregated file
2. `createdBy` to each aggregated file
3. Annotations about each file
