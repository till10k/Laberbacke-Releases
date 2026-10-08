# Laberbacke

### Hold a key. Talk. Let go. Your words are already in the text field.

**Voice dictation for macOS that lands text in *any* app — and costs cents a month instead of $15.**

Laberbacke is a push-to-talk dictation app for Apple Silicon Macs. You hold **Fn**
(or right ⌘ / right ⌥), you speak, you let go — and cleanly formatted text appears
at the cursor of whatever app you were already working in. Slack, Gmail, ChatGPT,
Claude, Notes, Terminal, Google Docs, your editor. No window to switch to, no
"copy the transcript" step, no waiting.

When connected, it streams your audio **while you are still talking**, so the transcript is
essentially finished the moment you release the key.

**Measured on the shipping build: 0.45–0.5 s from key-up to text in the field.**

**No connection? Keep recording.** Completed recordings are saved on your Mac,
survive app restarts, and are transcribed automatically when the connection and
your account are ready. Find the finished text in History.

[**⬇ Download the latest release**](../../releases/latest)

---

## Why not just buy Wispr Flow?

Because you would pay **$180 a year** for something you can have for **the price of a
coffee — per year**.

Laberbacke has no subscription and no markup. You pay Google's transcription rate
directly, per second of speech you actually produce. That is the entire cost model.

| | **Laberbacke** | **Wispr Flow** |
|---|---|---|
| **Price** | **No subscription.** Pay-per-use at cost: **$0.009 / audio minute** (streaming) or $0.005 (batch) | **$15 / user / month**, $12/mo billed annually |
| **Realistic monthly bill** | **~$1.04** at 20 dictations/day · **~$2.61** at 50/day · **~$5.22** at 100/day | $15 flat, whether you dictate once or a thousand times |
| **Free tier** | No tier. Every dictation costs the same fraction of a cent | 2,000 words/week on desktop, then it stops |
| **Break-even** | You would have to speak **27.8 hours per month** — ~287 dictations *every single day* — before Laberbacke costs as much as Wispr Flow Pro | — |
| **Metering** | Per-second, billed against your own Google key or your org's | Per-seat |
| **Where your text lives** | Local SQLite on your Mac, auto-purged after 90 days. Transcript content is **never** logged | Cloud account |
| **Offline recordings** | Saves completed audio locally and transcribes it after reconnecting. Pending recordings survive restarts; retry, delete and copy from History. | — |
| **Text can never be lost** | Hard product rule: if the paste fails, the text is on the clipboard *and* in a card you can click *and* in your history | — |
| **Bring your own key** | Yes — point it at your own Google API key and the vendor is out of the loop entirely | No |
| **Self-updating** | Yes, silently, with a SHA-256 check against a signed manifest — and **never** mid-dictation | Yes |
| **Download size** | **19.5 MB** (v0.4.12 DMG) | — |

### The price math, in full

Google's paid-tier rate for the streaming transcription model is **$0.009 per audio
minute** (price list read 2026-09-01 from `ai.google.dev/gemini-api/docs/pricing`).
Across **350 real dictations** measured in production, the mean dictation was
**11.6 seconds** long (median 5.3 s, p90 27.1 s).

| Your habit | Speech per month | **Laberbacke** | Wispr Flow Pro | You keep |
|---|---|---|---|---|
| 20 dictations/day | 116 min | **$1.04** | $15.00 | **$167/yr** |
| 50 dictations/day | 290 min | **$2.61** | $15.00 | **$149/yr** |
| 100 dictations/day | 580 min | **$5.22** | $15.00 | **$117/yr** |
| 200 dictations/day | 1,160 min | **$10.44** | $15.00 | **$55/yr** |
| **287 dictations/day** | 1,667 min | **$15.00** | $15.00 | break-even |

Nobody dictates 287 times a day. That is the point: at 20–100 dictations a day —
which covers essentially everyone — **Laberbacke is 3–14× cheaper**, and the gap grows
the *less* you use it, because a subscription charges you for the days you don't talk.
Even at a punishing 200 dictations a day you are still ahead.

---

## Benchmarks — measured, not marketing

Every number below was measured on the target machine (Apple Silicon, macOS 26.5
"Tahoe") against the shipping build, not estimated.

| What | Result |
|---|---|
| **Key-down → microphone armed** | **76.6 ms** (design target: < 100 ms) |
| **Key-up → text in the target field** | **0.45–0.5 s** on the streaming path — the sum of measured stages: 25–45 ms recorder finish + ~250 ms stream harvest + ~2 ms pipeline + ~180 ms paste |
| Same figure *before* streaming shipped | **1.9 s median** over 53 dictations — the streaming rewrite cut end-to-end latency by roughly **4×** |
| **Stream finalization** after end-of-speech | **227–268 ms**, 7 runs, over 6 s and 8.8 s of audio |
| **Audio encoding cost** | **6.9 ms of CPU for 12 s of audio** — the encoder is not the bottleneck and never was |
| **Paste reliability** | **9 of 10 target apps passed**: Gmail, ChatGPT, Claude.ai, Slack, Notes, Google Docs, TextEdit, Terminal, Safari — umlauts and emoji intact in every one |
| macOS "Tahoe" sender filter | **Never triggered.** All nine went through the fast primary path (`cgEventPost`); the AppleScript fallback was never needed |
| **Local rescue model accuracy** | Parakeet TDT 0.6b v3: **4.8 % WER** on FLEURS-German, 5.5 % CoVoST, 7.05 % Tuda-De |
| Real-world dictation length | 350 dictations: median **5.3 s**, mean **11.6 s**, p90 27.1 s, p95 39.6 s |
| **Download size** | **19.5 MB** (v0.4.12 DMG) |

> **Read the fine print, because we wrote it:** the 0.45–0.5 s figure applies to
> dictations that run longer than the ~1.0–1.5 s stream setup. A very short dictation
> finishes before the stream is ready and falls back to the batch path, which is
> slower — and cheaper. We would rather tell you that than quote you a number that
> only holds on a good day.

---

## What it actually does

**Push-to-talk that stays out of your way.** Hold Fn, right ⌘ or right ⌥ — or bind
your own combination. Double-tap latches it for continuous dictation; Esc aborts.
Recording caps at 9 minutes with a warning at 8.

**It writes into the app you are already in.** Synthetic ⌘V first, then AppleScript,
then Unicode typing, then Accessibility — four escalating strategies, and your
clipboard is restored afterwards. Overridable per app.

**Your text is never lost. Ever.** That is the app's first rule, not a feature. If
the paste cannot land — no text field, no target app, secure input — the transcript
appears in a card above the speech bar and one click puts it on the clipboard. It is
also in your history. Nothing you said just evaporates.

**It punctuates for the spot your cursor is in.** Dictate into the middle of a
sentence and Laberbacke fixes the spacing *and* the punctuation on both sides.
"I'm amazed how" + "many" becomes "I'm amazed how many", not "howmany". The trailing
period the transcriber always adds gets dropped when it would cut a live sentence in
half — and added back when you are dictating *between* two sentences.

**It removes your filler words locally.** Live probes against the API proved the
model's own "smart" mode does not actually strip them. So Laberbacke does it on your
Mac: hesitation sounds, sentence-opening filler, abandoned run-ups, and explicitly
negated self-corrections ("by Tuesday, no, by Wednesday" → "by Wednesday"). Three
further rules are deliberately **switched off** because two adversarial test rounds
found nineteen cases where they destroyed meaning. We shipped the safe ones.

**Reprocess a recording without saying it again.** Add a missing name to your dictionary, then open the dictation in History and choose “Audio neu verarbeiten”, directly above Copy and Delete. New recordings stay locally with their history entry and are removed when that entry is deleted. Older entries without saved audio cannot be reprocessed; another transcription can incur additional usage charges.

**It learns your vocabulary from your corrections.** Fix a word once — names, tools,
email addresses — and Laberbacke writes it correctly from the next dictation on. The
*term* travels with the request; the *misrecognition* never leaves your device. Every
learned pair is a row you can delete with one click, because the learning rule is a
heuristic and heuristics need an off switch.

**Prompt mode for AI coding assistants.** Wraps your dictation in a proven prompt
scaffold — XML structure, three building blocks, task last — while preserving your
wording **character for character**. Toggle it live from the HUD, mid-dictation.

**Keep your recordings when the connection drops.** Completed offline recordings
and recordings affected by temporary transmission failures are saved in a local
queue. They are processed after reconnecting with the original account, and the
finished text appears in History. Nothing is pasted into an app you moved to later.
You can retry or delete recordings individually. The queue is limited to 256 MiB
and protects recordings after they have finished and been saved successfully;
a crash during recording or an online request is outside that protection.

**Local rescue remains available for supported processing failures.** When a local
model on the Neural Engine supplies a transcript, the app says "transcribed locally".
It is less accurate and is *never* the default.

**It never touches your microphone until you dictate.** Which means your music does
not stutter every time you open or close the app on AirPods.

---

## Requirements — the honest list

- **Apple Silicon Mac** (M1 or newer). Intel is not supported.
- **macOS 14** (Sonoma) or newer.
- **The interface is German.** Laberbacke is built German-first, and it is genuinely
  better at German dictation and German/English code-switching than English-first
  tools are. If you need an English UI, this is not your app yet.
- **An account created by the operator.** There is no self-service signup.
- The app is **self-signed and not notarized** — see below.

### Where Wispr Flow is still ahead, and we are not going to pretend otherwise

macOS only (no Windows, iOS or Android). No meeting notetaker. No SOC 2 / ISO 27001
certification. No App Store distribution, no self-serve signup, and a first-launch
Gatekeeper detour you have to click through. If you need any of those, buy theirs.

If you want the fastest, cheapest, most private way to get spoken German into a text
field on a Mac — keep reading.

---

## Download and verify

The current build is always under [**Releases**](../../releases/latest):

| File | What it is |
|---|---|
| `Laberbacke-<version>.dmg` | The app |
| `Laberbacke-<version>.dmg.sha256` | Checksum — **compare it before opening** |
| `INSTALLATION.txt` | Step by step, including Gatekeeper and Accessibility |
| `DATENSCHUTZ.txt` | What leaves the device and what does not (German) |
| `appcast.json` | The version manifest the app polls itself |

```bash
shasum -a 256 ~/Downloads/Laberbacke-<version>.dmg
```

The value must match `Laberbacke-<version>.dmg.sha256` character for character. If it
does not: **do not open it** — report it.

### Why the checksum matters here

The app is self-signed and **deliberately not notarized**. macOS therefore does *not*
verify for you that the file was not swapped in transit — so you do it. On first
launch macOS will refuse the app, often with the misleading claim that it is
"damaged". It is not. The one-time workaround is in `INSTALLATION.txt` and takes a
single click in System Settings.

The same rule holds for the app's own updates: it refuses any download whose SHA-256
does not match the manifest, keeps the running version aside rather than deleting it,
and rolls back if the new one fails to start.

---

## Privacy in one paragraph

Transcription happens in the cloud — that is how you get this speed and this
accuracy. What *stays* on your Mac: your history and saved recordings (local SQLite, purged after 90
days), your API key (a file only your user account can read), and every
misrecognition the app has learned from your corrections. **No transcript content and
no key is ever written to a log.** Deleting your history deletes its text and saved recordings;
only text-free quantities — seconds, tokens, counts — survive, so your cost total
stays honest. The full disclosure ships as `DATENSCHUTZ.txt` in every release, and
you should read it before your first dictation: your dictionary terms travel with
every request, even the ones you didn't say.

---

## Version history

Every release below carries its own changelog. Since **0.2.0** the app updates itself
— on launch and every four hours, checksum-verified, never in the middle of a
dictation, with a notice afterwards telling you what changed.

⚠️ **Version 0.1.0 is a dead end.** It has no self-update. Any Mac still on 0.1.0 will
never receive another version automatically and must be replaced by hand.

[**→ All releases**](../../releases)

---

<sub>Source code lives privately in `till10k/Laberbacke`. This repository distributes
the built application only.</sub>

<sub>Wispr Flow is a trademark of its respective owner and is referenced here for
comparison only. Competitor pricing and feature claims were taken from
`wisprflow.ai/pricing` on 2026-09-08 and may change. Laberbacke performance figures
were measured on Apple Silicon under macOS 26.5; your results will vary with network,
hardware and how you speak. Transcription costs are Google API list prices passed
through at cost and are not a quoted price.</sub>

---

<sub>© 2026 Rügamer-Steiner. All rights reserved.</sub>
