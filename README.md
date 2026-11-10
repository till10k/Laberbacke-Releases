# Laberbacke

### Hold a key. Speak. Put your words where you are working.

Laberbacke is a dictation app for Apple Silicon Macs. Hold your recording key,
speak, and release it to insert the completed text into your current app.
Your dictionary, familiar work terms, history and saved recordings stay part
of the same workflow.

Version 0.7.2 lets every user choose **Gemini, MAI Transcribe or Soniox** in
**Settings → Language → Transcription model**. Your choice stays saved for your
Laberbacke account on this Mac, including after restarting or signing out.
Another account keeps its own selection.

Audio streams directly from your Mac to the selected provider while you speak.
Your Laberbacke account supplies short-lived access; permanent provider keys stay
on the server. Active dictations finish on their original model. New recordings
and audio reprocessing use your current choice. Without a personal choice, the
shared administrator default applies; Soniox uses the European Union region.

[**Download the latest release**](../../releases/latest)

### Pay for audio, without a Laberbacke subscription

Costs depend on the selected provider. Soniox real-time transcription is listed at **about $0.12 per audio hour**, or
**roughly $0.002 per audio minute**. Five hours of processed audio would therefore cost
**about $0.60** at that estimated rate. Actual billing is token-based and
depends on audio and text context. Retries and aborted audio can add usage;
optional text refinement and service infrastructure add separate costs. The
shared provider account is billed to the operator. Local tariff figures are
estimates; the provider's bill remains authoritative.

For comparison, [Wispr Flow Pro](https://wisprflow.ai/pricing) lists **$15 per
user per month**, or **$12 per month billed annually**, checked October 29,
2026. Its free plan lists 2,000 words per week on desktop. These are different
cost models: a paid managed service versus a separately operated app and cloud
account. This comparison is about published pricing; Wispr's recognition
speed and quality have not been measured against this build.

Soniox pricing source: [Soniox API pricing](https://soniox.com/pricing).

### New in 0.7.3: long Gemini dictations, back in seconds

Gemini dictations longer than about four minutes no longer keep loading after
you release the key. Gemini ends a live recording by itself 222 seconds after
it starts (measured against Google's service on November 10, 2026); Laberbacke
now renews the connection every three minutes in the background, so the text
is ready seconds after the last section closes. If a connection drops, long
Gemini recordings are recovered in up to six parallel parts instead of one
slow pass. Gemini is the default model for new accounts; an existing personal
choice stays. Long Soniox recordings recover reliably again and about three
times faster. A real ten-minute Gemini dictation through the app has not yet
been measured; recordings remain capped at 30 minutes.

### New in 0.7.2: your personal choice of transcription model

Choose Gemini, MAI Transcribe or Soniox without an administrator changing the
shared default for everyone. Your selection stays saved for your account on
this Mac. Switching models prepares the next dictation immediately, without
carrying over a failed provider's retry delay. An active recording keeps its
original model, including all sections of a long dictation. Recovered offline
recordings and audio reprocessing use the current choice when they start.

### New in 0.7.1: broader insertion and microphone speaker selection

Native apps, browsers and previously unknown editors now share the additional
Paste-menu route. Laberbacke recognizes more custom text fields and checks the
foreground again while preparing an insertion. Switching apps stops the old
attempt and keeps the complete text available; an ambiguous menu response does
not trigger a duplicate paste.

Soniox speaker labels and microphone levels can now select a clearly stronger
voice over quieter background speakers, without a saved voice profile. If the
evidence is unclear, the full transcript is kept. Loudness is only an
approximation of microphone distance, and overlapping audio is not physically
separated. Synthetic audio checks passed their defined keyword checks; real-office
speech and insertion across third-party editors still need broader practical
validation. This is not a guarantee for every text field.

### The details that matter while dictating

* **Keep dictating while usage records are saved.** Version 0.6.1 moves local
  usage writes off the audio path. A busy database can no longer hold up
  every audio packet; counts stay ordered and normal shutdown waits for them.
* **One completed insertion.** Long recordings rotate streaming connections;
  text is released only after all final sections are confirmed. Incomplete
  output is not inserted as if it were the whole recording.
* **German first, English when selected.** Recognition hints keep German
  sentences German while allowing familiar English product names. Selecting
  only English uses English recognition.
* **Record now, recover later.** Completed offline recordings remain on the
  Mac for transcription after reconnecting. Repeated failures eventually pause
  automatic retries, keeping the recording available for manual recovery.
* **Your text has a recovery path.** History and clipboard recovery remain
  available if a target app does not accept automatic insertion.
* **Automatic updates wait for a quiet moment.** Sparkle verifies signed
  update archives and defers restart while a dictation or insertion is active.

### Requirements and limits

Apple Silicon, macOS 14 or later, a permitted Laberbacke account and microphone
and Accessibility permissions are required. The download does not create an
account or broaden the operator's existing access policy. Internet access is
required for cloud transcription. Builds are self-signed and not notarized; follow
`INSTALLATION.txt` in the release for the first launch.

The MAI option is a **Microsoft public preview without an SLA**. Recognition
quality and time to insertion depend on the recording, network and target app.
No universal millisecond latency is promised. The privacy notice inside the app
describes audio sent to the selected provider, filtered recognition hints, local storage
and optional text processing. Older installations keep their previous speech
path until updated.

Wispr Flow is a trademark of its respective owner. Prices can change.

---

<sub>This repository distributes the built app. Source code lives privately in
`till10k/Laberbacke`. © 2026 Rügamer-Steiner. All rights reserved.</sub>
