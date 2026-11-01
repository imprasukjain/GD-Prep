# Placement Prep One-Stop

Speaking practice in a single static page: no backend, no database, no login. It has two modes, switched with the tabs at the top. It always opens in the light theme; the 🌙 Dark button in the header switches to dark, and the page remembers your choice on that device.

- **GD Room:** group discussion practice for MBA placements, with optional Gemini feedback.
- **Yap: daily speaking** (opens by default): speaking practice for MBA placement interviews, scored entirely in the browser. No AI and no key. If you switch to GD Room, the page remembers that on your device.

## Yap: daily speaking

- **Topics:** 180 built-in MBA placement prompts across 15 categories, each at Easy, Mid or Hard:
  - Interview: HR and personal; why MBA, role and company; behavioural (STAR) stories.
  - Domain: marketing, finance, operations and supply chain, HR and people management, strategy and consulting, product and analytics, economy and current affairs.
  - Cases and thinking: mini cases, guesstimates, sell-it and pitch questions.
  - GD and random: abstract GD topics, and random or fun questions.

  *Surprise me* picks a random category and level, and questions don't repeat until you've seen every one in that set.
- **Round:** optional think time (none, 10 or 30 s), then 30, 60 or 90 seconds of speaking, ending with a chime. Transcription uses the browser's Web Speech API, so Chrome and Edge send the audio to Google and Safari sends it to Apple. Firefox isn't supported, and in-app browsers (Instagram, LinkedIn and so on) get a prompt to open the page in a real browser.
- **Accurate transcripts with a Gemini key:** the browser's free speech engine is built for live captions. It drops words around pauses, deletes "um" and "uh", and struggles with Indian accents and terms. So when a Gemini key is saved, Yap also records your audio, and after the round Gemini transcribes it word for word (fillers included). The delivery score, pauses and content check all come from that transcript, and pace is measured from your first word to your last. Without a key, or if Gemini fails, the browser's transcript is used. On phones with a key, only the recording runs, because phones can't share the mic between recording and live recognition.
- **Your English:** India (default), US or UK. This tells the browser's speech engine which accent to expect; India English is much better at Indian accents, names and terms like lakh and crore.
- **Delivery score (0 to 100):** fixed arithmetic, no AI.
  - Pace, up to 55 points: full marks anywhere from 120 to 160 words a minute, falling to zero at 60 or 240.
  - Fillers, up to 25 points: falls to zero at 16 fillers per 100 words. It counts um, uh, er, ah, hmm, you know, I mean, kind of, sort of, basically, actually, literally, honestly, anyway, and "like" only when it isn't grammatical ("I'd like to" doesn't count). Speech engines often delete "um" from their final text, so ums seen in the live text but dropped later are counted too.
  - Staying power, up to 20 points: full marks for talking the whole time.
- **Fair-capture checks:** under 20 words or 20 seconds is "too short to score". Talking for 20 seconds or more but captured at under 40 wpm means the speech service dropped out, so no score is given. Echoed text that some Android phones resend is removed before counting.
- **Feedback:** a score band, a pace verdict, one targeted tip for the next rep, and keyword signals on what you said: word variety, an overused word, linking words, heavy hedging, and whether you landed a closing line. A missing example is only flagged when the question asks for one (behavioural questions, "give an example", "a time you…"). These are pattern matches, not understanding. If very few words were caught for the time spoken (under 85 a minute), the page warns that the speech engine may have missed words.
- **Content check (optional, needs a Gemini key):** after a round, Gemini gets the question and your recording (or, without a recording, the browser's transcript). It returns a verdict and accuracy out of 10, what you got right, what was wrong with the correct version, what a strong answer also covers, a model answer under 80 words, and the follow-up an interviewer would likely ask. It runs after every answer. Domain questions get a fact check (Accurate to Inaccurate); HR, behavioural, case and other questions are judged the way a panel would judge them (Strong to Weak), without demanding facts or examples the question doesn't need. Without a key, Yap shows a prompt to add one.
- **Sharing:** *Challenge a friend* copies or shares a link like `?yap=fin-m1` that opens the same question. *Save score card* makes a 1080×1350 PNG.
- **Streak:** the days you practised are kept in this browser only, to show a daily streak.

## GD Room

- **Topics:** 60 built-in GD topics across 6 types and 3 difficulty levels.
- **Roles:** Initiate (60 s), Enter mid-GD (45 s, after 3 AI participants), Summarize (60 s, after 6 AI points).
- **Recording:** with a Gemini key, your audio is recorded and converted to 16 kHz WAV in the browser. It's sent to Gemini in one call, which returns a verbatim transcript (fillers included), delivery notes and a panel scorecard.
- **Local metrics:** pauses are measured locally from the audio itself. Pace, fillers, numbers, examples, signposts and stakeholders are computed from the transcript.
- **Without a key:** it falls back to the browser's Web Speech API and shows local metrics only.
- **Nothing is saved:** every round is gone when you leave the page.

## Get a Gemini API key

1. Go to https://aistudio.google.com and choose **Get API key**, then **Create API key**.
2. Open the deployed site, expand **Gemini settings** at the top (shared by both tabs), paste the key and click **Save and connect**.
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
