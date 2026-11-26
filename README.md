# Door Dash Academy

A Flask quiz game with four modes, a goofy door-runner stage, a question deck editor, and an account locker.

## Run it

From this folder in PowerShell (Python 3.10 or newer):

```powershell
python -m pip install -r requirements.txt
python app.py
```

Open the local address printed by Flask, usually `http://127.0.0.1:5000`.

## Publish it online

This project includes a Render Blueprint in `render.yaml`. To publish a public
version:

1. Put this project folder in a GitHub repository and push it to GitHub.
2. In Render, choose **New → Blueprint**, connect that repository, and approve
   the service described by `render.yaml`.
3. When the deployment finishes, Render will provide a public `onrender.com`
   URL you can share with your friends.

The Blueprint uses Render's free web-service plan. Free services may spin down
when idle, so the first visit after a quiet period can take longer. Hosting
plan availability and limits are controlled by Render and may change. The
application runs with Flask debug mode disabled in production.

Each player's points, unlocks, and question data remain in that player's
browser. This deployment does not create shared accounts, synchronize progress,
or restrict access to friends; anyone with the public URL can open the game.

## Modes

- **Learning:** three lives. When they run out, spend 100 account points to regain one life and retry.
- **One-hit:** one life and no point revives.
- **Creative:** one life plus a one-use 50:50, second chance, and sliding puzzle clue.
- **Exam:** full-screen questions, 30 seconds per question, one locked answer each, and results only after the deck is finished.

Use **Restart** to restart the current mode, or **Quit** to return to mode selection. A correct answer awards 10 points. The first two runners are free; other runners and the cosmetic items in the locker cost points.

Points, unlocked runners, and cosmetics are stored in browser local storage and persist across runs in that browser. Clearing site data or using another browser/device will not carry the balance over; this first version does not have server-side player accounts.

## Add questions

Choose **Import a PDF** to extract text from a PDF. Text PDFs are read directly; scanned pages use in-browser OCR. The importer asks how many questions to use and defaults to 10 random questions. The full imported question pool is saved, and every fresh run or restart draws a new random set and order from it. You can also change the run count in the question stash at any time; applying a new count during a run immediately restarts that mode. Exam mode includes its own count control. Imported text opens in the editor so you can correct OCR/layout issues. PDF.js and Tesseract.js load from public CDNs, so PDF import and OCR need an internet connection.

Four labeled options and an answer key work best:

```text
Question 1: Which planet has prominent rings?
A) Mars
B) Saturn
C) Venus
D) Mercury
Answer: B
```

Questions and answers stay in the browser using local storage. The background music is synthesized in the browser and can be muted.
