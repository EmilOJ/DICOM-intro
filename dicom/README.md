## Introduction
The [DICOM](http://dicom.nema.org/standard.html) standard consists of two parts:
  1. **DICOM File Format**: The format that medical images are saved in -> DICOM files.
  2. **DICOM Network Protocol**:  Network protocol that applications connected to a hospital's network use to communicate. Not only used for image exchange but also patient and procedure information.

Before the DICOM standard was created medical applications had no standardised way of communicating with each other out of the box. When applications from different vendors had to be integrated it was a huge task.

PACS (Picture Archiving and Communication Systems) are complete medical systems that encompass
- Modalities (e.g.CT scanners)
- Digital image archives (image database)
- Workstations (where radiologist examine the images)

The functionality of PACS is DICOM-driven, meaning that they implement some parts of the DICOM standard necessary for their function. Any PACS device comes with a so-called *DICOM Conformance Statement* specifying what parts of the DICOM standard it supports.

The DICOM standard document consists of 16 volumes (*parts*) numbered PS3.1 through PS3.18 (parts 3 and 13 are retired).

## DICOM Information Model
The DICOM Information Model describes how DICOM views the real world. The real world in this context consists of patients, studies, medical devices etc. and each is in DICOM viewed as an *object* with a number of attributes describing it (think object oriented programming). These are standardized according to **DICOM Information Object Definitions (IODs)**: A patient IOD will always contain attributes such as patient name, ID, sex, age etc.
There are more than 2000 standard attributes defined in the *DICOM Data Dictionary*. The DICOM standard defines its own data types (called *Value Representations*) such as date, time, unsigned short etc.

When one DICOM device, known as an *Application Entity* (AE), communicates with another it is said to provide or request a *service* to/from that device. Say a CT-scanner needs to send an image (an IOD/object) to a image archive for storage. It requests a storage service from the image archive and provides an image object together with the service request.
More often than not a service includes some kind of data transfer. In the example above the request from the CT-scanner contains both a storage service request and an image object. Since this will always be the case for storage service requests it makes sense to always associate a storage request with an image object. This type of association is called a *Service-Object Pair* (SOP). There are many types of SOPs defined in the DICOM standard and they are grouped into *SOP Classes*.

![](/img/SCU_SCP_relationship.png)
*Shows the SCU/SCP relationship between a CT-scanner and an image archive.*

## DICOM Elements
DICOM elements are the basic building blocks of DICOM objects (DICOM files). If one wanted to DICOMize a simple JPEG image, the pixel data will be only one DICOM element out of many in the resulting DICOM object. Apart from the pixel data element, most DICOM elements can be seen as metadata about the image. An example of a DICOM element is shown here:

`(0028,0010) US 96 # 2, 1 Rows`

- `(0028,0010)` is called the **tag** and is the unique identifier for this particular element. The first number `0028` is the element group (all elements concerned with the image itself - as opposed to information about the scanner, study, patient etc. - are in group `0028`). `0010` is the element id within the group.
- `US` is called the **VR code** (Value Representation) and is the data type of the element. This field is omitted in some implementations. Possible datatypes include:
    - `US`: Unsigned short
    - `CS`: Coded string
    - `OB`: Other byte (i.e. byte stream)
- `96` is the value of the element. In this case the height of the image is 96 pixel rows.
- `#` starts a comment
- `2` is the length of the element value (always even number). If the value is a single character (`F` for female) the value is padded with a space (ASCII `0x20`).
- `1` value multiplicity (explained later)

