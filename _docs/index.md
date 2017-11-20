---
title: "Archiving your data at NCEI"
keywords: homepage
tags: [guidelines, archiving, data, NCEI]
#sidebar: home_sidebar
sidebar: mydoc_sidebar
topnav: topnav
toc: false
#permalink: index.html
summary: This is a guide for IOOS Regional Association Data Managers 
---


## Big Picture Perspective

Per  NOAA Administrative Order 212-15 and the Data Management Plan Procedural Directive, each new data acquisition project needs a Data Management Plan that identifies what data will be collected, who and where data will be collected, and where and when data will be archived. NCEI can accept data at the immediate end of the data collection process, at the end of the qa/qc process, when a "final version" of data are released to the public, or when the data collecting office no longer wants or is able to keep data locally.

Some key points to keep in mind when managing data:
 - Many Program and Project Offices provide good examples and guidance for managing observation data and metadata for marine scientists. While each program, project, and organization may have specific requirements for documenting, organizing, archiving and providing access to data funded by them, some fundamentals are common across the data management spectrum:
   - Plan for managing and documenting data collected at the beginning of the project, not the end
   - Designate a person to be responsible for managing data and information for the project
 - Need assistance with developing a Data Management Plan? Take a look at some of the resources below for good recommendations.
   - [IODE Guidelines for a Data Management Plan](http://www.iode.org/index.php?option=com_oe&amp;task=viewDocumentRecord&amp;docID=16859)
   - [NSF data management planning tool from DataONE](https://www.dataone.org/data-management-planning)
   - [Training resources](https://dmptool.org/community_resources)
   - [The UK Digital Curation Centre](http://www.dcc.ac.uk/resources/how-guides/develop-data-plan)
   - [NOAA Data Sharing Policy](https://nosc.noaa.gov/EDMC/PD.DSP.php)
 - To get an idea as to how NCEI ingests and archives data in an automated way, see [Example Archive Procedures](https://sites.google.com/a/noaa.gov/ncei-ioos-archive/cookbook/example-archive-procedures) for examples.
  
 -----------------------------------------------------------------------------------------------------------------

## Selecting the Data to be Archived

For the intentions of this procedure, we want to focus on region owned/managed observational data assets that are less than 10 TB per year in size. Use the following guidelines to determine which data sets should be included in the archive procedures:
 - If the data is already being submitted to a Data Assembly Center (DAC) that has an archive agreement with NCEI, verify your data will be incorporated into that archival process.
 - If the data will not be archived through a DAC, proceed with the steps below.

Below is a diagram of the pathway for the various types of IOOS RA data to get to the NCEI archive:

<!-- ![](./DataArchiveDecisionTreeForGoogle.jpg) -->

<a href="./DataArchiveDecisionTreeForGoogle-large.png"><img alt="thumb" src="./DataArchiveDecisionTreeForGoogle-small.png" height="20%"></a> 

(click for full-size image)
{: style="color:blue; font-size: 80%; text-align: center;"}

---------------------------------------------------------------------------------------------------------

## Formatting your Data

Whenever possible, data should be recorded or translated to scientific units (instead of raw sensor voltages), and be the best, science-quality version of these data available at the time of submission. Ancillary information that are critical for accurate interpretation and reuse of the data, such as calibration information or temperature and pH scale for sensor measurements, should be noted in the data files themselves or in associated documentation files.&nbsp;In order to fully document the data that has been collected, NCEI provides the following recommendations:
 - Use a consistent and unique file naming convention for each file. (e.g. `carocoops.cap2.buoy_2014_03_28_05.nc`) 
   - See the [Cookbook FAQ on recommended file naming conventions](https://sites.google.com/a/noaa.gov/ncei-ioos-archive/cookbook/cookbook-faq) for more details.
 - NCEI highly recommends formatting your data following the [NCEI NetCDF Templates v2.0](https://www.nodc.noaa.gov/data/formats/netcdf/v2.0/). These best practices capture NCEI's experience in providing long-term preservation, scientific quality control, product development, and multiple data re-use beyond its original intent.
 - Data should be in compliance with the [IOOS compliance checker](https://github.com/ioos/compliance-checker), specifically the [NCEI plugin for the IOOS compliance checker](https://github.com/ioos/cc-plugin-ncei).
 - To see how compliant your files are, use the [Online IOOS Compliance Checker](https://data.ioos.us/compliance/index.html).
 - For time-series station data, NCEI recommends using the [timeSeries Orthogonal template](https://www.nodc.noaa.gov/data/formats/netcdf/v1.1/timeSeriesOrthogonal.cdl). For other types of data follow the [NODC NetCDF decision tree](https://www.nodc.noaa.gov/data/formats/netcdf/v1.1/decision_tree_high_res.pdf).
 - See [Available NetCDF Tools](https://sites.google.com/a/noaa.gov/ncei-ioos-archive/cookbook/netcdf-tools) for some examples on how to generate, visualize, and use netCDF files.

---------------------------------------------------------------------------------------------------------------------

## Providing Data Integrity

The mission of NCEI is to "acquire, process, preserve, and disseminate oceanographic data." Thus, the acquisition of data from data providers is an important part of the NCEI mission. In order to maintain the integrity and to guarantee availability of the data that NCEI acquires, as well as to ensure the security of both NCEI and remote computer systems, NCEI has a few recommendations for standard practice for data acquisition:
 - NCEI uses a 'manifest' to list the data files to be archived, and provide checksums of the files in the package to validate the transfer was successful.
 - The relative path to the data files should be described in the manifest. If the data files are in a directory structure below the manifest file, we need to know where the data files are in relation to the manifest. If no relative path to the data files is described, NCEI will assume that the data and manifest are in the same directory.
 - There are two options when determining how you want to generate your manifest files:
   1. Generate the manifest files on a per file basis.
      - One text file for each netCDF file, which contains the checksum followed by a space and the netCDF file name. See the example at [NCEI Acquisition Standards](https://sites.google.com/a/noaa.gov/ncei-ioos-archive/cookbook/data-integrity).
      - The naming convention for this file follows the same name as the netCDF file followed by `.sha`, indicating it is a checksum file.
      - NCEI has been using this construct for the current archive automations with GLOS and SECOORA:
           - For example, the manifest for the netCDF file [`enp.wiwf1.met_2015_06_01_18.nc`](https://sites.google.com/a/noaa.gov/ncei-ioos-archive/cookbook/enp.wiwf1.met_2015_06_01_18.nc?attredirects=0&d=1) would be [`enp.wiwf1.met_2015_06_01_18.nc.md5`](https://sites.google.com/a/noaa.gov/ncei-ioos-archive/cookbook/enp.wiwf1.met_2015_06_01_18.nc.md5?attredirects=0&d=1) (using an md5 cryptographic hash value).
           - NCEI's current best practice is to use the SHA-2 family of crytographic hash functions (sha256 or sha384). But, other hash functions can be used as applicable.
   2. Generate one manifest file with all filenames and checksums for the package to be archived.
       - This can be a space delimited file with the filenames, including path to the files, and checksums.
       - This can be an xml formatted file with the filenames, including path to the files, and checksums. For an xml formatted example see [this file](https://sites.google.com/a/noaa.gov/ncei-ioos-archive/cookbook/SubmissionManifest_simple.xml?attredirects=0&d=1).
  - Review [standard practices to guarantee data integrity](https://sites.google.com/a/noaa.gov/ncei-ioos-archive/cookbook/data-integrity) for more information on manifest files and integrity checks. 

---------------------------------------------------------------------------------------------------------------------

## Organizing your Data

Well-organized data promotes the use and re-use of the interested data set throughout the community. Organizing your data into logical structures that the data lend themselves to be housed in is highly recommended (don't put a square peg in a round hole). Since you, the data provider, have the best handle on how stakeholders and users alike prefer to have the data organized, we default to your recommendations.

NCEI has seen a variety of ways for data managers to format their data. Below are some points to assist in your data management:
 - Organize your data in a way that would make the most sense to a future user of these data.Organize your data into a consistent logical structure.
 - Organize your data how you would like the data represented in the archive.
 - NCEI recommends to organize your non-federal buoy assets by station and providing new files for each month, if possible.
   - This allows NCEI to generate Archival Information Packages (AIPs) based on station and a higher level of granularity.
 - Some examples of data organization are as follows
 
     >Organizing your data through Directory Structure (One Directory per Station/Buoy):
     >: _Example Directory 1_
     >
     >  ![](./Example-1.png)
     >: _Example Directory 2_
     >
     >  ![](./Example-2.png)
     >  
     >Organizing your data through File Naming Convention (One Directory for all Files, NCEI parses based on name):
     >: _File Naming Convention_
     >
     >  ![](./Example-3.png)
     >  
     >Organizing your data through packaging (zip, tar, gzip, etc):
     >: _Packaging_
     >
     >  ![](./Example-4.png)
       





## Header 3


## Header 3


## Header 3


## Header 3


## Header 3



