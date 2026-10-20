# Crime Management and Evidence Organization System
## SLA Stage 3 Prototype Report

**Course:** Data Structures · Computer Engineering, SY CM2  
**Project team:** Aditya Mohite (125BTCM1207) · Nitin Misal (125BTCM1119)  
**Prototype:** Browser-based case management website  
**Date:** 21 October 2026

## 1. Introduction

The first two Structured Lab Activities built a C program for recording and managing crime case details. SLA-1 introduced adding and displaying case records. SLA-2 added searching and deleting records by Case ID. The reports also identified record updates and saving data between runs as useful next steps.

For SLA Stage 3, the project is presented as a clickable website prototype. It gives the existing case-record operations a visual interface and adds an update workflow. The prototype uses fictional case examples and saves changes in the current browser so a user can demonstrate the main interactions without installing a server or database.

## 2. Aim and Objectives

The aim is to make the crime case and evidence record workflow easier to understand and demonstrate through a browser interface.

The prototype is designed to:

1. Show case records with their Case ID, crime type, location, report date, officer and evidence description.
2. Let a user add a record while preventing duplicate Case IDs.
3. Find cases by ID or other visible record details and filter by crime type.
4. Allow existing case details to be updated.
5. Ask for confirmation before deleting a case.
6. Retain demo changes in browser storage between page reloads.

## 3. Scope of the Prototype

The prototype is a single-page front-end demonstration. Its sample records are fictional. It does not connect to a police database, use a server, manage accounts, upload evidence files, or synchronize information between devices. The evidence field is a text description, matching the fields used by the earlier C program.

## 4. Website Features

| Feature | What the user can do |
| --- | --- |
| Case overview | See total cases, crime categories, evidence notes and assigned officers. |
| Case register | Browse the current records, including the report date and officer in charge. |
| Search and filter | Search by Case ID, crime, location, officer or evidence text; narrow the list by crime type. |
| Add a case | Enter the record fields and receive a clear duplicate-ID warning if the ID is already in use. |
| Update a case | Edit a selected record while keeping its Case ID fixed. |
| Delete a case | Review the selected record and confirm before removing it. |
| Recent activity | See a short list of recent additions, edits and deletions during the current session. |
| Browser storage | Keep records on the same browser using local storage. |

## 5. Case Record Fields

The website carries forward the record details used in SLA-1 and SLA-2:

| Field | Purpose |
| --- | --- |
| Case ID | Unique positive identifier for a report. |
| Crime type | Category such as theft, vandalism, assault or burglary. |
| Location | Reported place of the incident. |
| Date reported | Date the report was entered. |
| Evidence description | Text summary of evidence associated with the case. |
| Officer in charge | Officer assigned to the case. |
| Status | Prototype label used to distinguish investigation and evidence review. |

## 6. Data Structure and Operations

The prototype's internal record handling follows the singly linked list introduced in the earlier C implementation. Each JavaScript `CaseNode` holds one case record and a `next` reference. A `head` reference identifies the first record. The browser interface displays records in a table, while its script performs operations on the linked records.

- **Add:** checks that the Case ID is unused, then appends the new record.
- **Display:** walks through the records and builds the table and summary.
- **Search:** checks records sequentially until a matching ID or text value is found.
- **Update:** finds a record and changes its editable fields.
- **Delete:** finds the selected record, asks for confirmation, then reconnects the surrounding references. Deleting the first record moves the start reference to the next record.
- **Persistence:** converts the records to JSON for browser storage and reconstructs them when the page opens again.

The site includes user-facing search and category filters, but it does not claim that browser storage is a secure or shared case-management database.

## 7. Demonstration Walkthrough

The following sequence demonstrates the main prototype workflow:

1. Open the case overview and review the fictional sample reports.
2. Search for Case ID 101 or filter the table by a crime type.
3. Open a case for editing and change a detail such as the location or evidence description.
4. Add a new report with a unique positive Case ID and complete the required fields.
5. Try reusing an existing Case ID to see the duplicate warning.
6. Start deleting a case, review the confirmation details, and either cancel or confirm.
7. Reload the page to see that demo records remain in the same browser.

## 8. Validation and User Feedback

The interface requires the Case ID and descriptive fields before a record can be submitted. Case IDs must be positive numbers and unique within the current records. The search field gives an empty-state message when there are no matches. Deletion requires a second confirmation action. Add, update and delete operations produce a visible confirmation message and appear in recent activity.

These are prototype-level interface safeguards. They do not replace server-side validation, access controls or an audit system.

## 9. Limitations and Future Improvements

The current version stores records only in one browser profile. Clearing that browser's site data can remove the demo records. There is no authentication, shared database, role separation, backup, encrypted evidence storage, file attachment handling or production audit trail. The sample content should not be replaced with real case information.

Possible future improvements include:

- Connect the interface to a backend database with authenticated users.
- Add record status, priority and date-range filters.
- Support evidence attachments with controlled access and a clear chain-of-custody log.
- Add input validation for date formats and required field lengths.
- Record who changed a case and when, and provide a recoverable archive instead of permanent deletion.

## 10. Conclusion

The Stage 3 prototype turns the earlier console-based case functions into a visual, interactive case register. It carries forward the original record fields and add, display, search and delete operations, and demonstrates the planned update feature. Browser storage makes the demonstration convenient, while the stated limitations distinguish this classroom prototype from a secure operational system.

## References

1. *Crime Management and Evidence Organization System — SLA-1 Review*, submitted 16 August 2026.
2. *Crime Management and Evidence Organization System — SLA-2 Review*, submitted 23 August 2026.
3. `index.html` in this Stage 3 prototype package.

