# TruLaL — True Last Logon for Active Directory

**TruLaL** provides a precise, defensible “true last logon” timestamp for Active Directory accounts by aggregating the non‑replicated `lastLogon` attribute from **every** domain controller (DC). It also surfaces the replicated `LastLogonDate` (i.e. `lastLogonTimestamp` in a human‑friendly form) to highlight expected replication lag.

> **Why this matters**
>
> * `lastLogon` is **accurate** but **not replicated** — you must query all DCs and take the most recent value.
> * `lastLogonTimestamp`/`LastLogonDate` is **replicated** but purposely **delayed** (~9–14 days by default), so it is unsuitable for near‑real‑time audits.
>
> **TruLaL** automates the per‑DC aggregation and gives you a trustworthy answer.

---

## Features

- Queries **all** DCs and converts raw FILETIME to `DateTime`.
- Calculates **True Last Logon** as the maximum of non‑null per‑DC values.
- Optionally exports **Summary** and **Per‑DC detail** to CSV.
- Displays `LastLogonDate` for context (replication lag awareness).
- Works with a **single user** or a **list of users**.

---

## Requirements

- **PowerShell 5.1+** or **PowerShell 7+**
- **ActiveDirectory** module (RSAT installed on a workstation, or run on a DC)
- Read access to user objects in the directory

---

## Installation

Clone the repository and place the script somewhere on your `$env:PATH` (or reference it by path).

```powershell
git clone https://github.com/<org-or-user>/TruLaL.git
cd TruLaL
