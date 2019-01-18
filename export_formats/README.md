
# Exported Tales Following the Research Object Standard

### ro_external
Describes a Tale whose data was never brought into the Whole Tale system. The remote files are listed in `fetch.txt` and are additionally defined in `metadata/manifest.json`.

### ro_local
Describes a Tale whose data existed in the Whole Tale system at the time of publishing. The files are listed under `data/workspace`, but do not contain any data; they are shown only to give an example. To save space, each file points to the location where it can be downloaded. 

### Differences betwenen ro_external and ro_local

The main difference between the two, at face value, is that one references external data while the other contains it. This small difference propagates into `manifest.json` the following ways

1. In ro_remote, the `uri` points to the location of where the file can be downloaded from. To describe where the file _should_ go, `bundledAs` is used to provide the original filename and folder.
2. In ro_local, the relative path of the file is given as the `uri`. The name of the file is also provided with `filename`.

For example,

```
  {
    "uri":"data/workspace/L-L1_LOSC_4_V1-1167559920-32.hdf5",
    "@type":"schema:CreativeWork", 
    "filename":"L-L1_LOSC_4_V1-1167559920-32.hdf5" 
  }
 ```
 
 ```
    {
        "uri": "https://losc.ligo.org/s/events/GW170104/L-L1_LOSC_4_V1-1167559920-32.hdf5",
        "@type": "schema:CreativeWork",
        "bundledAs": {
          "folder": "data/workspace/",
          "filename": "L-L1_LOSC_4_V1-1167559920-32.hdf5"
        }
    }
 ```



##### Other Notes

1. It should be possible to use `bundledAs` for local files to separately define the path + filename.