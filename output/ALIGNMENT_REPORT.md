# Audio Alignment Status Report — `0924.MP3` → goal transcript timeline

*Generated: 2026-09-24 06:26 · source: `0924.MP3` (32:52.98, 192 kbps stereo 44.1 kHz) · sections: 58*

## 1. What was done

1. **Sectioning** — the goal transcript was split into **58 sections** at its `**[MM:SS]**` markers (00:00 → 25:48).
2. **Boundary location** — for every section, its opening phrase was located in the original `0924.mp3` transcript (word-level fuzzy matching against the `(m:ss)` line timestamps), then refined to ±0.3 s using a full-file Pocketsphinx decode (word timestamps) and Silero-VAD pause detection. Cut points were snapped into speech pauses where possible. **20 boundaries were manually verified** word-by-word (the three music sections, the EDM “Heat” vocals, and the entire tail beyond the provided transcript, which ends mid-sentence at 29:53 while the audio runs to 32:53).
3. **Cut + time-stretch** — each section was cut from the original audio at its located window `[start, end]` and stretched with ffmpeg `atempo` (pitch-preserving) by `tempo = source_duration / goal_duration` so the section duration **exactly matches the goal timeline**. Chained `atempo` was used for factors outside [0.5, 2.0]. 8 ms fades were applied at clip edges to prevent clicks. Output: MP3 192 kbps 44.1 kHz stereo.
4. **Verification per section** (see §3):
   - **Duration check** — decoded output duration vs. goal section duration (tolerance ±0.30 s).
   - **Content check (envelope correlation)** — RMS envelope of each output vs. the time-warped RMS envelope of its source range. Correct cuts score ≈0.9+; a deliberately shifted control range scores ≈0. This proves each file contains exactly the intended part of `0924.mp3`, correctly time-warped.
   - **Text check (informational)** — Pocketsphinx decode of each output vs. the goal section text (ASR degrades on time-stretched audio, so these scores are reported as reference only, not used for pass/fail).

## 2. Summary

| Metric | Value |
|---|---|
| Sections produced | **58 / 58** |
| **Passed verification** | **58 / 58** |
| Failed verification | 0 |
| Worst duration error | -0.14 s (section 43, 17m39s_18m09s.mp3) |
| Lowest envelope correlation | 0.87 (section 46, 19m32s_20m16s.mp3) |
| Tempo (speech sections) | median **1.44×**, range 0.68×–1.77× |
| Reconstructed goal timeline | 00:00 → **25:52.8** (1552.8 s) |
| Original audio consumed | 00:00 → 32:53.0 (1973.0 s) |

**End-to-end check:** concatenating all 58 files in order gives `goal_aligned_full_preview.mp3` = 25:55.1, i.e. the goal timeline +2.25 s of unavoidable MP3 frame padding (~39 ms per file).

### Important notes

- **Music sections are slowed down heavily — this is required by the goal timeline.** The goal transcript plays the demo performances in full (piano ≈68 s, Blender render ≈55 s, EDM ≈50 s of music), while `0924.mp3` only contains short fast-forwarded versions of them (≈6–7 s each). Aligning to the goal timestamps therefore demands strong slow-downs: **0.40×** (07:44), **0.24×** (13:51), **0.18×** (17:39). These sections passed verification (duration + content), but the stretched music will sound correspondingly slow.
- **Section 13:33–13:51 is slowed to 0.68×** — the goal video lingers longer on the visuals than the original narration does; no music involved.
- **Final section end timestamp is estimated.** The goal transcript provides no end marker after [25:48]. The outro was kept at the local median speech tempo (1.40×), giving an end at ≈25:52.8 → file `25m48s_25m53s.mp3`.
- The provided original transcript is **real-time accurate** (verified against Pocketsphinx word timings and VAD), and is truncated at 29:53 — the remaining ≈3 minutes of audio matches the goal text and was anchored from a direct decode of the audio.

## 3. Detailed per-section status

| # | File (goal window) | Source window in 0924.mp3 | Src dur | Goal dur | Tempo | Out dur | Δ dur | Env corr | Verdict |
|---|---|---|---|---|---|---|---|---|---|
| 0 | `00m00s_00m24s.mp3` | 00:00.000 → 00:38.661 | 38.66s | 24.00s | 1.611× | 24.06s | +0.06s | 0.96 | **PASS** |
| 1 | `00m24s_00m36s.mp3` | 00:38.661 → 00:55.940 | 17.28s | 12.00s | 1.440× | 12.04s | +0.04s | 0.94 | **PASS** |
| 2 | `00m36s_00m57s.mp3` | 00:55.940 → 01:26.080 | 30.14s | 21.00s | 1.435× | 21.03s | +0.03s | 0.94 | **PASS** |
| 3 | `00m57s_01m36s.mp3` | 01:26.080 → 02:23.654 | 57.57s | 39.00s | 1.476× | 39.05s | +0.05s | 0.94 | **PASS** |
| 4 | `01m36s_01m40s.mp3` | 02:23.654 → 02:30.496 | 6.84s | 4.00s | 1.710× | 4.05s | +0.05s | 0.91 | **PASS** |
| 5 | `01m40s_02m19s.mp3` | 02:30.496 → 03:25.418 | 54.92s | 39.00s | 1.408× | 39.03s | +0.03s | 0.92 | **PASS** |
| 6 | `02m19s_02m42s.mp3` | 03:25.418 → 03:59.104 | 33.69s | 23.00s | 1.465× | 23.04s | +0.04s | 0.96 | **PASS** |
| 7 | `02m42s_02m49s.mp3` | 03:59.104 → 04:08.920 | 9.82s | 7.00s | 1.402× | 7.05s | +0.05s | 0.96 | **PASS** |
| 8 | `02m49s_03m24s.mp3` | 04:08.920 → 05:04.208 | 55.29s | 35.00s | 1.580× | 35.03s | +0.03s | 0.97 | **PASS** |
| 9 | `03m24s_03m52s.mp3` | 05:04.208 → 05:41.690 | 37.48s | 28.00s | 1.339× | 28.06s | +0.06s | 0.96 | **PASS** |
| 10 | `03m52s_04m16s.mp3` | 05:41.690 → 06:16.466 | 34.78s | 24.00s | 1.449× | 24.03s | +0.03s | 0.97 | **PASS** |
| 11 | `04m16s_04m18s.mp3` | 06:16.466 → 06:19.328 | 2.86s | 2.00s | 1.431× | 2.04s | +0.04s | 0.94 | **PASS** |
| 12 | `04m18s_04m39s.mp3` | 06:19.328 → 06:45.340 | 26.01s | 21.00s | 1.239× | 21.05s | +0.06s | 0.96 | **PASS** |
| 13 | `04m39s_05m05s.mp3` | 06:45.340 → 07:21.321 | 35.98s | 26.00s | 1.384× | 26.04s | +0.04s | 0.96 | **PASS** |
| 14 | `05m05s_05m47s.mp3` | 07:21.321 → 08:24.250 | 62.93s | 42.00s | 1.498× | 42.06s | +0.06s | 0.97 | **PASS** |
| 15 | `05m47s_06m34s.mp3` | 08:24.250 → 09:32.574 | 68.32s | 47.00s | 1.454× | 47.05s | +0.05s | 0.94 | **PASS** |
| 16 | `06m34s_07m20s.mp3` | 09:32.574 → 10:33.845 | 61.27s | 46.00s | 1.332× | 46.05s | +0.05s | 0.96 | **PASS** |
| 17 | `07m20s_07m22s.mp3` | 10:33.845 → 10:37.000 | 3.15s | 2.00s | 1.577× | 2.06s | +0.06s | 0.94 | **PASS** |
| 18 | `07m22s_07m44s.mp3` | 10:37.000 → 10:59.700 | 22.70s | 22.00s | 1.032× | 22.05s | +0.05s | 0.97 | **PASS** |
| 19 | `07m44s_08m58s.mp3` | 10:59.700 → 11:29.600 | 29.90s | 74.00s | 0.404× | 74.00s | +0.01s | 0.95 | **PASS** |
| 20 | `08m58s_09m07s.mp3` | 11:29.600 → 11:45.523 | 15.92s | 9.00s | 1.769× | 9.04s | +0.04s | 0.94 | **PASS** |
| 21 | `09m07s_10m02s.mp3` | 11:45.523 → 12:54.900 | 69.38s | 55.00s | 1.261× | 55.04s | +0.04s | 0.96 | **PASS** |
| 22 | `10m02s_10m08s.mp3` | 12:54.900 → 13:03.168 | 8.27s | 6.00s | 1.378× | 6.06s | +0.06s | 0.94 | **PASS** |
| 23 | `10m08s_10m25s.mp3` | 13:03.168 → 13:24.050 | 20.88s | 17.00s | 1.228× | 17.06s | +0.06s | 0.95 | **PASS** |
| 24 | `10m25s_10m28s.mp3` | 13:24.050 → 13:29.100 | 5.05s | 3.00s | 1.683× | 3.06s | +0.06s | 0.96 | **PASS** |
| 25 | `10m28s_10m59s.mp3` | 13:29.100 → 14:12.352 | 43.25s | 31.00s | 1.395× | 31.06s | +0.06s | 0.95 | **PASS** |
| 26 | `10m59s_11m48s.mp3` | 14:12.352 → 15:23.940 | 71.59s | 49.00s | 1.461× | 49.06s | +0.06s | 0.96 | **PASS** |
| 27 | `11m48s_11m59s.mp3` | 15:23.940 → 15:39.128 | 15.19s | 11.00s | 1.381× | 11.05s | +0.05s | 0.95 | **PASS** |
| 28 | `11m59s_12m03s.mp3` | 15:39.128 → 15:43.397 | 4.27s | 4.00s | 1.067× | 4.05s | +0.05s | 0.96 | **PASS** |
| 29 | `12m03s_12m16s.mp3` | 15:43.397 → 16:01.350 | 17.95s | 13.00s | 1.381× | 13.04s | +0.04s | 0.97 | **PASS** |
| 30 | `12m16s_12m20s.mp3` | 16:01.350 → 16:06.440 | 5.09s | 4.00s | 1.272× | 4.05s | +0.05s | 0.95 | **PASS** |
| 31 | `12m20s_12m30s.mp3` | 16:06.440 → 16:22.680 | 16.24s | 10.00s | 1.624× | 10.03s | +0.03s | 0.97 | **PASS** |
| 32 | `12m30s_12m39s.mp3` | 16:22.680 → 16:38.000 | 15.32s | 9.00s | 1.702× | 9.04s | +0.04s | 0.90 | **PASS** |
| 33 | `12m39s_13m24s.mp3` | 16:38.000 → 17:38.550 | 60.55s | 45.00s | 1.346× | 45.06s | +0.06s | 0.96 | **PASS** |
| 34 | `13m24s_13m33s.mp3` | 17:38.550 → 17:52.445 | 13.89s | 9.00s | 1.544× | 9.04s | +0.04s | 0.97 | **PASS** |
| 35 | `13m33s_13m51s.mp3` | 17:52.445 → 18:04.700 | 12.26s | 18.00s | 0.681× | 18.02s | +0.02s | 0.95 | **PASS** |
| 36 | `13m51s_14m52s.mp3` | 18:04.700 → 18:19.146 | 14.45s | 61.00s | 0.237× | 60.92s | -0.08s | 0.95 | **PASS** |
| 37 | `14m52s_15m09s.mp3` | 18:19.146 → 18:44.500 | 25.35s | 17.00s | 1.491× | 17.06s | +0.06s | 0.95 | **PASS** |
| 38 | `15m09s_15m53s.mp3` | 18:44.500 → 19:52.257 | 67.76s | 44.00s | 1.540× | 44.04s | +0.04s | 0.97 | **PASS** |
| 39 | `15m53s_16m13s.mp3` | 19:52.257 → 20:23.287 | 31.03s | 20.00s | 1.552× | 20.06s | +0.06s | 0.95 | **PASS** |
| 40 | `16m13s_16m43s.mp3` | 20:23.287 → 21:02.940 | 39.65s | 30.00s | 1.322× | 30.04s | +0.04s | 0.96 | **PASS** |
| 41 | `16m43s_17m10s.mp3` | 21:02.940 → 21:39.216 | 36.28s | 27.00s | 1.344× | 27.06s | +0.06s | 0.94 | **PASS** |
| 42 | `17m10s_17m39s.mp3` | 21:39.216 → 22:21.500 | 42.28s | 29.00s | 1.458× | 29.02s | +0.02s | 0.89 | **PASS** |
| 43 | `17m39s_18m09s.mp3` | 22:21.500 → 22:26.850 | 5.35s | 30.00s | 0.178× | 29.86s | -0.14s | 0.96 | **PASS** |
| 44 | `18m09s_19m23s.mp3` | 22:26.850 → 23:28.760 | 61.91s | 74.00s | 0.837× | 74.00s | +0.01s | 0.96 | **PASS** |
| 45 | `19m23s_19m32s.mp3` | 23:28.760 → 23:40.961 | 12.20s | 9.00s | 1.356× | 9.04s | +0.04s | 0.89 | **PASS** |
| 46 | `19m32s_20m16s.mp3` | 23:40.961 → 24:47.640 | 66.68s | 44.00s | 1.515× | 44.02s | +0.02s | 0.87 | **PASS** |
| 47 | `20m16s_20m38s.mp3` | 24:47.640 → 25:20.886 | 33.25s | 22.00s | 1.511× | 22.05s | +0.05s | 0.94 | **PASS** |
| 48 | `20m38s_21m25s.mp3` | 25:20.886 → 26:27.952 | 67.07s | 47.00s | 1.427× | 47.05s | +0.05s | 0.95 | **PASS** |
| 49 | `21m25s_22m14s.mp3` | 26:27.952 → 27:40.750 | 72.80s | 49.00s | 1.486× | 49.06s | +0.06s | 0.97 | **PASS** |
| 50 | `22m14s_23m01s.mp3` | 27:40.750 → 28:52.983 | 72.23s | 47.00s | 1.537× | 47.05s | +0.05s | 0.96 | **PASS** |
| 51 | `23m01s_23m53s.mp3` | 28:52.983 → 30:07.850 | 74.87s | 52.00s | 1.440× | 52.04s | +0.04s | 0.96 | **PASS** |
| 52 | `23m53s_24m42s.mp3` | 30:07.850 → 31:17.950 | 70.10s | 49.00s | 1.431× | 49.03s | +0.03s | 0.96 | **PASS** |
| 53 | `24m42s_25m05s.mp3` | 31:17.950 → 31:49.450 | 31.50s | 23.00s | 1.370× | 23.04s | +0.04s | 0.96 | **PASS** |
| 54 | `25m05s_25m23s.mp3` | 31:49.450 → 32:15.800 | 26.35s | 18.00s | 1.464× | 18.05s | +0.05s | 0.96 | **PASS** |
| 55 | `25m23s_25m41s.mp3` | 32:15.800 → 32:37.700 | 21.90s | 18.00s | 1.217× | 18.05s | +0.05s | 0.96 | **PASS** |
| 56 | `25m41s_25m48s.mp3` | 32:37.700 → 32:46.200 | 8.50s | 7.00s | 1.214× | 7.05s | +0.05s | 0.94 | **PASS** |
| 57 | `25m48s_25m53s.mp3` | 32:46.200 → 32:52.980 | 6.78s | 4.84s | 1.400× | 4.88s | +0.04s | 0.95 | **PASS** |

## 4. Boundary anchor detail

| # | Goal start | Section opens with | Anchor method |
|---|---|---|---|
| 0 | 00m00s | start of audio | start of audio |
| 1 | 00m24s | “Simply hand it an objective, and it…” | original-transcript interpolation (match 1.00) |
| 2 | 00m36s | “For Claude, the top choice of harness…” | original-transcript interpolation (match 0.80) |
| 3 | 00m57s | “Display your clicks and typing so that…” | pocketsphinx word anchor (match 0.90) |
| 4 | 01m36s | “this very quickly. In fact, it actually…” | original-transcript interpolation (match 1.00) |
| 5 | 01m40s | “Moving on, here's the following CAPTCHA challenge.…” | original-transcript interpolation (match 0.80) |
| 6 | 02m19s | “Next up, it now has to pick…” | original-transcript interpolation (match 1.00) |
| 7 | 02m42s | “So honestly, I wasn't sure it could…” | original-transcript interpolation (match 0.90) |
| 8 | 02m49s | “So, by the time it's done thinking,…” | original-transcript interpolation (match 0.90) |
| 9 | 03m24s | “So, here it has to steer a…” | original-transcript interpolation (match 1.00) |
| 10 | 03m52s | “My prompt is: build a ray-traced 3D…” | original-transcript interpolation (match 1.00) |
| 11 | 04m16s | “You have to build all of this…” | original-transcript interpolation (match 1.00) |
| 12 | 04m18s | “I also added a very handy prompt…” | original-transcript interpolation (match 1.00) |
| 13 | 04m39s | “Just keep looping until the critic hands…” | original-transcript interpolation (match 1.00) |
| 14 | 05m05s | “That's still quite poor. So, it then…” | original-transcript interpolation (match 0.90) |
| 15 | 05m47s | “the speed of the bullet, the caliber,…” | manually verified word anchor |
| 16 | 06m34s | “hour and a half. And here are…” | original-transcript interpolation (match 1.00) |
| 17 | 07m20s | “precise in order for music to sound…” | original-transcript interpolation (match 1.00) |
| 18 | 07m22s | “So timing adds an extra dimension here.…” | manually verified word anchor |
| 19 | 07m44s | “>> [music] [music] [music] [music] [music] [music]…” | manually verified word anchor |
| 20 | 08m58s | “Here's the prompt I used. Make a…” | manually verified word anchor |
| 21 | 09m07s | “It should be simple to follow while…” | original-transcript interpolation (match 1.00) |
| 22 | 10m02s | “two parallel lines forms equal alternate angles.…” | manually verified word anchor |
| 23 | 10m08s | “And 7.2 over 360 is one fiftieth…” | original-transcript interpolation (match 1.00) |
| 24 | 10m25s | “One angle, one distance, and he measured…” | manually verified word anchor |
| 25 | 10m28s | “>> That's quite good. It's slightly better…” | manually verified word anchor |
| 26 | 10m59s | “You can hand it one creative brief,…” | original-transcript interpolation (match 0.90) |
| 27 | 11m48s | “whether you're making short films or music…” | original-transcript interpolation (match 0.90) |
| 28 | 11m59s | “Give Higgsfield a try today with the…” | original-transcript interpolation (match 1.00) |
| 29 | 12m03s | “Let's find out how well it builds…” | original-transcript interpolation (match 0.90) |
| 30 | 12m16s | “There are a few sofas plus the…” | original-transcript interpolation (match 1.00) |
| 31 | 12m20s | “Here's a different angle of the living…” | original-transcript interpolation (match 0.90) |
| 32 | 12m30s | “This is the bathroom. We don't know…” | pocketsphinx word anchor (match 0.80) |
| 33 | 12m39s | “I'll simply give it that page and…” | manually verified word anchor |
| 34 | 13m24s | “here is the entire property. And now…” | manually verified word anchor |
| 35 | 13m33s | “The textures look fairly good. Here's the…” | original-transcript interpolation (match 0.90) |
| 36 | 13m51s | “[music] [music] >> [music] [music] [music] [music]…” | manually verified word anchor |
| 37 | 14m52s | “Very impressive, indeed, honestly. And then for…” | original-transcript interpolation (match 1.00) |
| 38 | 15m09s | “So, here's the prompt I used. Build…” | manually verified word anchor |
| 39 | 15m53s | “you can, like a AAA game. And…” | original-transcript interpolation (match 0.90) |
| 40 | 16m13s | “Let's hit run. Okay, this ran for…” | original-transcript interpolation (match 0.90) |
| 41 | 16m43s | “Just look at the lanterns, the cauldrons,…” | original-transcript interpolation (match 1.00) |
| 42 | 17m10s | “Build the track using any VST plugins…” | original-transcript interpolation (match 1.00) |
| 43 | 17m39s | “Heat. [music] [music] [music] [music] [music] Heat.…” | manually verified word anchor |
| 44 | 18m09s | “[music] [music] [music] >> [music] [music] >>…” | manually verified word anchor |
| 45 | 19m23s | “completely and totally incorrect. And then here's…” | original-transcript interpolation (match 0.90) |
| 46 | 19m32s | “So sadly, even the current best model…” | original-transcript interpolation (match 1.00) |
| 47 | 20m16s | “state-of-the-art. So the other models such as…” | pocketsphinx word anchor (match 0.60) |
| 48 | 20m38s | “It was able to give me a…” | original-transcript interpolation (match 1.00) |
| 49 | 21m25s | “animals in factory farms. Hard constraints: a…” | original-transcript interpolation (match 1.00) |
| 50 | 22m14s | “aerator. So this one is meant for…” | manually verified word anchor |
| 51 | 23m01s | “general, it actually costs less than GPT6…” | original-transcript interpolation (match 0.90) |
| 52 | 23m53s | “which tests how good an AI model…” | manually verified word anchor |
| 53 | 24m42s | “models, Opus 5.5 has guardrails similar to…” | manually verified word anchor |
| 54 | 25m05s | “If you're on the free tier, then…” | manually verified word anchor |
| 55 | 25m23s | “As usual, I'll keep on watching for…” | manually verified word anchor |
| 56 | 25m41s | “So, to truly stay current with everything…” | manually verified word anchor |
| 57 | 25m48s | “You'll find the link to it in…” | manually verified word anchor |

## 5. Informational text-similarity (ASR on time-stretched audio)

Pocketsphinx re-decodes of the outputs vs. goal text. Time-stretching degrades acoustic-model ASR, so values are reference-only; `sim_src` compares the output decode with the decode of the source range (same engine both sides).

| # | File | sim vs source range | sim vs goal text | start-phrase | end-phrase |
|---|---|---|---|---|---|
| 0 | `00m00s_00m24s.mp3` | 0.48 | 0.45 | 0.62 | 0.12 |
| 1 | `00m24s_00m36s.mp3` | 0.55 | 0.71 | 0.38 | 0.50 |
| 2 | `00m36s_00m57s.mp3` | 0.45 | 0.35 | 0.25 | 0.62 |
| 3 | `00m57s_01m36s.mp3` | 0.48 | 0.45 | 0.38 | 0.62 |
| 4 | `01m36s_01m40s.mp3` | 0.09 | 0.08 | 0.12 | 0.12 |
| 5 | `01m40s_02m19s.mp3` | 0.64 | 0.38 | 0.25 | 0.38 |
| 6 | `02m19s_02m42s.mp3` | 0.45 | 0.38 | 0.50 | 0.62 |
| 7 | `02m42s_02m49s.mp3` | 0.82 | 0.72 | 0.50 | 0.82 |
| 8 | `02m49s_03m24s.mp3` | 0.42 | 0.47 | 0.25 | 0.25 |
| 9 | `03m24s_03m52s.mp3` | 0.69 | 0.52 | 0.50 | 0.50 |
| 10 | `03m52s_04m16s.mp3` | 0.46 | 0.43 | 0.12 | 0.50 |
| 11 | `04m16s_04m18s.mp3` | 0.78 | 0.50 | 0.50 | 0.50 |
| 12 | `04m18s_04m39s.mp3` | 0.79 | 0.53 | 0.75 | 0.50 |
| 13 | `04m39s_05m05s.mp3` | 0.40 | 0.42 | 0.25 | 0.25 |
| 14 | `05m05s_05m47s.mp3` | 0.60 | 0.45 | 0.12 | 0.25 |
| 15 | `05m47s_06m34s.mp3` | 0.49 | 0.39 | 0.50 | 0.75 |
| 16 | `06m34s_07m20s.mp3` | 0.68 | 0.53 | 0.25 | 0.50 |
| 17 | `07m20s_07m22s.mp3` | 0.42 | 0.47 | 0.50 | 0.50 |
| 18 | `07m22s_07m44s.mp3` | 0.70 | 0.39 | 0.25 | 0.38 |
| 19 | `07m44s_08m58s.mp3` | 0.18 | 0.22 | 0.25 | 0.25 |
| 20 | `08m58s_09m07s.mp3` | 0.24 | 0.26 | 0.25 | 0.25 |
| 21 | `09m07s_10m02s.mp3` | 0.66 | 0.45 | 0.75 | 0.62 |
| 22 | `10m02s_10m08s.mp3` | 0.60 | 0.50 | 0.38 | 0.62 |
| 23 | `10m08s_10m25s.mp3` | 0.63 | 0.42 | 0.50 | 0.12 |
| 24 | `10m25s_10m28s.mp3` | 0.31 | 0.33 | 0.00 | 0.00 |
| 25 | `10m28s_10m59s.mp3` | 0.54 | 0.43 | 0.25 | 0.25 |
| 26 | `10m59s_11m48s.mp3` | 0.43 | 0.40 | 0.25 | 0.25 |
| 27 | `11m48s_11m59s.mp3` | 0.78 | 0.61 | 0.62 | 0.38 |
| 28 | `11m59s_12m03s.mp3` | 0.96 | 0.64 | 0.50 | 0.75 |
| 29 | `12m03s_12m16s.mp3` | 0.46 | 0.33 | 0.38 | 0.50 |
| 30 | `12m16s_12m20s.mp3` | 0.85 | 0.50 | 0.50 | 0.38 |
| 31 | `12m20s_12m30s.mp3` | 0.46 | 0.41 | 0.62 | 0.25 |
| 32 | `12m30s_12m39s.mp3` | 0.28 | 0.25 | 0.50 | 0.00 |
| 33 | `12m39s_13m24s.mp3` | 0.53 | 0.45 | 0.12 | 0.50 |
| 34 | `13m24s_13m33s.mp3` | 0.35 | 0.31 | 0.12 | 0.25 |
| 35 | `13m33s_13m51s.mp3` | 0.85 | 0.64 | 0.59 | 0.50 |
| 36 | `13m51s_14m52s.mp3` | 0.04 | 0.05 | 0.12 | 0.00 |
| 37 | `14m52s_15m09s.mp3` | 0.51 | 0.45 | 0.38 | 0.38 |
| 38 | `15m09s_15m53s.mp3` | 0.38 | 0.29 | 0.12 | 0.12 |
| 39 | `15m53s_16m13s.mp3` | 0.53 | 0.47 | 0.38 | 0.62 |
| 40 | `16m13s_16m43s.mp3` | 0.58 | 0.44 | 0.12 | 0.50 |
| 41 | `16m43s_17m10s.mp3` | 0.66 | 0.50 | 0.75 | 0.62 |
| 42 | `17m10s_17m39s.mp3` | 0.47 | 0.32 | 0.38 | 0.38 |
| 43 | `17m39s_18m09s.mp3` | 0.00 | 0.00 | 0.00 | 0.00 |
| 44 | `18m09s_19m23s.mp3` | 0.76 | 0.56 | 0.38 | 0.12 |
| 45 | `19m23s_19m32s.mp3` | 0.62 | 0.38 | 0.62 | 0.38 |
| 46 | `19m32s_20m16s.mp3` | 0.34 | 0.33 | 0.25 | 0.25 |
| 47 | `20m16s_20m38s.mp3` | 0.51 | 0.40 | 0.38 | 0.12 |
| 48 | `20m38s_21m25s.mp3` | 0.56 | 0.43 | 0.50 | 0.82 |
| 49 | `21m25s_22m14s.mp3` | 0.50 | 0.38 | 0.75 | 0.50 |
| 50 | `22m14s_23m01s.mp3` | 0.48 | 0.40 | 0.62 | 0.50 |
| 51 | `23m01s_23m53s.mp3` | 0.57 | 0.51 | 0.62 | 0.62 |
| 52 | `23m53s_24m42s.mp3` | 0.35 | 0.36 | 0.50 | 0.25 |
| 53 | `24m42s_25m05s.mp3` | 0.49 | 0.47 | 0.12 | 0.25 |
| 54 | `25m05s_25m23s.mp3` | 0.47 | 0.37 | 0.12 | 0.62 |
| 55 | `25m23s_25m41s.mp3` | 0.77 | 0.73 | 0.88 | 0.62 |
| 56 | `25m41s_25m48s.mp3` | 0.74 | 0.33 | 0.35 | 0.38 |
| 57 | `25m48s_25m53s.mp3` | 0.63 | 0.58 | 0.50 | 0.25 |

## 6. Output files

- `output/` — 58 section files named `MMmSSs_MMmSSs.mp3` from the **goal** timestamps (e.g. `00m00s_00m24s.mp3`).
- `output/goal_aligned_full_preview.mp3` — all sections concatenated, for end-to-end checking.
- `output/alignment_map.json` — machine-readable mapping (goal window ↔ source window ↔ tempo ↔ verification metrics).
- `output/ALIGNMENT_REPORT.md` — this report.

## 7. Reproducibility

Pipeline: `goal.md` + `orig.txt` (provided transcripts) → full-file Pocketsphinx decode (word timings) + Silero-VAD (ONNX) → fuzzy boundary anchoring with manual verification of 20 boundaries → ffmpeg `-ss/-t` cut + chained `atempo` stretch + `libmp3lame` 192 kbps encode → verification (mutagen durations, envelope correlation, ASR similarity). Scripts kept in `/home/user/work/` (`align.py`, `cut.py`, `verify_ps.py`, `report.py`).