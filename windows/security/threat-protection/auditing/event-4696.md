---
title: 4696(S) A primary token was assigned to process. (Windows 10)
description: Describes security event 4696(S) A primary token was assigned to process.
ms.pagetype: security
ms.prod: m365-security
ms.mktglfcycl: deploy
ms.sitesec: library
ms.localizationpriority: none
author: dansimp
ms.date: 09/07/2021
ms.reviewer: 
manager: dansimp
ms.author: dansimp
ms.technology: windows-sec
---

# 4696(S): A primary token was assigned to process.


<img src="images/event-4696.png" alt="Event 4696 illustration" width="442" height="454" hspace="10" align="left" />

***Subcategory:***&nbsp;[Audit Process Creation](audit-process-creation.md)

***Event Description:***

This event generates every time a process runs using the non-current access token, for example, UAC elevated token, RUN AS different user actions, scheduled task with defined user, services, and so on.

***IMPORTANT*:** this event is deprecated starting from Windows 7 and Windows 2008 R2.

> **Note**&nbsp;&nbsp;For recommendations, see [Security Monitoring Recommendations](#security-monitoring-recommendations) for this event.

<br clear="all">

***Event XML:***
```
- <Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
- <System>
 <Provider Name="Microsoft-Windows-Security-Auditing" Guid="{54849625-5478-4994-a5ba-3e3b0328c30d}" /> 
 <EventID>4696</EventID> 
 <Version>0</Version> 
 <Level>0</Level> 
 <Task>13312</Task> 
 <Opcode>0</Opcode> 
 <Keywords>0x8020000000000000</Keywords> 
 <TimeCreated SystemTime="2015-08-25T21:33:42.401Z" /> 
 <EventRecordID>561</EventRecordID> 
 <Correlation /> 
 <Execution ProcessID="4" ThreadID="88" /> 
 <Channel>Security</Channel> 
 <Computer>Win2008.contoso.local</Computer> 
 <Security /> 
 </System>
- <EventData>
 <Data Name="SubjectUserSid">S-1-5-18</Data> 
 <Data Name="SubjectUserName">WIN2008$</Data> 
 <Data Name="SubjectDomainName">CONTOSO</Data> 
 <Data Name="SubjectLogonId">0x3e7</Data> 
 <Data Name="TargetUserSid">S-1-5-18</Data> 
 <Data Name="TargetUserName">dadmin</Data> 
 <Data Name="TargetDomainName">CONTOSO</Data> 
 <Data Name="TargetLogonId">0x1c8c5</Data> 
 <Data Name="TargetProcessId">0xf40</Data> 
 <Data Name="TargetProcessName">C:\\Windows\\System32\\WerFault.exe</Data> 
 <Data Name="ProcessId">0x698</Data> 
 <Data Name="ProcessName">C:\\Windows\\System32\\svchost.exe</Data> 
 </EventData>
 </Event>

```

***Required Server Roles:*** this event is deprecated starting from Windows 7 and Windows 2008 R2.

***Minimum OS Version:*** Windows Server 2008, Windows Vista.

***Event Versions:*** 0.

***Field Descriptions:***

**Subject:**

-   **Security ID** \[Type = SID\]**:** SID of account that requested the “assign token to process” operation. Event Viewer automatically tries to resolve SIDs and show the account name. If the SID cannot be resolved, you will see the source data in the event.

> **Note**&nbsp;&nbsp;A **security identifier (SID)** is a unique value of variable length used to identify a trustee (security principal). Each account has a unique SID that is issued by an authority, such as an Active Directory domain controller, and stored in a security database. Each time a user logs on, the system retrieves the SID for that user from the database and places it in the access token for that user. The system uses the SID in the access token to identify the user in all subsequent interactions with Windows security. When a SID has been used as the unique identifier for a user or group, it cannot ever be used again to identify another user or group. For more information about SIDs, see [Security identifiers](/windows/access-protection/access-control/security-identifiers).

-   **Account Name** \[Type = UnicodeString\]**:** the name of the account that requested the “assign token to process” operation.

-   **Account Domain** \[Type = UnicodeString\]**:** subject’s domain or computer name. Formats vary, and include the following:

    -   Domain NETBIOS name example: CONTOSO

    -   Lowercase full domain name: contoso.local

    -   Uppercase full domain name: CONTOSO.LOCAL

    -   For some [well-known security principals](https://support.microsoft.com/kb/243330), such as LOCAL SERVICE or ANONYMOUS LOGON, the value of this field is “NT AUTHORITY”.

    -   For local user accounts, this field will contain the name of the computer or device that this account belongs to, for example: “Win81”.

-   **Logon ID** \[Type = HexInt64\]**:** hexadecimal value that can help you correlate this event with recent events that might contain the same Logon ID, for example, “[4624](event-4624.md): An account was successfully logged on.”

**Process Information:**

-   **Process ID** \[Type = Pointer\]: hexadecimal Process ID of the process which started the new process with the new security token. Process ID (PID) is a number used by the operating system to uniquely identify an active process. To see the PID for a specific process you can, for example, use Task Manager (Details tab, PID column):

    <img src="images/task-manager.png" alt="Task manager illustration" width="585" height="375" />

    If you convert the hexadecimal value to decimal, you can compare it to the values in Task Manager.

    You can also correlate this process ID with a process ID in other events, for example, “[4688](event-4688.md): A new process has been created” **Process Information\\New Process ID**.

-   **Process Name** \[Type = UnicodeString\]: full path and the name of the executable for the process which ran the new process with new security token.

**Target Process:**

-   **Target Process ID** \[Type = Pointer\]**:** hexadecimal Process ID of the new process with new security token. If you convert the hexadecimal value to decimal, you can compare it to the values in Task Manager.

> You can also correlate this process ID with a process ID in other events, for example, “[4688](event-4688.md): A new process has been created” **Process Information\\New Process ID**.

-   **Target Process Name** \[Type = UnicodeString\]**:** full path and the name of the executable for the new process.

**New Token Information:**

-   **Security ID** \[Type = SID\]**:** SID of account through which the security token will be assigned to the new process. Event Viewer automatically tries to resolve SIDs and show the account name. If the SID cannot be resolved, you will see the source data in the event.

> **Note**&nbsp;&nbsp;A **security identifier (SID)** is a unique value of variable length used to identify a trustee (security principal). Each account has a unique SID that is issued by an authority, such as an Active Directory domain controller, and stored in a security database. Each time a user logs on, the system retrieves the SID for that user from the database and places it in the access token for that user. The system uses the SID in the access token to identify the user in all subsequent interactions with Windows security. When a SID has been used as the unique identifier for a user or group, it cannot ever be used again to identify another user or group. For more information about SIDs, see [Security identifiers](/windows/access-protection/access-control/security-identifiers).

-   **Account Name** \[Type = UnicodeString\]**:** the name of the account through which the security token will be assigned to the new process.

-   **Account Domain** \[Type = UnicodeString\]**:** subject’s domain or computer name. Formats vary, and include the following:

    -   Domain NETBIOS name example: CONTOSO

    -   Lowercase full domain name: contoso.local

    -   Uppercase full domain name: CONTOSO.LOCAL

    -   For some [well-known security principals](https://support.microsoft.com/kb/243330), such as LOCAL SERVICE or ANONYMOUS LOGON, the value of this field is “NT AUTHORITY”.

    -   For local user accounts, this field will contain the name of the computer or device that this account belongs to, for example: “Win81”.

-   **Logon ID** \[Type = HexInt64\]**:** hexadecimal value that can help you correlate this event with recent events that might contain the same Logon ID, for example, “[4624](event-4624.md): An account was successfully logged on.”

## Security Monitoring Recommendations

For 4696(S): A primary token was assigned to process.

| **Type of monitoring required**                                                                                                                                                                                                                                                                                   | **Recommendation**                                                                                                                                                                                                      |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **High-value accounts**: You might have high-value domain or local accounts for which you need to monitor each action.<br>Examples of high-value accounts are database administrators, built-in local administrator account, domain administrators, service accounts, domain controller accounts and so on. | Monitor this event with the **“Subject\\Security ID”** or **“New Token Information\\Security ID”** that corresponds to the high-value account or accounts.                                                              |
| **Anomalies or malicious actions**: You might have specific requirements for detecting anomalies or monitoring potential malicious actions. For example, you might need to monitor for use of an account outside of working hours.                                                                                | When you monitor for anomalies or malicious actions, use the **“Subject\\Security ID”** or **“New Token Information\\Security ID”** (with other information) to monitor how or when a particular account is being used. |
| **Non-active accounts**: You might have non-active, disabled, or guest accounts, or other accounts that should never be used.                                                                                                                                                                                     | Monitor this event with the **“Subject\\Security ID”** or **“New Token Information\\Security ID”** that corresponds to the accounts that should never be used.                                                          |
| **Account allowlist**: You might have a specific allowlist of accounts that are the only ones allowed to perform actions corresponding to particular events.                                                                                                                                                      | If this event corresponds to an “allowlist-only” action, review the **“Subject\\Security ID”** and **“New Token Information\\Security ID”** for accounts that are outside the allowlist.                                 |
| **Accounts of different types**: You might want to ensure that certain actions are performed only by certain account types, for example, local or domain account, machine or user account, vendor or employee account, and so on.                                                                                 | If this event corresponds to an action you want to monitor for certain account types, review the **“Subject\\Security ID”** or **“New Token Information\\Security ID”** to see whether the account type is as expected. |
| **External accounts**: You might be monitoring accounts from another domain, or “external” accounts that are not allowed to perform certain actions (represented by certain specific events).                                                                                                                     | Monitor this event for the **“Subject\\Security ID”** or **“New Token Information\\Security ID”** corresponding to accounts from another domain or “external” accounts.                                                 |
| **Restricted-use computers or devices**: You might have certain computers, machines, or devices on which certain people (accounts) should not typically perform any actions.                                                                                                                                      | Monitor the target **Computer:** (or other target device) for actions performed by the **“Subject\\Security ID”** or **“New Token Information\\Security ID”** that you are concerned about.                             |
| **Account naming conventions**: Your organization might have specific naming conventions for account names.                                                                                                                                                                                                       | Monitor **“Subject\\Security ID”** or **“New Token Information\\Security ID”** for names that don’t comply with naming conventions.                                                                                     |

-   If you have a pre-defined “**Process Name**” or “**Target Process Name**” for the process reported in this event, monitor all events with “**Process Name**” or “**Target Process Name**” not equal to your defined value.

-   You can monitor to see if “**Process Name**” or “**Target Process Name**” is not in a standard folder (for example, not in **System32** or **Program Files**) or is in a restricted folder (for example, **Temporary Internet Files**).

-   If you have a pre-defined list of restricted substrings or words in process names (for example, “**mimikatz**” or “**cain.exe**”), check for these substrings in “**Process Name**” or “**Target Process Name**”.

-   It can be uncommon if process runs using local account.

