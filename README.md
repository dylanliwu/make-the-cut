https://github.com/user-attachments/assets/0d13e615-b816-4c2d-91a0-e4354bda79d3

PASTE_YOUR_EXISTING_VIDEO_LINE_HERE

# Make the Cut

Live at [makethecut.ca](https://makethecut.ca)

At McMaster, first year engineering is general and your GPA decides which stream you get into. McMaster doesn't release the cutoffs, so most people are just guessing.

Make the Cut lets students enter their grades and stream choices, then estimates the GPA you need for each stream based on everyone's submissions. It's had 11,000+ submissions so far and around 500 students use it each year.

## How it works

1. Students enter their grades and rank the streams they want.
2. Fake or unrealistic submissions get filtered out (like a perfect grade in every course or a 0 GPA).
3. A Node.js serverless function simulates the actual stream allocation. It sorts everyone by GPA, scales each stream's seat count to match the number of submissions, and places each student into their top choice that still has room.
4. The GPA of the last person placed in a stream becomes that stream's predicted cutoff. This gets combined with university stats in a weighted average.
5. Cutoffs are precomputed and saved, so the site just reads the results instead of rerunning the simulation every time someone loads the page.

After placements come out, students can report what stream they actually got, so we can compare the predictions against real results.

## Tech

- React + TypeScript frontend
- Appwrite for the database and auth
- Node.js serverless functions for the cutoff calculations

## Structure

```
frontend/    React app
backend/     serverless functions (validation + allocation)
utils/       shared helpers
types.d.ts   shared types
```

## Running locally

```bash
git clone https://github.com/dylanliwu/make-the-cut.git
cd make-the-cut/frontend
npm install
npm run dev
```

You'll need your own Appwrite project set up in a `.env` file.

## Limitations

- People who submit might not represent the whole class.
- Seat counts per stream are estimates since McMaster doesn't publish them.
- It's a prediction, not a guarantee.
