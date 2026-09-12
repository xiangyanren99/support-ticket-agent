# offline-documentation-guide.md

> **Portfolio demonstration document. This guide is fictional and must not be used for real clinical or operational decisions.**

# Offline Documentation Guide

**Organization:** Northstar Community Care
**Guide ID:** MOB-OFF-207
**Application:** Northstar Visit Mobile
**Document owner:** Mobile Support Team

## Purpose

Northstar Visit Mobile allows clinicians to enter visit documentation when internet access is unavailable. Offline mode is intended to support temporary connectivity loss and is not a replacement for regular synchronization.

## Before leaving Wi-Fi

Before beginning field visits, clinicians should:

* Sign in while connected to a trusted network.
* Open the daily schedule and confirm that assigned visits are visible.
* Select **Prepare for Offline Use** from the application menu.
* Wait until the message **Offline preparation complete** appears.
* Confirm the device has sufficient battery life.
* Avoid signing out after offline preparation is complete.

Clinicians should never use unsecured public devices to access the application.

## How offline documentation works

When the device loses connectivity, newly entered documentation is stored locally in encrypted application storage. A banner labeled **Working Offline** appears at the top of the screen.

Locally stored notes are marked **Pending Sync**. They have not reached the central system until synchronization finishes successfully.

Clinicians should keep the application installed and avoid deleting its data while records remain pending.

## When connectivity returns

The application automatically attempts to synchronize when a stable connection becomes available. The clinician should keep the application open until each visit shows **Synced**.

A spinning icon means synchronization is still in progress. A red warning icon means additional action is required.

## Basic troubleshooting

When documentation does not synchronize:

1. Confirm the device has internet access.
2. Keep the application open for two minutes.
3. Select **Sync Now**.
4. Confirm the correct account is signed in.
5. Restart the application once.
6. Do not repeatedly submit the same visit.

Fictional error code **NS-417** means the application found a pending record with incomplete required fields. The clinician should reopen the visit, review highlighted fields, save, and retry synchronization.

## When to contact support

Contact support when:

* Records remain pending after two synchronization attempts.
* Error NS-417 continues after required fields are completed.
* The application closes unexpectedly during synchronization.
* A visit disappears from the schedule.
* The device reports that local storage is unavailable.

Provide the visit date, application version, device type, error code, and troubleshooting steps already attempted. Do not include patient-identifying information in the initial support ticket.