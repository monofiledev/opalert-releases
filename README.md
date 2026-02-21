# OpAlert

OpAlert is a standalone, client-side Reddit monitoring utility built with Flutter. It autonomously scans targeted subreddits for high-intent keywords and delivers local push notifications, allowing users to identify and engage with leads in real-time. 

By utilizing local background processing, OpAlert operates entirely on the user's device, requiring no centralized database, and no recurring server costs.

## Core Features

* **Zero-Configuration Parsing:** Retrieves public community discussions directly, bypassing complex OAuth setups and commercial API restrictions.
* **Autonomous Background Polling:** Utilizes Android's `Workmanager` to run silent background scans (approx. every 20 minutes) without draining battery life.
* **Local Push Notifications:** Alerts the user instantly when a tracked phrase is mentioned, deep-linking directly to the Reddit thread.
* **Time-Based Categorization:** Automatically calculates the Unix Epoch timestamp of comments and categorizes leads as **New** (< 1 hour), **Recent** (< 48 hours), or **Older**.
* **Local Bookmarking:** Saves high-value leads to persistent local storage (`SharedPreferences`) for later engagement.
* **Topic Agnostic:** Functions entirely based on user-defined parameters. Can be used for lead generation, brand monitoring, or general keyword tracking.


## Installation & Build Instructions

This repository is configured with a GitHub Actions CI/CD pipeline. 

1. Fork or clone this repository.
2. Navigate to the **Actions** tab in your GitHub repository.
3. Trigger the `Build Native Flutter APK` workflow.
4. Download the generated `.apk` artifact and install it directly on your Android device.

## Usage Guide

### 1. Configuration
Navigate to the **Settings** tab within the app to define your monitoring parameters.
* **Subreddits:** Enter target subreddits separated by commas (e.g., `webdev, productivity, SaaS`). Do not include the `r/` prefix.
* **Trigger Phrases:** Enter exact keywords or phrases (e.g., `how do I organize, looking for a tool, tired of`). The scanner uses strict string matching and will flag any comment containing these exact sequences.

### 2. Live Scanning
Navigate to the **Live** tab and press "Manual Scan" to immediately fetch the latest 100 comments from your target subreddits and filter them against your trigger phrases. 

### 3. Auto-Scan (Background Mode)
Toggle the **Auto-Scan** switch in the top right corner of the app bar. Android will schedule a background worker to poll your targets approximately every 20 minutes. If a match is found that has not been previously alerted, you will receive a system push notification.

## Disclaimer & Rate Limiting

OpAlert is a client-side utility and is subject to standard network rate limiting. 
* The background service is intentionally throttled to 20-minute intervals to respect server loads and prevent temporary IP blocks.

