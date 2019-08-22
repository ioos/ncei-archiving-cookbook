---
title: "Standard Practices for Ensuring Data Integrity"
keywords: archiving, guidance, cookbook, tools, procedure, integrity
tags: [guidelines, archiving, data, NCEI, tools, procedure]
toc: false
#permalink: index.html
summary: The mission of NCEI is to ''acquire, process, preserve, and disseminate oceanographic data.'' Thus, the acquisition of data from data providers is an important part of the NCEI mission. In order to maintain the integrity and to guarantee availability of the data that NCEI acquires, as well as to ensure the security of both NCEI and remote computer systems, NCEI has a few recommendations for standard practice for data acquisition.
---


## Background

 1. NCEI recommends the data provider will make the data files available so that NCEI can "pull" the data from the remote site. That is, NCEI will initiate the network transaction, copying the files from the remote site to an NCEI server. NCEI will use ftp, http, https, rsync or other appropriate file transfer protocol to transfer the files from the remote site. NCEI will schedule the transfers to balance timely acquisition against resource usage.
    * One reason NCEI prefers to "pull" the data is because NCEI operates multiple data acquisition servers in an effort to guarantee that no data are ever lost due to unexpected downtime of any one of its servers. Even if there is a system outage in one location the data continue to be acquired at the other locations. In addition, if NCEI adds another redundant data acquisition server the data providers will not have to change their configurations.
2. NCEI strongly recommends using standard mechanisms to guarantee data integrity.
    * Every data file should be accompanied by a computed [cryptographic "checksum"](https://en.wikipedia.org/wiki/Cryptographic_hash_function) (link points you to a Wikipedia description if you are interested in diving a bit deeper). The use of a checksum will prevent incomplete or otherwise corrupted data files from being acquired from data providers. These checksums must be made available concurrently with the data files. NCEI software will validate the data files against their checksums in order to maintain data integrity.
    * NCEI currently recommends the use of the SHA-2 family of cryptographic hash functions. (MD5 and SHA-1 have been formally deprecated by NIST.) We are able to use SHA-1, SHA-256, or any other cryptographic hash function which is supported at NCEI. (See [Toolbox](./practices.html#unix) section below.)
    * NCEI recommends accompanying your data files with a "**manifest**", a file containing the names and checksums of your data files (see [example of a simple **`manifest.xml`**](./SubmissionManifest-simple.xml). Using the "**manifest**" fulfills two needs:
       - The "**manifest**" lists the data files in a given package. Thus, there is no question which files belong to the package. Files which are not in the package can be safely ignored, and only files in the package will be processed.
       - The "**manifest**" includes the checksums of the files in the package. The integrity of each file can be determined. And changes to files can be determined by comparing the checksum in the "**manifest**" against the checksum of any file previously downloaded by NCEI; if the checksums are different, the file is presumed to have changed and will be downloaded by NCEI to replace the original file.
 3. NCEI requests data to be available for a minimum number of days in order to ensure that the data can be acquired even in the event of a short power outage, system failure, network failure, or other resource problem. When the system returns to normal operation state, NCEI will automatically attempt to acquire the most recent data from the data providers. We have found that three (3) days is usually sufficient to guarantee successful acquisition, but the longer the period of availability the better, preferably at least one (1) month.
 4. NCEI recommends that if a user ID and password is required to access the data to be acquired, that this user ID and password not be transferred over unencrypted connections. Thus, ftp should not be used because ftp sends the user ID and password over an unencrypted connection. However, https (http + SSL) can be used, because https is encrypted. rsync over ssh can also be used in this way.
<br>
<br>


## Toolbox:
--------------------------------------------------------------------------------------------------------------
### UNIX

One simple way to generate checksums for a directory of data files (on most UNIX-based operating systems) is to use the `sha256sum(1)` or `sha384sum(1)` tool:

     sha256sum * > SHA256SUMS

Doing so will allow the use of the "check" mode of the `sha256sum` tool to verify the checksums of the files after they have been transferred:

     sha256sum -c SHA256SUMS

Another common method of storing checksums is to create a file having the suffix "`.sha256`" for each data file in the collection. Each "`.sha256`" file contains the SHA-256 checksum for the corresponding data file. For example, say the following data files are to be acquired:

```
datafile01.nc
datafile02.nc
datafile03.nc
```

Then the following SHA-256 checksum files would need to be created:

```
datafile01.nc.sha256
datafile02.nc.sha256
datafile03.nc.sha256
```

The following shell command will generate these files:

      for i in * ; do sha256sum $i > $i.sha256 ; done

Similarly, SHA-384 or SHA-512 checksums can be generated using the `sha384sum(1)` or `sha512sum(1)` commands on most UNIX-based operating systems:

      for i in * ; do sha384sum $i > $i.sha384 ; done

-----------------------------------------------------------------------------------------------------------------

### WINDOWS

Similar commands to that described under the UNIX-based operating systems, above, are available for Windows.

#### Third party utilities

There are numerous third party utilities produced for the WINDOWS-based operating system which can be useful for generating manifest files. For example, `Cygwin64` - a large collection of GNU and Open Source tools which provide functionality similar to a Linux distribution on Window.

#### System tools

One simple way to generate checksums for data files (on most WINDOWS-based operating systems) is to use the `certutil.exe` -- a command-line program that is installed as part of Windows Certificate Services. Among other features, the `certutil.exe` is able to generate and display a cryptographic hash over a file.

```
Usage:
  CertUtil [Options] -hashfile InFile [HashAlgorithm]
  Generate and display cryptographic hash over a file

Options:
  -gmt              -- Display times as GMT
  -seconds          -- Display times with seconds and milliseconds
  -v                -- Verbose operation
  -privatekey       -- Display password and private key data

CertUtil -?              -- Display a verb list (command list)
CertUtil -hashfile -?    -- Display help text for the "hashfile" verb
CertUtil -v -?           -- Display all help text for all verbs
```

The following examples show how to use `certutil.exe` for calculating various checksums and creating  the "**manifest**" files:

SHA256 checksum for one file (`data.txt` in this example)
:
```
>certutil -hashfile data.txt SHA256
SHA256 hash of file data.txt:
c0 20 8f 75 aa 8b e1 5b 74 82 68 b0 85 4f ab f3 0e 8d 85 18 be 1b cf eb b9 fe 2e d3 91 7a ec c2
CertUtil: -hashfile command completed successfully.
```

SHA384 checksum for the same file
:
```
>certutil -hashfile data.txt SHA384
SHA384 hash of file data.txt:
ec ae b9 79 60 85 57 f3 e8 89 32 f9 86 fb 58 81 d5 16 ef 09 06 bf de 3b c5 4e f0 2d cb c0 a6 9a ac 0a 2b 41 9b ec 27 05 11 0f 3a 2f f8 7b 1f 64
CertUtil: -hashfile command completed successfully.
```


SHA512 checksum for the same file
:
```
>certutil -hashfile data.txt SHA512
SHA512 hash of file data.txt:
82 27 dd 81 07 80 37 42 55 65 66 17 8b 9e 32 5e 1e 29 01 17 77 41 96 b0 e2 d2 4a 4d 41 e9 1d 17 82 28 f0 7c ba d2 8d 8e 75 a5 f0 79 69 6b 33 8f ff ad b0 21 91 20 1e dd b5 c3 11 7e 87 71 e5 00
CertUtil: -hashfile command completed successfully.
```

Recursive manifest file for a directory of files
:
```
>for /F %i IN ('dir [DIRECTORY PATH]\*.nc /s/b') do (certutil -hashfile %i SHA384 | find /v "CertUtil") >> manifest.txt
```
where
   * `dir [DIRECTORY PATH]\*.nc /s/b` ---	 provides the fill path to all the nc files in [DIRECTORY PATH];
   * `certutil -hashfile %i SHA384` --- calculates the SHA384 hash value for each file;
   * `find /v "CertUtil"` --- removes the line `CertUtil: -hashfile command completed successfully`;
   * `>> manifest.txt` --- writes the output to the file `manifest.txt`

-----------------------------------------------------------------------------------------------------------------

### BagIt

According to Wikipedia, _"BagIt is a hierarchical file packaging format designed to support disk-based storage and network transfer of arbitrary digital content. A "bag" consists of a "payload" (the arbitrary content) and "tags", which are metadata files intended to document the storage and transfer of the bag. A required tag file contains a manifest listing every file in the payload together with its corresponding checksum."_

For short Library of Congress video clip describing the **BagIt** capability, check out [here](http://www.digitalpreservation.gov/multimedia/videos/bagit0609.html), or on [YouTube](https://youtu.be/l3p3ao_JSfo).

For those Python gurus, there is a [Python implementation](https://github.com/LibraryOfCongress/bagit-python) of the **BagIt** utility.
