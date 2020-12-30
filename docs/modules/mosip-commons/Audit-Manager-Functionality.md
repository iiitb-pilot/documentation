# Audit Manager
The Audit Manager in MOSIP captures all the information pertaining to the actions performed by various MOSIP applications. This information can further be used for data analysis which will help in inspecting, cleansing, transforming and modeling data to discovering useful information, informing conclusions and decision-making.

## Audit Log Parameters
The following parameters are captured as a part of audit service, 

Parameters | Description | Example
-----------|-------------|----------
**Event ID** | The ID of the Event that triggered for which the audit action has happened | 
**Event Type** | Type of event that triggered the audit log | System, User  
**Event Name** | Name of the event | Create, Register, Update, Processing
**Log Description** | Detailed description of the audit event captured | 
**Module ID** | Application Module ID that triggered for which the audit action has happened | 
**Module Name** | Name of the application module | Packet Service, Resident Service and MISP Management Service)
**Ref ID** | Reference ID for any cross reference purpose relevant for audit tracking | userid, rid, prid, app id, app or module id etc.
**Ref ID Type** | Type of reference id entered |
**Application ID** | Application Id of audit action happened and logged | 
**Application Name** | Name of the application | Admin, Resident Services, Partner Management etc.

## Application Specific Audit Details

* [Admin Service Audits](Admin-Service-Audits.md)
* [Resident Service Audits](Resident-Service-Audits.md)
* [Partner Management Audits](Partner-Management-Audits.md)
* Registration Client Audits - TBD
* Registration Processor Audits - TBD
* ID Repository Audits - TBD
* ID Authentication Audits - TBD
* Pre-registration Audits - TBD
* Admin Portal Audits - TBD

## Abbreviations
Abbreviation | Definition
-------------|-------------
ADM | Admin
PKT	| Packet
BLK	| Bulk
RID	| Registration ID
RES	| Resident
MISP | MOSIP Infrastructure Service Provider
PMS | Partner Management System
UIN	| Unique Identification Number
VID	| Virtual ID