---
name: automate-boring-stuff
description: Applies Al Sweigart's "Automate the Boring Stuff with Python" framework — spotting repetitive/rule-based manual tasks worth scripting, picking the right tool (regex, file/folder ops via os/shutil/pathlib, CSV/Excel/PDF/Word/JSON handling, web scraping with requests/BeautifulSoup or Selenium, scheduling, email/SMS, GUI automation with pyautogui as a last resort), and safe-automation habits (dry runs, testing on samples, try/except around flaky steps) — to any task about automating a repetitive computer task with Python. Use whenever the user wants to "automate the boring stuff," mentions renaming/organizing/moving files in bulk, scraping a website, reading/writing Excel/CSV/PDF/Word programmatically, scheduling a script, sending automated emails, or automating clicks/keystrokes — even if they don't name the book.
---

# Automate the Boring Stuff with Python

Apply this skill when the user wants to turn a repetitive, manual, computer-based task into a script. The book's core value isn't clever code — it's picking the right practical tool for the task and not breaking things while automating them.

## Core concepts

**Is this worth automating?** — Good candidates are tasks that are repetitive, rule-based (a human could write down the steps as a checklist), and either time-consuming or error-prone by hand. If a task is a one-off or requires real judgment calls each time, a script may cost more to write than it saves — flag this tradeoff rather than automating reflexively.

**Regex and string handling** — Use regular expressions for pattern-based text extraction/validation (emails, phone numbers, log lines, filenames matching a pattern); use plain string methods (`split`, `strip`, `replace`, f-strings) when the pattern is simple — regex adds power but also fragility and unreadability, so don't reach for it by default.

**File and folder operations** — Use `os`/`shutil`/`pathlib` for bulk copy/move/rename/delete across files and directories. For anything destructive or hard to undo (bulk rename, bulk delete, overwriting files), do a dry run first: print what *would* happen before actually doing it, and prefer generating a log of changes made — bulk file operations are one of the easiest ways to silently destroy real user data.

**Structured file formats** — Read/write CSV with the `csv` module, Excel with `openpyxl`, PDFs with a PDF library (extraction is often messy — text layout doesn't always extract cleanly), Word docs with `python-docx`, and JSON with the built-in `json` module. The goal is always to get data out of (or into) a format a script can work with programmatically instead of a human doing it by hand in the GUI.

**Web scraping** — Use `requests` + `BeautifulSoup` for static pages (fetch HTML, parse with selectors); use Selenium (or similar) only when the page requires JavaScript execution, logins, or interaction to reveal the content. Before scraping, check whether the site offers an API instead (more stable than scraping), and be mindful of rate limits, `robots.txt`, and the site's terms of service — flag this explicitly rather than assuming scraping is always fine.

**Scheduling instead of babysitting** — For anything that needs to run repeatedly, use the OS's own scheduler (cron, Windows Task Scheduler) or a scheduling library, rather than a script sitting in an infinite loop with `time.sleep()` — the latter dies with the terminal/process and doesn't survive reboots.

**Automated communications** — Sending email/SMS programmatically (e.g. via `smtplib` or a transactional email/SMS API) is useful for notifications on completion/failure of longer automations — treat credentials for these carefully (never hardcode them in the script) and consider rate limits so a bug doesn't turn into a spam incident.

**GUI automation as last resort** — `pyautogui`-style keyboard/mouse automation (clicking specific screen coordinates, sending keystrokes) is the least robust option — it breaks with screen resolution, window position, or UI changes. Reach for it only when there's no API or file-based way to accomplish the task, and note the fragility to the user.

**Safe-automation habits** — Test on a small sample or a copy of the data before running at full scale, especially for anything that modifies or deletes files. Wrap flaky steps (network calls, file I/O, external services) in `try`/`except` so one failure doesn't silently corrupt a batch job, and log what happened rather than only printing to a console that'll be gone after the run.

**Readable over clever** — Prefer straightforward stdlib and well-known libraries over cleverness; a script that runs occasionally to save someone time should be easy to re-read and modify later, not maximally elegant.

## How to apply this

1. **Confirm the task is actually worth automating** — repetitive, rule-based, and costly enough by hand to justify the script.
2. **Pick the tool that matches the task**, not the most familiar one: plain strings vs. regex for text; `os`/`shutil`/`pathlib` for file operations; the right library for CSV/Excel/PDF/Word/JSON; `requests`+BeautifulSoup vs. Selenium for the web; scheduler vs. sleep-loop for recurring runs; GUI automation only as a last resort.
3. **For anything destructive (bulk rename/move/delete/overwrite)**, insist on a dry run or preview step before it runs for real, and suggest logging what changed.
4. **For scraping**, check for an API alternative first and flag rate-limit/ToS considerations.
5. **Wrap unreliable steps in error handling** and suggest testing on a small sample before scaling up to the full dataset/folder.
6. **Keep the resulting script simple and readable** — this is a personal-productivity tool, not production infrastructure, unless the user says otherwise.

Ground every suggestion in the user's actual task and files — this is a practical automation checklist, not an exhaustive library reference.
