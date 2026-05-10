# Close Reader

A live classroom annotation tool. Teachers upload any piece of writing; students tag and annotate phrases in real time.

## How it works

**Teacher** opens `index.html`, pastes a text excerpt, configures which tags are available, and clicks **Create Session**. This generates two links:

- **Student link** — share with the class (no special access)
- **Teacher link** — keep private; grants the ability to see all annotations, delete them, and export data

**Students** open the student link, enter their name, and start reading. Clicking any phrase opens a popover where they can apply one or more tags and write an optional note. Annotations appear live for everyone without a page refresh.

## Features

- Paste any text — sentences are split into clickable phrases automatically
- 8 default tags: Confusing, Interesting, Important, Surprising, Question, Quotable, Agree, Disagree
- Teachers can toggle tags on/off and add custom ones before creating a session
- Student annotations are attributed by name and visible to the teacher in real time
- Colored dot indicators on each phrase show at a glance where the class is engaging
- Teacher view: see all annotations per phrase, delete individual entries, clear everything, or export as JSON
- No accounts or installs — runs entirely in the browser

## Stack

Vanilla HTML/CSS/JS, no build step. Firebase Realtime Database for live sync.

Each session is stored at `sessions/{CODE}` in the database. The teacher token is stored in session metadata and validated client-side; the student link carries no token.

## Running locally

Open `index.html` directly in a browser or serve the folder with any static file server:

```bash
npx serve .
```

The Firebase project is already configured in both files — no setup needed.

## Session data structure

```
sessions/{SESSION_CODE}/
  meta/
    title          string
    source         string
    createdAt      timestamp
    teacherToken   string
    tags           [{id, label, color}]
  phrases          string[]
  annotations/
    {phraseIndex}/
      {studentId}/
        tags        string[]
        note        string
        studentName string
        createdAt   timestamp
```
