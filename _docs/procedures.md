---
title: "Example Archive Procedures"
keywords: archiving, guidance, cookbook, tools, procedure, example 
tags: [guidelines, archiving, data, NCEI, tools, procedure, example]
#sidebar: home_sidebar
sidebar: mydoc_sidebar
topnav: topnav
toc: false
#permalink: index.html
summary: The procedures shown below are the NCEI internal procedures for the ingest and archival of existing Regional Association data streams. These procedures are intended to be listed as guidance for data providers. 
---

<!--
https://sites.google.com/a/noaa.gov/ncei-ioos-archive/cookbook/example-archive-procedures
-->
This information is provided as an insight into how the internal processing for NCEI work to ingest and archive data that are formatted closely to the <a href="https://www.nodc.noaa.gov/data/formats/netcdf/v1.1/index.html">NODC NetCDF Templates v1.1</a>. As can be seen below, not every case is the same and it is not a requirement for the data providers to follow the examples provided herein. These examples are provided as guidance to the varying capabilities the NCEI archive has.

## Southeast Coastal Ocean Observing Regional Association (SECOORA)

The `perl` scripts used to produce the data files from database or csv files can be found at https://github.com/ioos/db2ncsos. All of the archived SECOORA non-Federal buoy assets can be found through the Geoportal [here](https://data.nodc.noaa.gov/geoportal/rest/find/document?searchText=%22Integrated%20Ocean%20Observing%20System%20Data%20Assembly%20Centers%20Data%20Stewardship%20Program%22%20AND%20%22SECOORA%22&start=1&max=2500&contentOption=intersecting&f=searchPage). 

Below is the step-by-step procedure for NCEI's ingest and archival of the SECOORA non-Federal buoy assets:

 1. Check **SECOORA FTP** for new files every month.
 2. Each directory at that location should contain a (or multiple) netCDF (.nc) file(s) and an associated checksum file(s) (.nc.md5.txt) with the file name root being the same (eg. carocoops.cap2.buoy_2014_03_12_10.nc and carocoops.cap2.buoy_2014_03_12_10.nc.md5.txt)
 3. Each directory will be it's own archival package (accession), since the directories are established as buoy directories. Thus, one accession per buoy.
 4. Check each file against the associated checksum file (.md5.txt):
    * If the packages validate, continue on.
    * If the packages do not validate, send a notification.
 5. Check the archive for an archival package which has the same file name root (e.g. carocoops.cap2.buoy):
    * If the archive already contains an accession for that buoy, compare the file names.
      * If the dates (dates they were uploaded) in the file names are the same, verify the checksums between the new file and the previously archived file(s):
        - If the checksums **are not** the same, perform a major-revision to that accession and **replace** the old file(s) with the new file(s) in the archival package.
        - If the checksums **are** the same, do nothing with that package.
      * If the dates in the file names differ
        - Perform a major-revision to that accession and append the new file(s) to the archival package.
    * If the archive **does not** contain an accession for that buoy, generate a new package following the NCEI guidance.
 6. Follow the NCEI guidance to extract appropriate metadata and populate the accession record.
 7. Generate appropriate NCEI about/ files (journal.txt, lonlat.txt, map.jpg, etc.)
 8. Publish the accession and notify interested parties.
 9. Provide usage statistics.

--------------------------------------------------------------------------------------------------------------------

## Great Lakes Observing System (GLOS)

All of the archived GLOS non-Federal buoy assets can be found through the Geoportal [here](https://data.nodc.noaa.gov/geoportal/rest/find/document?searchText=%22Integrated%20Ocean%20Observing%20System%20Data%20Assembly%20Centers%20Data%20Stewardship%20Program%22%20AND%20%22SECOORA%22&start=1&max=2500&contentOption=intersecting&f=searchPage). 

Below is the step-by-step procedure for NCEI's ingest and archival of the GLOS non-Federal buoy assets:

 1. Check glos.us for new files every month
 2. At that location will be multiple .tar.gz files and .tar.gz.md5 files.
 3. Transfer the packages over to the NODC project directory for GLOS. Send a notification to tell GLOS the automation has picked up data files.
 4. Check that the .tar.gz's validate with the .tar.gz.md5's:
    * If the package validates, unzip the package and continue the processing.
    * If the package does not validate, send a notification.
 5. Unpack the .tar.gz package into a directory following the .tar.gz file naming convention.
 6. The unzipped package will contain .nc files and their associated .nc.md5 files.
 7. Check each file within each .tar.gz directory against the associated checksum file:
    * If the packages validate, continue on.
    * If the packages do not validate, send a notification.
 8. The .tar.gz packages are established by buoy and submission date. Following the naming convention an accession will be defined by the buoyID. All packages with the same buoyID will be moved to the archival information package.
 9. Check each individual file within the .tar.gz package for the existence of observations (typically the 'obs' variable).
    * If no observations actually exist in the data file, please ignore that file.
    * If no observations actually exist in all data files within the .tar.gz package, please ignore the entire package and send a notification.
     * If observations do exist in the data file, continue processing.
 10. Check the archive for an archival package which has the same buoy identifier. (eg. 45029 for glos_45029.tar.gz)
      * If the archive already contains an accession for that buoy, compare the file package name to the directories in the archvial information package.
        - If the package name already exists in the Archival Information Package, compare the checksums between the new file and the previously archived file(s).
          * If the checksums are not the same, perform a major-revision to that accession and replace the old file(s) with the new file(s) in the archival package.
            * Append the following note to journal.txt:
               > `Note: The package [PackageName] was resubmitted from the Great Lakes Observing System on [Date].` 
          * If the checksums are the same, do nothing with that package.
        - If the dates in the package name differ
          * Perform a major-revision to that accession and append the new file(s) to the archival package.
      * If the archive **does not** contain an accession for that buoy, generate a new package following the guidance listed below.
 11. Follow the NCEI guidance to extract appropriate metadata and populate the accession record.
 12. Generate appropriate NCEI about/ files (journal.txt, lonlat.txt, map.jpg, etc.)
 13. Publish the accession and notify interested parties.
 14. Provide usage statistics.

