# Laberbacke

### Hold a key. Speak. Put your words where you are working.

Laberbacke is a dictation app for Apple Silicon Macs. Hold your recording key,
speak, and release it to insert the completed text into your current app.
Your dictionary, familiar work terms, history and saved recordings stay part
of the same workflow.

Since version 0.6.0, **Microsoft MAI-Transcribe-2-Streaming** is the shared speech
path. Audio streams directly from your Mac to Azure while you speak. Your
Laberbacke account supplies a short-lived access token; you do not configure
or receive the operator's permanent Azure key.

An administrator can switch the shared default to Gemini Streaming and back
without another app download. Updated apps check this setting every 15 seconds;
active dictations finish on their original provider. This is a speech-provider
switch, not a rollback of unrelated application changes.

[**Download the latest release**](../../releases/latest)

### Pay for audio, without a Laberbacke subscription

Microsoft's MAI introductory rate is **$0.54 per audio hour**, or **$0.009 per
audio minute**, through December 31, 2026. Five hours of processed audio would
therefore cost **$2.70** at that rate. Retries and aborted audio can add usage;
optional text refinement and service infrastructure can add separate costs.
The shared Azure subscription is billed to the operator. Local tariff figures
are estimates, and Azure's delayed bill remains authoritative.

For comparison, [Wispr Flow Pro](https://wisprflow.ai/pricing) lists **$15 per
user per month**, or **$12 per month billed annually**, checked October 29,
2026. Its free plan lists 2,000 words per week on desktop. These are different
cost models: a paid managed service versus a separately operated app and cloud
account. This comparison is about published pricing; Wispr's recognition
speed and quality have not been measured against this build.

MAI pricing source: [Microsoft AI](https://microsoft.ai/news/our-first-streaming-transcription-model/).

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
required for MAI transcription. Builds are self-signed and not notarized; follow
`INSTALLATION.txt` in the release for the first launch.

MAI streaming is a **Microsoft public preview without an SLA**. Recognition
quality and time to insertion depend on the recording, network and target app.
No universal millisecond latency is promised. The privacy notice inside the app
describes audio sent to Microsoft, filtered recognition hints, local storage
and optional text processing. Older installations keep their previous speech
path until updated.

Wispr Flow is a trademark of its respective owner. Prices can change.

---

<sub>This repository distributes the built app. Source code lives privately in
`till10k/Laberbacke`. © 2026 Rügamer-Steiner. All rights reserved.</sub>
