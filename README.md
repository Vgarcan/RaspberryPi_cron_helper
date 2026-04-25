
# ![XEMI CRON HELPER](xemi_cron_helper.png)

# XEMI Cron Helper

Interactive Bash assistant for creating, listing, editing and deleting Linux user cron jobs.

Designed to make `crontab` easier and safer to use from a visual terminal menu.

---

## Table of Contents

* [About](#about)
* [Features](#features)
* [Safety Model](#safety-model)
* [Requirements](#requirements)
* [Installation](#installation)
* [Usage](#usage)
* [Supported Cron Formats](#supported-cron-formats)
* [Generated Job Format](#generated-job-format)
* [Logs](#logs)
* [Examples](#examples)
* [Limitations](#limitations)
* [License](#license)
* [Author](#author)

---

## About

**XEMI Cron Helper v1.3** is a visual terminal tool for managing user cron jobs on Linux.

It helps you:

* create cron jobs with a guided schedule assistant
* list existing jobs
* separate generated jobs from manual jobs
* edit jobs interactively
* delete jobs with confirmation
* attach optional log files to cron commands
* view job logs from the menu

It works with the user crontab managed by:

```bash
crontab -l
crontab -e
crontab -u <user>
````

---

## Features

* Guided cron job creation
* Standard 5-field cron expression support
* Common macro support, such as `@reboot`, `@daily`, `@hourly`
* Schedule validation
* Minute, hour and weekday validation
* Optional job name using `CronJob-ID`
* Optional comments/descriptions
* Optional per-job log redirection
* Duplicate job prevention
* List generated and manual jobs separately
* Edit schedule, command, log path, name and comment
* Delete by job number or `CronJob-ID`
* Double confirmation before deleting
* Preserves environment lines such as `PATH=`, `SHELL=` and `MAILTO=`
* Action logging under `~/.xemi_logs`

---

## Safety Model

The helper does not directly edit crontab blindly.

It works by:

1. reading the current user crontab into a temporary file
2. parsing cron job lines and metadata comments
3. applying the selected change
4. writing the updated crontab back with `crontab`

Temporary files are created using:

```bash
mktemp
```

Delete operations require two confirmations.

Duplicate jobs are skipped if the same schedule and command already exist.

When launched with `sudo`, the script tries to resolve the real user and manage that user's crontab instead of accidentally writing to root's crontab.

---

## Requirements

Required:

```bash
bash
cron
crontab
getent
awk
grep
sed
mktemp
hostname
```

Recommended:

```bash
less
```

Check cron service status:

```bash
systemctl status cron
```

On some distributions the service may be called:

```bash
systemctl status crond
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/Vgarcan/xemi_cron_helper.git
cd xemi_cron_helper
```

Make executable:

```bash
chmod +x xemi_cron_helper
```

Run locally:

```bash
./xemi_cron_helper
```

Optional global install:

```bash
sudo mv xemi_cron_helper /usr/local/bin/
```

Then run:

```bash
xemi_cron_helper
```

---

## Usage

Start the helper:

```bash
xemi_cron_helper
```

Main menu:

```text
1) Create a new cron job (guided)
2) List current cron jobs
3) Edit an existing cron job
4) Delete a cron job
5) Exit
```

---

## Supported Cron Formats

The helper supports standard cron expressions:

```text
MIN HOUR DAY MONTH WEEKDAY command
```

Example:

```cron
0 5 * * 1 /home/victor/scripts/backup.sh
```

It also supports common cron macros:

```text
@reboot
@yearly
@annually
@monthly
@weekly
@daily
@midnight
@hourly
```

Example:

```cron
@reboot /home/victor/scripts/startup.sh
```

Cron field examples:

```text
*        every value
*/15     every 15 units
1,3,5    list of values
1-5      range
mon-fri  weekday names
jan,apr  month names
```

---

## Generated Job Format

When you create a job with a name and comment, the helper writes it like this:

```cron
# [CronJob-ID]: backup_media
# Daily backup for Django media files
0 2 * * * /home/victor/scripts/backup_media.sh >> "/home/victor/logs/cronjobs/backup_media.log" 2>&1
```

The `CronJob-ID` lets you find, edit or delete the job more easily later.

The helper also recognises legacy metadata blocks using:

```cron
# [XEMI-ID]: old_job_name
```

---

## Logs

The helper writes its own action log to:

```bash
~/.xemi_logs/cron_helper.log
```

Example entry:

```text
[2026-04-25 16:30:12] user=victor host=server01 created cron job for victor schedule='0 2 * * *' command='/home/victor/scripts/backup.sh' log='/home/victor/logs/cronjobs/backup.log'
```

Cron jobs can also have their own output logs.

Default job log directory:

```bash
~/logs/cronjobs
```

Example:

```bash
/home/victor/logs/cronjobs/backup_media.log
```

---

## Examples

### Run a Django cleanup command every day

```cron
0 3 * * * /home/victor/project/.venv/bin/python /home/victor/project/manage.py clearsessions >> "/home/victor/logs/cronjobs/django_clearsessions.log" 2>&1
```

### Run a backup every Sunday at 2 AM

```cron
0 2 * * 0 /home/victor/scripts/weekly_backup.sh >> "/home/victor/logs/cronjobs/weekly_backup.log" 2>&1
```

### Run a script every 15 minutes

```cron
*/15 * * * * /home/victor/scripts/check_services.sh >> "/home/victor/logs/cronjobs/check_services.log" 2>&1
```

### Run a command at reboot

```cron
@reboot /home/victor/scripts/start_local_services.sh >> "/home/victor/logs/cronjobs/startup.log" 2>&1
```

---

## Limitations

This helper manages user crontabs only.

It does not manage:

```text
/etc/crontab
/etc/cron.d/*
/etc/cron.daily
/etc/cron.hourly
/etc/cron.weekly
/etc/cron.monthly
systemd timers
```

Environment lines such as these are preserved, but not edited through the helper:

```cron
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
SHELL=/bin/bash
MAILTO=""
```

The helper is designed for common cron management tasks, not as a full replacement for advanced cron or systemd timer configuration.

---

## License

MIT License

---

## Author

Victor Garcia

GitHub:

```text
https://github.com/Vgarcan
```

```

