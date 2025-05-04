
# ![XEMI CRON HELPER](xemi_cron_helper.png)

# XEMI CRON HELPER - v1.3

> A powerful and interactive Bash tool to manage cron jobs with visual feedback, safety prompts and log integration.  
> Ideal for developers, sysadmins, and students who want an intuitive way to schedule and maintain periodic tasks.

---

## 📜 Table of Contents

- [](#)
- [XEMI CRON HELPER - v1.3](#xemi-cron-helper---v13)
  - [📜 Table of Contents](#-table-of-contents)
  - [🧰 Features](#-features)
  - [⚙️ Requirements](#️-requirements)
  - [📦 Installation](#-installation)
  - [🚀 How to Use](#-how-to-use)
    - [1. Create a Cron Job](#1-create-a-cron-job)
    - [2. List Cron Jobs](#2-list-cron-jobs)
    - [3. Edit a Cron Job](#3-edit-a-cron-job)
    - [4. Delete a Cron Job](#4-delete-a-cron-job)
  - [📝 Log Output](#-log-output)
  - [🧪 Example Use Case](#-example-use-case)
  - [📌 Notes](#-notes)
  - [🛠 Future Ideas](#-future-ideas)

---

## 🧰 Features

✅ Visual and interactive terminal UI  
✅ Easy cron expression setup (guided and custom)  
✅ View jobs with ID, comment, and log file  
✅ Edit name, schedule, command, and log path  
✅ Secure deletion with double confirmation  
✅ Supports automatic log path suggestions  
✅ Comment tagging to identify jobs  
✅ Designed to work under normal user context (not root)

---

## ⚙️ Requirements

- Bash Shell (`/bin/bash`)
- `crontab` command available
- GNU tools (`awk`, `grep`, `sed`, `less`)
- Works on most modern Linux distributions

---

## 📦 Installation

```bash
chmod +x xemi_cron_helper.sh
./xemi_cron_helper.sh
````

You can also move it to a global path:

```bash
sudo mv xemi_cron_helper.sh /usr/local/bin/xemi-cron
xemi-cron
```

---

## 🚀 How to Use

After running the script, you'll see a terminal interface like this:

```
╔════════════════════════════════════════════╗
║           XEMI CRON HELPER - v1.3          ║
╚════════════════════════════════════════════╝
```

### 1. Create a Cron Job

* Guided prompts to select **when** to run your task.
* Custom option for advanced cron users.
* Add optional name, description, and output log.

### 2. List Cron Jobs

* View all jobs with metadata, description, schedule, and log location.
* View logs directly from the script.

### 3. Edit a Cron Job

* Select job by number or CronJob-ID.
* Modify schedule, command, comment, log or name.
* Fully interactive and non-destructive.

### 4. Delete a Cron Job

* Safe interface with visual preview.
* Requires double confirmation.
* Deletes job and its metadata in one go.

---

## 📝 Log Output

If you choose to log job output, logs will be stored by default in:

```
~/logs/cronjobs/your-job-name.log
```

You can change the path when creating/editing the job.

---

## 🧪 Example Use Case

Let’s say you want to **run a Python script every day at 3AM** and save its output:

```
Select: Create a new cron job
→ Option 4 (Specific time every day)
→ Hour: 3 | Minute: 0
→ Command: /home/user/scripts/clean_db.py
→ Add name? Yes → "clean_db"
→ Add comment? Yes → "Daily cleanup task"
→ Save log? Yes → (default path suggested)
→ Confirm and save ✅
```

Now your cron job is fully tagged, logged, and documented.

---

## 📌 Notes

* XEMI CRON HELPER does not overwrite your entire crontab.
* It loads your current jobs, updates one at a time.
* Jobs without metadata comments are still supported and shown.
* Supports jobs for the **current user only**.

---

## 🛠 Future Ideas

* Backup/restore crontabs
* Export/import cron jobs as JSON
* Syntax validation for custom cron expressions
* Support for `@reboot`, `@hourly`, etc.

---

© 2025 · Created with 💙 by Víctor G.C. · XEMI Tools Project

