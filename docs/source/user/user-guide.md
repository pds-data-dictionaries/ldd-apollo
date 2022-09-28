# PDS4 Apollo Mission Dictionary User's Guide
2022-09-28 
Jennifer Ward

# Introduction
   1. Purpose of this User's Guide
      - This User's Guide provides an overview of the Apollo Mission Data Dictionary. It details how to include the dictionary in a PDS4 label, describes the organization of classes and attributes, provides definitions of the classes and attributes, and lists examples of labels that use it.  
   1. Audience
      - This User's Guide should be useful to data providers intending to archive Apollo data with PDS as well as PDS Nodes who are working with these data providers.

# Overview of the Apollo Mision Data Dictionary

The Apollo Mission Data Dictionary contains classes, attributes, and rules specific to the Apollo missions and their instruments. 
Steward: Jennifer Ward, PDS Geosciences Node, geosci@wunder.wustl.edu

# How to Include the Apollo Mission Data Dictionary in a PDS4 Label

The dictionary consists of a set of files with names in the form PDS4_APOLLO_xxxx_yyyy.ext, where
- xxxx = the PDS4 Information Model version, e.g. 1I00 
- yyyy = the Apollo Mission Dictionary version, e.g. 1000

and the file extensions are

- .csv = A comma-separated value table of dictionary attributes 
- .JSON = The dictionary contents in JSON format 
- .sch = The dictionary "rules" as an XML Schematron file 
- .txt = The report generated when the dictionary was built 
- .xml = The PDS4 label that describes this set of files 
- .xsd = The dictionary contents as an XML schema file

Only the schema and Schematron files are needed for validating a PDS4 label.

The latest version of this dictionary may be found on the PDS web site at https://pds.nasa.gov/datastandards/dictionaries/index-missions.shtml#apollo.

The following is an example showing the use of this dictionary in a PDS4 label.

```
   <?xml version="1.0" encoding="UTF-8"?>
   <?xml-model href="https://pds.nasa.gov/pds4/pds/v1/PDS4_PDS_1I00.sch" schematypens="http://purl.oclc.org/dsdl/schematron"?>
   <?xml-model href="https://pds.nasa.gov/pds4/mission/apollo/v1/PDS4_APOLLO_1I00_1000.sch" schematypens="http://purl.oclc.org/dsdl/schematron"?>    
   <Product_Observational xmlns="http://pds.nasa.gov/pds4/pds/v1"
       xmlns:apollo="http://pds.nasa.gov/pds4/mission/apollo/v1"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://pds.nasa.gov/pds4/pds/v1              https://pds.nasa.gov/pds4/pds/v1/PDS4_PDS_1I00.xsd
                           http://pds.nasa.gov/pds4/mission/apollo/v1 https://pds.nasa.gov/pds4/mission/apollo/v1/PDS4_APOLLO_1I00_1000.xsd">
```

The following is an example showing the location of the Apollo dictionary classes and attributes in a PDS4 label.

```
<Context_Area>
    <Time_Coordinates>
    <Investigation_Area>
    <Observing_System>
    <Target_Identification>
    <Mission_Area>
      <apollo:Observation_Information>
        <apollo:product_type>
      <apollo:Seismic_Parameters>
        <apollo:pse_data_type>
        <apollo:Metadata_Location>
          <apollo:metadata_file_name>
          <Internal_Reference>
            <lid_reference>
            <reference_type>
        [<apollo:ASCII_Equivalent>
          <apollo:ascii_equivalent_file_name>
          <Internal_Reference>
            <lidvid_reference>
            <reference_type>]
        OR
        [<apollo:SEED_Equivalent>
          <apollo:seed_file_name>
          <Internal_Reference>
            <lidvid_reference>
            <reference_type>]
        <apollo:station>
        <apollo:channel>
        <apollo:location>        
        <apollo:sampling_rate>
        <apollo:sample_count>
```

The namespace for the Apollo Mission Dictionary is http://pds.nasa.gov/pds4/mission/apollo/v1, abbreviated "apollo:".

# Organization of Classes and Attributes

Below is a list showing the hierarchy of classes in order of appearance in the PDS4 label. 
See the Definitions section for complete definitions.

The classes are:

- Observation_Information class
- Seismic_Parameters class
    - Metadata_Location subclass
    - SEED Equivalent subclass
    - ASCII Equivalent subclass
    
The attributes are:

- In Observation_Information
	- product_type
	    
- In Seismic_Parameters
    - pse_data_type
    - Metadata_Location
	- ASCII_Equivalent
	- SEED_Equivalent
	- station
	- channel
	- location
	- sampling_rate
	- sample_count
	     
- In Metadata_Location
	- metadata_file_name
	- pds.Internal_Reference
	
- In ASCII_Equivalent
	- ascii_equivalent_file_name
	- pds.Internal_Reference
	     
- In SEED_Equivalent
	- seed_file_name
	- pds.Internal_Reference

# Definitions

Classes (in alphabetical order)

*ASCII_Equivalent*
- The ASCII_Equivalent class contains attributes that identify and locate the ASCII data product equivalent to a given Apollo PSE SEED data product.

*Metadata_Location*
- The Metadata_Location class contains attributes that identify and locate the metadata associated with a given Apollo PSE data product.

*Observation_Information*
- The Observation_Information class provides information about a science observation.

*SEED_Equivalent*
- The SEED_Equivalent class contains attributes that identify and locate the SEED data product equivalent to a given Apollo PSE ASCII data product.

*Seismic_Parameters*
- The Seismic_Parameters class contains attributes specific to the Apollo Passive Seismic Experiment (PSE) data products.


Attributes (in alphabetical order)

*ascii_equivalent_file_name*
Apollo PSE data products are archived in their native SEED format and in a PDS-compatible ASCII format. The ascii_equivalent_file_name attribute gives the name of the file that is the ASCII equivalent of a SEED format file.
- PDS4 data type: ASCII_File_Name
- Valid values: N/A
- Minimum occurrences: 1
- Maximum occurrences: 1
- Nillable: No

*channel*
Time the signal was recorded on Earth at the ground station. Time in seconds since the beginning of the epoch (1 January 1970). The timing can be negative for early in the mission.
- PDS4 data type: ASCII_Short_String_Collapsed
- Valid values: ATT, MH1, MH2, MHZ, SHZ
    - ATT - Time the signal was recorded on Earth at the ground station. Time in seconds since the beginning of the epoch (1 January 1970). The timing can be negative for early in the mission.
    - MH1 - Horizontal Component 1 of the mid-period instrument.
    - MH2 - Horizontal Component 2 of the mid-period instrument.
    - MHZ - Vertical Component of the mid-period instrument.
    - SHZ - Vertical Component of the short-period instrument.
- Minimum occurrences: 0
- Maximum occurrences: 1
- Nillable: No

*location*
Apollo PSE location.
- PDS4 data type: ASCII_Short_String_Collapsed
Valid values: 00, 01
    00 - Peaked response of the mid-period seismometer.
    01 - Flat response of the mid-period seismometer.
Minimum occurrences: 0
Maximum occurrences: 1
Nillable: No

*metadata_file_name*
Apollo PSE observations are stored with the seismic data from the instrument in one file (mini-SEED or GeoCSV format) and the metadata for the measurements in another file (dataless SEED or StationXML format). The metadata_file_name attribute gives the name of the file containing the metadata associated with a given data file.
- PDS4 data type: ASCII_File_Name
- Valid values: N/A
- Minimum occurrences: 1
- Maximum occurrences: 1
- Nillable: No

*product_type*
The product_type identifies a group of data products within a collection that have some property in common, such as processing level, resolution, or instrument-specific setting.
- PDS4 data type: ASCII_Short_String_Collapsed
- Valid values: Dataless-SEED, GeoCSV, Mini-SEED, StationXML
    - Dataless-SEED - Apollo PSE product containing seismic metadata in SEED format.
    - GeoCSV - Apollo PSE product containing seismic data in an ASCII table in GeoCSV format.
    - Mini-SEED - Apollo PSE product containing seismic data in mini-SEED format.
    - StationXML - Apollo PSE product containing seismic metadata in StationXML format.
- Minimum occurrences: 0
- Maximum occurrences: 1
- Nillable: No

*pse_data_type*
Apollo PSE mini-SEED products and their equivalent GeoCSV products contain only seismic data, and therefore have the data_type "waveform". Apollo PSE dataless SEED products and their equivalent StationXML products contain only metadata for the seismic data files, and therefore have the data_type "metadata".
- PDS4 data type: ASCII_Short_String_Collapsed
- Valid values: metadata, waveform
    - metadata - The data product contains only metadata.
    - waveform - The data product contains only seismic data.
- Minimum occurrences: 1
- Maximum occurrences: 1
- Nillable: No

*sample_count*
Sample_count is the number of samples in a Apollo PSE mini-SEED or GeoCSV product.
- PDS4 data type: ASCII_Integer
- Valid values: N/A
- Minimum occurrences: 0
- Maximum occurrences: 1
- Nillable: No

*sampling_rate*
Sampling_rate represents the number of samples per second. The sampling rate is nominal, and there is a small variation between the nominal sampling rate and the actual sampling rate, which can be estimated using the timing trace ATT.
- PDS4 data type: ASCII_Real
- Valid values: N/A
- Minimum occurrences: 0
- Maximum occurrences: 1
- Nillable: No

*seed_file_name*
Apollo PSE data products are archived in their native SEED format and in a PDS-compatible ASCII format. The seed_file_name attribute gives the name of the file that is the SEED equivalent of an ASCII data file.
- PDS4 data type: ASCII_File_Name
- Valid values: N/A
- Minimum occurrences: 1
- Maximum occurrences: 1
- Nillable: No

*station*
Apollo seismic station.
- PDS4 data type: ASCII_Short_String_Collapsed
- Valid values: N/A
- Minimum occurrences: 0
- Maximum occurrences: 1
- Nillable: No

# Examples

Example PDS4 label snippet for data in MiniSEED format:

```
<Mission_Area>
      <apollo:Observation_Information>
        <apollo:product_type>Mini-SEED</apollo:product_type>
      </apollo:Observation_Information>
      <apollo:Seismic_Parameters>
        <apollo:pse_data_type>waveform</apollo:pse_data_type>
        <apollo:Metadata_Location>
          <apollo:metadata_file_name>dataless.xa.0.seed</apollo:metadata_file_name>
          <Internal_Reference>
            <lid_reference>urn:nasa:pds:apollo_pse:data_seed:dataless.xa.0</lid_reference>
            <reference_type>data_to_metadata</reference_type>
          </Internal_Reference>
        </apollo:Metadata_Location>
        <apollo:ASCII_Equivalent>
          <apollo:ascii_equivalent_file_name>xa.s11..att.1969.202.0.a.csv</apollo:ascii_equivalent_file_name>
          <Internal_Reference>
            <lidvid_reference>urn:nasa:pds:apollo_pse:data_table:xa.s11..att.1969.202.0.a::1.0</lidvid_reference>
            <reference_type>seed_to_ascii</reference_type>
          </Internal_Reference>
        </apollo:ASCII_Equivalent>
        <apollo:station>S11</apollo:station>
        <apollo:channel>ATT</apollo:channel>
        <apollo:sampling_rate unit="Hz">1.65625</apollo:sampling_rate>
        <apollo:sample_count>101005</apollo:sample_count>
      </apollo:Seismic_Parameters>
    </Mission_Area>
```

Example PDS4 label snippet for data in GeoCSV format:

```
<Mission_Area>
      <apollo:Observation_Information>
        <apollo:product_type>GeoCSV</apollo:product_type>
      </apollo:Observation_Information>
      <apollo:Seismic_Parameters>
        <apollo:pse_data_type>waveform</apollo:pse_data_type>
        <apollo:Metadata_Location>
          <apollo:metadata_file_name>stationxml.xa.0.sxml</apollo:metadata_file_name>
          <Internal_Reference>
            <lid_reference>urn:nasa:pds:apollo_pse:data_table:stationxml.xa.0</lid_reference>
            <reference_type>data_to_metadata</reference_type>
          </Internal_Reference>
        </apollo:Metadata_Location>
        <apollo:SEED_Equivalent>
          <apollo:seed_file_name>xa.s11..att.1969.202.0.mseed</apollo:seed_file_name>
          <Internal_Reference>
            <lidvid_reference>urn:nasa:pds:apollo_pse:data_seed:xa.s11..att.1969.202.0::1.0</lidvid_reference>
            <reference_type>ascii_to_seed</reference_type>
          </Internal_Reference>
        </apollo:SEED_Equivalent>
        <apollo:station>S11</apollo:station>
        <apollo:channel>ATT</apollo:channel>
        <apollo:sampling_rate unit="Hz">1.65625</apollo:sampling_rate>
        <apollo:sample_count>101005</apollo:sample_count>
      </apollo:Seismic_Parameters>
    </Mission_Area>
```

Example PDS4 label snippet for dataless SEED file:

```
<Mission_Area>
      <apollo:Observation_Information>
        <apollo:product_type>Dataless-SEED</apollo:product_type>
      </apollo:Observation_Information>
      <apollo:Seismic_Parameters>
        <apollo:pse_data_type>metadata</apollo:pse_data_type>
        <apollo:ASCII_Equivalent>
          <apollo:ascii_equivalent_file_name>stationxml.xa.0.sxml</apollo:ascii_equivalent_file_name>
          <Internal_Reference>
            <lidvid_reference>urn:nasa:pds:apollo_pse:data_table:stationxml.xa.0::1.0</lidvid_reference>
            <reference_type>seed_to_ascii</reference_type>
          </Internal_Reference>
        </apollo:ASCII_Equivalent>
      </apollo:Seismic_Parameters>
    </Mission_Area>
```

Example PDS4 label snippet for metadata in StationXML format:

```
<Mission_Area>
      <apollo:Observation_Information>
        <apollo:product_type>StationXML</apollo:product_type>
      </apollo:Observation_Information>
      <apollo:Seismic_Parameters>
        <apollo:pse_data_type>metadata</apollo:pse_data_type>
        <apollo:SEED_Equivalent>
          <apollo:seed_file_name>dataless.xa.0.seed</apollo:seed_file_name>
          <Internal_Reference>
            <lidvid_reference>urn:nasa:pds:apollo_pse:data_seed:dataless.xa.0::1.0</lidvid_reference>
            <reference_type>ascii_to_seed</reference_type>
          </Internal_Reference>
        </apollo:SEED_Equivalent>
      </apollo:Seismic_Parameters>
    </Mission_Area>
```
