---
title: "Archiving Cookbook FAQ"
keywords: archiving, guidance, cookbook, tools, FAQ
tags: [guidelines, archiving, data, NCEI, tools, FAQ]
toc: false
summary: Frequently asking questions on the NCEI Archiving Process
---


## General Questions

#### Real time vs delayed mode?

NCEI would like all of the data, both delayed QA/QC data and real-time data.

#### Directory structure?

NCEI prefers the files to be organized by platform, with each platform being its own directory. See the example below:

 ![](./faq-1-0.png)

<!--   Preferred directory structure

```
    .
    ├── PR1
    │   ├── DSG_PR1.accelerometer2.realtime.nc
    │   ├── DSG_PR1.diagnostics.realtime.nc
    │   ├── DSG_PR1.doppler.realtime.zcell36.nc
    │   ├── DSG_PR1.met.pr.realtime.nc
    │   ├── DSG_PR1.sbe37.realtime.1m.nc
    │   ├── DSG_PR1.waves.mstrain.v1.realtime.nc
    │   └── DSG_PR1.waves.triaxys.realtime.nc
    ├── PR2
    │   ├── DSG_PR2.accelerometer2.realtime.nc
    │   ├── DSG_PR2.diagnostics.realtime.nc
    │   ├── DSG_PR2.doppler.realtime.zcell36.nc
    │   ├── DSG_PR2.met.pr.realtime.nc
    │   ├── DSG_PR2.sbe37.realtime.1m.nc
    │   ├── DSG_PR2.waves.mstrain.v1.realtime.nc
    │   ├── DSG_PR2.waves.triaxys.realtime.nc
    ├── PR3
    │   ├── DSG_PR3.accelerometer2.realtime.nc
    │   ├── DSG_PR3.diagnostics.realtime.nc
    │   ├── DSG_PR3.doppler.realtime.zcell36.nc
    │   ├── DSG_PR3.met.pr.realtime.nc
    │   ├── DSG_PR3.sbe37.realtime.1m.nc
    │   └── DSG_PR3.waves.mstrain.v1.realtime.nc
    ├── VI1
    │   ├── DSG_VI1.accelerometer2.realtime.nc
    │   ├── DSG_VI1.diagnostics.realtime.nc
    │   ├── DSG_VI1.doppler.realtime.zcell40.nc
    │   ├── DSG_VI1.met.pr.realtime.nc
    │   ├── DSG_VI1.sbe37.realtime.1m.nc
    │   ├── DSG_VI1.waves.mstrain.v1.realtime.nc
    │   └── DSG_VI1.waves.triaxys.realtime.nc
    └── VIA
        ├── DSG_VIA.diagnostics.cbibs.realtime.nc
        ├── DSG_VIA.doppler.cbibs.realtime.nc
        ├── DSG_VIA.met.cbibs.realtime.nc
        ├── DSG_VIA.waves.cbibs.realtime.nc
        └── DSG_VIA.wqm.cbibs.realtime.nc

``` -->

#### What should we put in the archive section of the certification?

In order to be certified, a RICE must provide a Standard Operating Procedure (to be no more than 2 pages) that identifies (in general terms) their process for archiving data, identifies aggregated data sets to be archived, provides a timeline for completion of the necessary agreement with NCEI or other appropriate national data archive center.  An approved agreement with NCEI must be in red prior to being approved as a certified RICE. The approved agreement with NCEI will be in one of the following formats (**B** and **C** can be obtained from the ATRAC system):

&nbsp;&nbsp;&nbsp;**A:** Submission Information Form (deprecated);<br>
&nbsp;&nbsp;&nbsp;**B:** Request to Archive; or<br>
&nbsp;&nbsp;&nbsp;**C:** Data Submission Agreement.

Below are examples of the various archive states the archival of RICE data could be in. NCEI has provided their recommendation of what information to include in the certification, in some cases, specific text to include.
  1. **If the region does not have an agreement with NCEI.**
     * Include the following information:
        1. List of parameters/observations being collected.
        2. Processing steps/quality control including final format.
        3. Timing of data submissions and approximate sizes.
        4. Development of data documentation (metadata).
        5. Data disposition (path to archive center).
        6. Data affiliations, including both institutions and individual persons whose names will be associated with the data set in some way, e.g., where did it come from, where does it go, etc.
  2. **If the region is under negotiations with NCEI to archive the data.**
     * Include the information requested above and the current Request to Archive documentation from the ATRAC system.
     * Provide an estimated date as to when the RICE expects to be archiving their data.
  3. **If the region has an approved Request to Archive, but NCEI has not implemented the archive procedure yet.**
     * Include the approved Request to Archive.
     * Add the following text to the certification (replacing _RICE_ with your region name): _RICE **has completed the required documentation for the** (description of data files) **data files in the NCEI ATRAC system. The Request to Archive (attached here) has been approved and NCEI is developing the archival process. We expect the automated archival of** RICE (description of data files) **to be operational by the end of** (give a date when we can expect the data to be archived, for example the calendar year (January 2017))_.
  4. **If the region has an already existing agreement with NCEI and will be making adjustments to that process after the certification is submitted.**
     * Include the current agreement to the certification documentation.
     * Include a statement that details how the current framework is being renegotiated with NCEI and the documentation will be updated to reflect any changes.
  5. **If the region has established an agreement with NCEI and are actively archiving data.**
      * Include the approved Request to Archive document exported from the ATRAC system.
      * Include the Submission Agreement document exported from the ATRAC system.
      * Add the following text to the certification (replacing _RICE_ with your region name): _RICE **already archives** (description of data) **through NCEI and this process is documented in the accompanying Request to Archive and Submission Agreement Form updated** (date of last update to submission agreement form)_.

------------------------------------------------------------------------------------------------------------------------

## Data File Questions

#### What do you recommend for file naming conventions?

While there are no specific requirements for file name conventions, NCEI recommends that there are no special characters in the file names. While there are various perspectives on what a file name should include in it, NCEI recommends simple unique file names. Something along the lines of:

<pre><b>
    organization_platform_YYYYMMDD-YYYYMMDD.nc

    where,

          organization      = organization that collected the data

          platform          = name of the platform which collected the data

          YYYYMMDD-YYYYMMDD = four digit year, two digit month, and two digit day for the start and end times of the file.

          nc                = type of file (e.g. netCDF)
</b></pre>

There are various websites available which provide guidance on file name conventions, feel free to use the resources below for more information.
 * **Stanford University Library**: https://library.stanford.edu/research/data-management-services/data-best-practices/best-practices-file-naming
 * **Perdue Library**: http://guides.lib.purdue.edu/c.php?g=353013&p=2378293
 * **Oregon State University**: http://oregonstate.edu/cws/training/faq/what-are-good-file-naming-conventions

#### Who do we list as the creator_name in the netCDF file?

The person generating the files.

#### For the NCEI netCDF template V2.0, how should we populate the various publisher attributes (publisher_name, publisher_institution, publisher_url, publisher_type, publisher_email, publisher_phone)?

Use the Regional Association information to populate the publisher attributes; see below for an example, the information used to populate these attributes are generic entries used to give you an idea of what we are looking for:

<pre><b>
        publisher_name: NANOOS Data Manager
        publisher_url: http://nanoos.org
        publisher_email: dmac@nanoos.org
        publisher_phone: 555-555-5555
        publisher_type: position
        publisher_institution: NANOOS
</b></pre>

#### What do we list in the projects attribute?

Any associated projects that are affiliated with the data in that file.

#### What is the right thing to do for variables that have no CF `standard_name`?

For example, **phycoerythrin**. The units the instrument reports in are **Relative Fluorescence Units (RFU)**, which are not UDUNITS as far as I can tell.  What is the right thing to do for variables like this?

Our recommendation for variables with no CF `standard_name` is to:
 1. Double check that it doesn't exist in the [CF standard_name list](https://cfconventions.org/standard-names.html). Keep it mind a variation of the variable could be applicable in some cases.
 2. (Optional) Request the standard_name to be added to the CF standard_name table. See [this repository](https://github.com/cf-convention/discuss) for instructions on requesting new `standard_name` terms. We can assist with this if you would like to pursue it.
 3. If the name, or variation of the name, doesn't exist in the list please use the long_name attribute to clearly identify what the variable contains.
 4. Populate the units attribute with the appropriate descriptive units for the variable. To be CF compliant the units attribute must be in a compliant UDUNITS format.
 5. Remove the standard_name attribute.

#### What should we list in the institution global attribute?

Our recommendation is to populate the institution global attribute with the associated institution that collected the data. This could be a list of institutions which collected the data:

<pre><b>    institution: GLOS,U-GLOS, University of Michigan Marine Hydrodynamics Laboratories </b></pre>

Or, one institution:

<pre><b>    institution: University of South Florida(USF) Coastal Ocean Monitoring and Prediction System </b></pre>
