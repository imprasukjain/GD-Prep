# GD Room

Personal group discussion (GD) practice for MBA placements. It's a single static page: no backend, no database, no login.

## How it works

- **Topics:** 60 built-in GD topics across 6 types and 3 difficulty levels.
- **Roles:** Initiate (60 s), Enter mid-GD (45 s, after 3 AI participants), Summarize (60 s, after 6 AI points).
- **Recording:** with a Gemini key, your audio is recorded and converted to 16 kHz WAV in the browser. It's sent to Gemini in one call, which returns a verbatim transcript (fillers included), delivery notes and a panel scorecard.
- **Local metrics:** pauses are measured locally from the audio itself. Pace, fillers, numbers, examples, signposts and stakeholders are computed from the transcript.
- **Without a key:** it falls back to the browser's Web Speech API and shows local metrics only.
- **Nothing is saved:** every round is gone when you leave the page.

## Get a Gemini API key

1. Go to https://aistudio.google.com and choose **Get API key**, then **Create API key**.
2. Open the deployed site, expand **Gemini settings**, paste the key and click **Save and connect**.
3. Tick **Remember on this device** only on your own phone or laptop.

The key never goes in this repo. It lives only in your browser's storage and is sent only to `generativelanguage.googleapis.com`.

## Lock the key down (recommended)

In Google Cloud Console, open **APIs & Services**, then **Credentials**, then your key.

1. Under **Application restrictions**, choose **Websites** and add `https://<your-username>.github.io/*`. If you also test locally, add `http://localhost:*/*`.
2. Under **API restrictions**, select only the **Generative Language API**.

With these set, a leaked key is useless anywhere else.

## Deploy to GitHub Pages

Deployment is automated by `.github/workflows/pages.yml`: every push to `main` publishes `index.html` to GitHub Pages.

One-time setup: on GitHub, open **Settings**, then **Pages**, and under **Source** choose **GitHub Actions**. The site goes live at `https://<your-username>.github.io/<repo-name>/` once the workflow finishes. You can also re-run it by hand from the **Actions** tab (**Deploy to GitHub Pages**, then **Run workflow**).

## Run locally

The mic needs `localhost` or `https`. Opening the file directly with `file://` won't record.

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Notes

- Chrome or Edge on desktop gives the best experience. Safari works. Firefox works only with a Gemini key, since it has no Web Speech.
- On the Gemini API free tier, Google may use prompts and audio to improve its products. Enable billing on the key's project if you don't want that. The Google AI Pro monthly Cloud credit can cover it.
- If the default model is retired or rate-limited, pick another in **Gemini settings**. The list is pulled live from your key.
