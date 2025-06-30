# Setup for Cognex DM8700 in WCS

## Table of Contents
1.  Purpose
2.  Scope / Activities Affected
3.  References
4.  Definitions and Acronyms
5.  Exclusions / Compatibility
6.  Procedure / Instructions
7.  Compliance / Approvals
8.  Common / Known Issues
9.  Solutions / Recommendations
10. General
11. Revision / Approval History
12. Record Keeping

---

## 1. Purpose

This document provides a guide on how to configure a Cognex scanner in the Workstation Control System (WCS). The document outlines the standard work process to set up the scanner as if it was brand new or factory default.

## 2. Scope / Activities Affected

These instructions apply to everyone who needs to use a scanner in WCS, including but not limited to the WCS development team, the implementation team, and process engineers.

## 3. References

### Related Documents

| Number and Hyperlink                                            | Title/Description                                       |
| :-------------------------------------------------------------- | :------------------------------------------------------ |
| [https://support.cognex.com/en/downloads/dataman/software-firmware](https://support.cognex.com/en/downloads/dataman/software-firmware) | Support - DataMan Software & Firmware \| Cognex         |
| [https://support.cognex.com/docs/dmst_6112/web/EN/DMCC/Content/Topics/dmcc-main.html?tocpath=_____1](https://support.cognex.com/docs/dmst_6112/web/EN/DMCC/Content/Topics/dmcc-main.html?tocpath=_____1) | DMCC Reference - DataMan Control Commands Overview - Documentation \| Cognex |
| [https://support.cognex.com/docs/dmst_631/EN/CommunicationsAndProgramming.pdf](https://support.cognex.com/docs/dmst_631/EN/CommunicationsAndProgramming.pdf) | Cognex Communications and Programming Guide             |
| [https://support.cognex.com/en/documentation/dataman/dm-8700](https://support.cognex.com/en/documentation/dataman/dm-8700) | DataMan 8700 – Documentation \| Cognex                  |

### Additional Resources

| Number and Hyperlink | Title/Description |
| :------------------- | :---------------- |
| TBA                  | Block Point       |

## 4. Definitions and Acronyms

*   **WCS**: Workstation Control System
*   **IP**: Internet Protocol
*   **PoE**: Power over Ethernet
*   **DM**: DataMan
*   **TCP**: Transmission Control Protocol

## 5. Exclusions / Compatibility

Cognex DM8700 uses the base/cradle firmware `xx` and the handheld firmware `xx`.

The scanner driver that allows system connectivity with WCS is compatible with all WCS versions prior to Version 3.7.0 – Alpha.

For more information on the compatibility, refer to the block point.

### Precautions

It is important to understand the compatibility to your plant area / line along with the list of the approved compatible workstation, firmware, and schema versions.

### Requirements / Prerequisites

*   Users must have administrative rights on their computer to be able to download the required software.
*   User must have a Cognex DM8700 at hand with a PoE (provided by Cognex).

## 6. Procedure / Instructions

1.  Download and Install the DataMan Setup Tool software by clicking the following link: [https://support.cognex.com/en/downloads/dataman/software-firmware](https://support.cognex.com/en/downloads/dataman/software-firmware)
    *   Ensure that you are downloading the `.exe` file for the DM8700 or the desired model.
2.  After installation, open the DataMan Setup Tool. To connect the hardware via a Power over Ethernet (PoE) injector using the Cognex-recommended sequence, complete the following steps. Be sure to refer to the diagram in 8.2.4 for guidance.
    *   Connect the PoE injector to the Ethernet network (both ends of the patch cable).
    *   Connect the power cord (AC 230V/110V) to the PoE injector.
    *   Connect the reader to the PoE injector.
    *   For more info about connecting the hardware, visit the Networking section on the DataMan Communications and Programming Guide at the following link: [https://support.cognex.com/docs/dmst_631/EN/CommunicationsAndProgramming.pdf](https://support.cognex.com/docs/dmst_631/EN/CommunicationsAndProgramming.pdf)
3.  After connecting the hardware, follow these steps to verify its proper connection.
    1.  Open Settings/Network and Internet and under Advance network settings, click on Change Adapter Options.
    2.  Right-Click on Ethernet and choose Properties.
    3.  Double-Click on Internet Protocol Version 4 (TCP/IPv4).
    4.  Ensure IP address is set to `192.168.0.XX` (Choose a for Host ID XX choose a non-existing number in your network).
    5.  Ensure Subnet Mask is set to `255.255.0.0`.
    6.  Save changes by clicking ok on both windows opened.
    7.  Open Command Prompt and ping to the Scanner by typing the following: `Ping 192.168.0.60` (Or the IP address of the scanner if it has been changed).
    8.  Result should look like the image below.
        (Image Placeholder for Ping Result)
        A successful ping to the hardware's IP address confirms it is properly connected to the network.
4.  Go back to the DataMan Setup Tool and look for the hardware that has just been connected.
5.  Click the Connect tab then refresh to select `DM8700Base-87ADBE`.
6.  Open the Communication step and select Ethernet to verify IP Address, Subnet Mask, and Telnet Port.
7.  After the connection has been verified, enable Telnet Client on Windows and connect to the scanner.
    1.  Search on start menu and open: `Turn Windows features on or off`.
    2.  Scroll down and check the box for the Telnet Client to enable it.
        (Image Placeholder for Telnet Client Checkbox)
    3.  Search on start menu and open: `Telnet`.
    4.  To connect to the scanner, type `o + IP address + telnet port` (example: `o 192.168.0.60 23`) under Telnet type.
    5.  Once the connection is successful through either the Telnet Client or Ubuntu software, perform the following commands:
        *   To get the name of the device, type the following: `||>get device.name`
        *   To get the serial number of the device, type the following: `||>get device.serial-number`

## 7. Compliance / Approvals

[Compliance requirement(s) / Approval(s) after completing]

## 8. Common / Known Issues

In some case using the connection through Telnet Client is not successful. Refer to 11.1 for the solution.

## 9. Solutions / Recommendations

1.  If a connection through Telnet is not successful, use the Ubuntu software to connect instead.
    1.  Search on start menu and open: `Ubuntu`.
    2.  If not installed use the Quick Guide to Install Ubuntu 20.04 LTS to install it.
    3.  Open Ubuntu and install the telnet server by typing the following command: `sudo apt install telnet -y`
    4.  Once the installation is complete, connect to telnet port by typing: `telnet + IP Address + telnet port` (example: `telnet 192.168.0.60 23`)
    5.  Then use the same commands in 8.5.1 and 8.5.2 to get the name and serial number of the device.

## 10. General

*   Updates, changes, revisions to this document shall be completed by the Automation and Controls Engineering (ACE) team.
*   Submit change request to the Automation and Controls Engineering (ACE) team.
    *   [email: acecoreengineeringgroup@groups.ford.com](mailto:acecoreengineeringgroup@groups.ford.com).

## 11. Revision / Approval History

| Rev. # | Description of Changes | Pages Affected | Author | Approval | Date       |
| :----- | :--------------------- | :------------- | :----- | :------- | :--------- |
| v1.00  | Update                 |                |        |          | 2/26/2025  |
| 1.00   | Initial Release        |                |        |          | 2/26/2025  |

## 12. Record Keeping

1.  [Instructions for maintaining records]
2.  Edit, update, save, maintain master file with Word.
    *   **Notice**: The blue items in the document header, footer, and revision chart are document / file properties and these can be seen within file manager by right clicking file > Properties > Details; and within document by clicking on top banner File > Info.
3.  Save Word file on Sharepoint (Example: External SharePoint).
    *   MLP Documents
4.  Convert word document to HMTL (Web site converter).
    1.  Open web browser link.
    2.  DOCX (WORD) to HTML (Online & Free)
    3.  **NOTE**: File must be closed before proceeding to next step.
5.  Drag and drop your word document file on website RED Choose Files area or click area and browse for file.
6.  Click website RED Convert > area.
7.  After converting within website select BLUE Download button.
8.  Open Downloads or default download location in file explorer.
9.  Move new HMTL to Git document’s location and documents Sharepoint.

