# Automated Shared Drive Backup & Activity Monitor  
Google Workspace Automation (Apps Script)

## Overview
The **Automated Shared Drive Backup & Activity Monitor** is a lightweight solution built on **Google Workspace** using **Apps Script**.  
It automatically backs up selected Shared Drives or folders into a designated Backup Shared Drive, logs changes, and sends scheduled activity reports to administrators.

This solution is ideal for small and medium-sized businesses that need simple Drive protection and compliance visibility without deploying servers or external infrastructure.

---

## Key Features
- 🔄 **Automatic Shared Drive or Folder Backups**  
  Copies only new or updated files into a designated backup drive.

- 📁 **Incremental Backup Logic**  
  No duplicate uploads; only changed files are stored.

- 📝 **Activity Monitoring & Logging**  
  Tracks:
  - file additions  
  - deletions  
  - renames  
  - permission changes  

- 📧 **Daily/Weekly Email Reports**  
  Summary of backup activity + file changes.

- 🗂 **Simple Google Sheet Configuration**  
  - Source drive/folder IDs  
  - Backup destination ID  
  - Reporting options  
  - Enable/disable features  
   
- ⏱ **Runs Automatically Using Apps Script Triggers**  
  Zero maintenance needed.

---

## Architecture
Below is the high-level architecture of the solution:

```
            +------------------+
            |      Users       |
            +--------+---------+
                     |
                     v
    +----------------+----------------+
    |            Google Shared Drives |
    +----------------+----------------+
                     |
                     v
    +---------------------------------------------+
    |           Apps Script (Backup Engine)        |
    |---------------------------------------------|
    |  • Reads configuration from Google Sheets    |
    |  • Performs incremental backup               |
    |  • Logs events and file changes              |
    |  • Sends email reports via Gmail API         |
    +----------------+-----------------------------+
                     |
                     v
          +----------+-----------+
          | Backup Shared Drive  |
          |     (Destination)    |
          +-----------------------+
```

---

## Installation

### 1. Copy the Apps Script Project
1. Open **Google Apps Script**  
2. Create a **new script project**  
3. Paste the code from `/apps-script/main.gs`  
4. Save

---

### 2. Prepare Configuration Sheet
Create a Google Sheet with the following columns:

| Setting | Value | Description |
|--------|--------|-------------|
| source_ids | driveID1, driveID2 | Shared Drive or folder IDs to back up |
| backup_destination_id | driveID | Backup Shared Drive |
| report_frequency | daily/weekly | Email reporting frequency |
| report_email | user@example.com | Recipient |
| enable_activity_monitor | true/false | Toggle file event logging |

Update your Apps Script project to reference the sheet ID.

---

### 3. Set Triggers
In Apps Script:
1. Click **Triggers**
2. Add new trigger:
   - Function: `runBackup`
   - Event type: **Time-driven**
   - Frequency: Hourly / Daily / Weekly

---

## How It Works
1. Script reads configuration from Google Sheets.  
2. Retrieves files from the source Shared Drives or folders.  
3. Compares with previously logged files to identify new/changed ones.  
4. Copies changed files to the backup destination.  
5. Logs all activity into a secondary log sheet.  
6. If reporting enabled → sends summary email.

---

## Use Cases
- Backup Shared Drives for small businesses  
- Compliance event tracking  
- Insider changes visibility  
- Simple disaster recovery  
- Cross-team file mirroring  

---

## Security
- Runs fully inside user’s Google Workspace environment  
- No external servers or storage  
- Uses least-privilege OAuth scopes  
- Admin can review and approve permissions  

---

## Files in This Repository

```
/apps-script/main.gs → Core backup script
/apps-script/helpers.gs → Logging + utilities
/config/config-example.xlsx → Example configuration structure
/docs/architecture.png → Architecture diagram
/docs/how-it-works.md → Detailed flow explanation
README.md → This documentation
```

---

## Contact
This solution is maintained by **Bernier Tech ltd**.  
For assistance or customization requests, open an issue in this repository.
