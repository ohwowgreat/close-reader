# Close Reader

A live classroom annotation tool. Teachers paste any text into a shared room; students click phrases to tag and annotate them in real time.

## How it works

Everyone goes to the same URL. The teacher creates a room with a code and password; students join with just the code and their name.

**Teacher** checks "I'm the teacher," enters a room code (e.g. `HIST101`) and a password, and joins. They get a floating **Edit Reading** button to open the edit panel, paste text, configure tags, and publish. The reading appears instantly for everyone in the room.

**Students** enter the room code and their name. Clicking any phrase opens the annotation sidebar where they can apply one or more tags and write an optional note. Annotations from all students appear live.

## Features

- Any text — sentences or paragraphs are split into clickable phrases automatically
- 8 default tags: Confusing, Interesting, Important, Surprising, Question, Quotable, Agree, Disagree
- Teachers can toggle tags on/off and add custom ones before publishing
- Colored dot indicators on each phrase show at a glance where the class is engaging
- Class annotations panel shows everyone's tags and notes on the selected phrase
- Teachers can export all room data as JSON
- No accounts or installs — runs entirely in the browser

## Stack

Single HTML file. Vanilla HTML/CSS/JS, no build step. Firebase Realtime Database for live sync.

## Running locally

Open `index.html` directly in a browser or serve the folder with any static file server:

```bash
npx serve .
```

## Firebase setup

The Firebase project is configured in `index.html`. Before it will work, set your Realtime Database rules to allow public read/write:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

## Data structure

```
rooms/{ROOM_CODE}/
  config/
    teacherPassword   string
    createdAt         timestamp
  content/
    title             string
    source            string
    rawText           string
    phrases           string[]
    tags              [{id, label, color}]
    publishedAt       timestamp
  annotations/
    {phraseIndex}/
      {studentId}/
        tags          string[]
        note          string
        studentName   string
        updatedAt     timestamp
```
