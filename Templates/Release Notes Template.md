---
uid: releaseNotes
---

# Release Notes

*Product Version x.x*<br>
© 2020 OSIsoft, LLC. All rights reserved. <!--*This section may be removed if this note is part of a broader manual.*-->

## Overview

<!--Insert brief description of your product here.  If these release notes cover service packs or patches in addition to the major release numbers, briefly identify each version covered.-->

## Fixes and Enhancements

<!--*This section may be removed if this is the first release of a product.  If multiple releases are covered by this note, for example, if service packs and patches are added, these can either sectioned by release, or, if lengthy, can have sub-pages per release.* -->

### Fixes

This section lists items that were resolved in release *{ x.x.x.xxxx }* - *{ mm/dd/yyyy }*.
Item | Description
---- | -----------
*{work item #}* | *{ work item release note }*

### Enhancements

This section lists features that were added in release *{ x.x.x.xxxx }* - *{ mm/dd/yyyy }*.

<!--*Using bullet style:*-->
* *{ new feature }*
* *{ new feature }*

<!--OR

*Using  table style:*-->
Item | Description
---- | -----------
*{Work item #}* | *{ feature description }*

## Known Issues

This section lists problems and enhancements that have been deferred until a future release.
<!--*Use bullets and tables as necessary (table format below).* -->
Item | Description
---- | -----------
*{ item #}* | *{ problem/enhancement description }*

## Setup

<!--*This section may be removed if the setup instructions are captured within a separate topic in the same manual.*-->

### Operating Systems

<!--*Insert text here.*-->  For example: This release supports Windows Server 2019, Windows Server 2016, and Windows 10 (32 and 64 bit).

### Server Platforms

<!--*Insert text here.*-->

### Distribution Kit Files

<!--*Insert text here. Please list the files, redistributables, additional .EXEs or MSI’s that are including in the setup kit if appropriate.*-->

### Installation and Upgrade

<!--*Provide clear installation and upgrade instructions.  Include guidance on specific steps needed to confirm that an upgrade scenario was successful.  If additional guidance is required for repairing the product once its installed please include guidance in this section.*-->

### Uninstalling Product

<!--*Insert text here.*-->

## Security Information and Guidance

### OSIsoft’s Commitment

Because the PI System often serves as a barrier protecting control system networks and mission-critical infrastructure assets, OSIsoft is committed to (1) delivering a high-quality product and (2) communicating clearly what security issues have been addressed. This release of *{ product name }* is the highest quality and most secure version of the *{ product name }* released to date. OSIsoft's commitment to improving the PI System is ongoing, and each future version should raise the quality and security bar even further.

### Vulnerability Communication

The practice of publicly disclosing internally discovered vulnerabilities is consistent with the Common Industrial Control System Vulnerability Disclosure Framework developed by the Industrial Control Systems Joint Working Group (ICSJWG). Despite the increased risk posed by greater transparency, OSIsoft is sharing this information to help you make an informed decision about when to upgrade to ensure your PI System has the best available protection.

For more information, refer to [OSIsoft’s Ethical Disclosure policy (https://www.osisoft.com/ethical-disclosure-policy)](https://www.osisoft.com/ethical-disclosure-policy).

To report a security vulnerability, refer to [OSIsoft's Report a Security Vulnerability (https://www.osisoft.com/report-a-security-vulnerability)](https://www.osisoft.com/report-a-security-vulnerability).

### Vulnerability Scoring

OSIsoft has selected the Common Vulnerability Scoring System (CVSS) to quantify the severity of security vulnerabilities for disclosure. To calculate the CVSS scores, OSIsoft uses the National Vulnerability Database (NVD) calculator maintained by the National Institute of Standards and Technology (NIST).  OSIsoft uses High, Medium and Low categories to aggregate the CVSS Base scores. This removes some of the opinion related errors of CVSS scoring.  As noted in the CVSS specification, Base score range from 0 for the lowest severity to 10 for the highest severity.

### Overview of New Vulnerabilities Found or Fixed

This section is intended to provide relevant security-related information to guide your installation or upgrade decision. OSIsoft is proactively disclosing aggregate information about the number and severity of *{ product name }* security vulnerabilities that are fixed in this release.

<!--*Provide an overview of the types of Security Vulnerabilities fixed in this release*-->

<!--*NOTE:  If NO security vulnerabilities are identified in the current release, please use the following statement:*-->

No security-related information is applicable to this release

<!--*When vulnerabilities exist Product teams should decide which format works best specific to the release and/or is applicable.  Two different samples are provided below.*-->

**Sample A** - For this release of the *{ product name }*, *{ x number }* of security vulnerability has been identified and fixed.

Based on the CVSS scoring system this issue has been categorized as a High (7.0 – 8.9). This high-level security issue is network accessible and has been resolved in the *{ product release name }*. To reduce exposure to this security issue, either limit access to the port used by the PI SQL products, or upgrade to the latest release.  

**Sample A with OSIsoft sub-component** - Based on the CVSS scoring system this issue has been categorized as a High (7.0 – 8.9). This high-level security issue has been resolved in *{ OSIsoft’s PI SDK version 1.1 sub-component }* which has been packaged in this *{ PI ProcessBook 1998 release }*. To reduce exposure to this security issue upgrade to the latest release.

**Sample A with 3rd Party sub-component** - Based on the CVSS scoring system this issue has been categorized as a High (7.0 – 8.9). This high-level security issue has been resolved in the 3rd Party *{ OpenSSL sub-component }* which has been packaged in this *{ PI ProcessBook 1998 release }*. To reduce exposure to this security issue upgrade to the latest release.

**Sample B** - For this release of the *{ product name }*, *{x number}* of security vulnerability has been identified and fixed. The table below provides an overview of the types and severity of the security fixes.

Security Vulnerabilities fixed in this release  
Severity Category| CVSS Base Score Range  | Number of Fixed Vulnerabilities
---- | ------ | -----------
Critical | 9.0-10 | *{ quantity }*
High | 7.0-8.9 | *{ quantity }*
Medium | 4.0-6.9 | *{ quantity }*
Low | 0-3.9 | *{ quantity }*

**Sample B with sub-components** - For this release of the *{product name}*, *{x number}* of security vulnerability has been identified and fixed. The tables below provide an overview of the types and severity of the security fixes. {*Some/All*} of the vulnerabilities were associated with *{OSIsoft/3rd Party}* sub-component {*name*} which is packaged in this release.

Summary of Security Vulnerabilities fixed in this release

Severity Category| CVSS Base Score Range  | Number of Fixed Vulnerabilities
---- | ------ | -----------
Critical | 9.0-10 | *{ quantity }*
High | 7.0-8.9 | *{ quantity }*
Medium | 4.0-6.9 | *{ quantity }*
Low | 0-3.9 | *{ quantity }*

Security Vulnerabilities fixed in the *{ OSIsoft/3rd Party sub-component name}*
Severity Category| CVSS Base Score Range  | Number of Fixed Vulnerabilities
---- | ------ | -----------
Critical | 9.0-10 | *{ quantity }*
High | 7.0-8.9 | *{ quantity }*
Medium | 4.0-6.9 | *{ quantity }*
Low | 0-3.9 | *{ quantity }*

<!--*Optional “Microsoft Software Security Defenses topic below” (applies to C++ projects)*-->

### Microsoft Software Security Defenses

In addition to finding and fixing security bugs within the *{ product name }* , it is equally critical that OSIsoft leverage security defenses provided by the Microsoft Visual C++ compiler that builds it and the Microsoft Windows operating system that runs it. Over the past decade, Microsoft has continually added new defenses and improved existing defenses with successive versions of the compiler and the operating system.  To learn more about many of these key defenses, consult the Microsoft whitepaper Mitigating Software Vulnerabilities.

## Documentation Overview

<!--*This section may be removed if the information is  captured within a separate topic in the same manual.*-->

Example:

**PI Notifications User Guide:** An introduction to PI Notifications for the end user. This user guide provides a product overview, installation procedures, a tutorial to acquaint you with the user interface for PI Notifications, and other topics to allow you to work with and troubleshoot PI Notifications.

**PI System Explorer User Guide:** Provides an overview and explains the functions of the PI System Explorer interface.  

## Technical Support and Resources

<!--*This section may be removed if the information is  captured within a separate topic in the same manual.*-->

For technical assistance, contact OSIsoft Technical Support at +1 510-297-5828 or log a case through the OSIsoft Customer Portal. Additionally, the Contact Us page on the portal offers contact options for customers outside of the United States.

When you contact OSIsoft Technical Support, be prepared to provide this information:

* Product name, version, and build numbers
* Computer platform (CPU type, operating system, and version number)
* Time that the difficulty started
* Log files at that time
* Details of any environment changes prior to the start of the issue
* Summary of the issue, including any relevant log files during the time the issue occurred

The PI Square community has resources to help you with your technical questions.  PI Developers Club program offers specific services to developers and system integrators.

_____________________________________________________________

<!--*This section may be removed if the release note is included as a topic in a broader manual.*-->

OSIsoft, LLC  
1600 Alvarado Street  
San Leandro, CA 94577 USA  
Tel: (01) 510-297-5800  
Fax: (01) 510-357-8136  
Web: <http://www.osisoft.com>  

No part of this publication may be reproduced, stored in a retrieval system, or transmitted, in any form or
by any means, mechanical, photocopying, recording, or otherwise, without the prior written permission
of OSIsoft, LLC.

OSIsoft, the OSIsoft logo and logotype, Managed PI, OSIsoft Advanced Services, OSIsoft Cloud Services, OSIsoft Connected Services, PI ACE, PI Advanced Computing Engine, PI AF SDK, PI API, PI Asset Framework, PI Audit Viewer, PI Builder, PI Cloud Connect, PI Connectors, PI Data Archive, PI DataLink, PI DataLink Server, PI Developers Club, PI Integrator for Business Analytics, PI Interfaces, PI JDBC Driver, PI Manual Logger, PI Notifications, PI ODBC Driver, PI OLEDB Enterprise, PI OLEDB Provider, PI OPC DA Server, PI OPC HDA Server, PI ProcessBook, PI SDK, PI Server, PI Square, PI System, PI System Access, PI Vision, PI Visualization Suite, PI Web API, PI WebParts, PI Web Services, RLINK and RtReports are all trademarks of OSIsoft, LLC.
All other trademarks or trade names used herein are the property of their respective owners.  

U.S. GOVERNMENT RIGHTS  
Use, duplication or disclosure by the US Government is subject to restrictions set forth in the OSIsoft, LLC license agreement and as provided in DFARS 227.7202, DFARS 252.227-7013, FAR 12-212, FAR 52.227-19, or their successors, as applicable.

Version: *{ version }*  
Published: *{ date published }*
