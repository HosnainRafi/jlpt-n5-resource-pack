# JLPT N5 Resource Pack

A complete, organized collection of JLPT N5 study materials, ready for use in apps and websites. It combines full mock tests from nihonez.com, mock tests and quizzes from minnanihongo.com, and the official listening audio for Lessons 1–25 of *Minna no Nihongo Shokyu I* (みんなの日本語初級Ⅰ), the standard beginner textbook that covers the entire N5 syllabus.

A machine-readable catalog of everything in this repository is available at [`index.json`](index.json).

## Repository Structure

```
jlpt-n5-resource-pack/
├── index.json                          # Machine-readable catalog (app-friendly)
├── jlpt-n5-tests/                      # 9 full JLPT N5 tests (nihonez.com)
│   └── <test-slug>/
│       ├── test.json                   # All questions with answers, explanations, audio
│       └── audio/                      # Listening audio files (mp3)
├── minnanihongo-n5-mocks/              # 5 full mock tests (minnanihongo.com)
│   └── n5-mock-{1..5}/
│       ├── n5-mock-{1..5}.json         # Structured questions, transcripts, audio, images
│       ├── <section>/audio/            # Listening audio (mp3)
│       └── <section>/images/           # Question images (jpg/png)
├── minnanihongo-n5-quizzes/            # 112 N5 quizzes with answer keys (minnanihongo.com)
│   ├── grammar/                        # 26 quizzes
│   ├── vocabulary/                     # 23 quizzes
│   ├── kanji/                          # 19 quizzes
│   ├── listening/                      # 43 quizzes
│   └── reading/                        # 1 quiz
├── minna-no-nihongo-listening/         # Official book audio, Lessons 1–25
│   ├── index.json                      # Lesson → track mapping with durations
│   └── lesson-{01..25}/                # 3–5 audio tracks per lesson (87 total)
└── jlpt-official-workbook-vol2-n5/     # Official JLPT Workbook Vol. 2 (2018) – N5
    ├── pdf/                            # All 3 test sections, answer key, scripts
    └── audio/                          # 4 listening audio tracks
```

## Contents Summary

| Collection | Source | Items | Notes |
| --- | --- | --- | --- |
| `jlpt-n5-tests` | [nihonez.com](https://nihonez.com/jlpt-n5-test/) | 9 tests, ~678 questions | Full questions, choices, correct answers, detailed explanations, listening audio |
| `minnanihongo-n5-mocks` | [minnanihongo.com](https://www.minnanihongo.com/jlpt-mock-tests/n5) | 5 mocks, 335 questions | Questions, listening transcripts (scripts), audio, images. Answer keys are not exposed to guest sessions and are therefore not included |
| `minnanihongo-n5-quizzes` | [minnanihongo.com](https://www.minnanihongo.com/quizzes?level=N5) | 112 quizzes | Each quiz has prompts, choices, correct answers, and explanations |
| `minna-no-nihongo-listening` | 3A Corporation (official publisher) | Lessons 1–25, 87 tracks | Official audio of *Minna no Nihongo Shokyu I* 2nd edition |
| `jlpt-official-workbook-vol2-n5` | Japan Foundation / JEES ([jlpt.jp](https://www.jlpt.jp/e/samples/sampleindex.html)) | Full official practice test | Official Workbook Vol. 2 (2018) N5 sections, answer key, scripts, and listening audio |

### N5 Test Collection (nihonez.com)

| Test | Questions |
| --- | --- |
| JLPT N5 Mock Test – July 2024 | 67 |
| JLPT N5 Mock Test – July 2025 | 67 |
| JLPT N5 Mock Test – December 2025 | — (premium content, not included) |
| JLPT N5 Korean Practice Test 1 (2026) | 67 |
| JLPT N5 Mock Test (2010–2011) | 89 |
| JLPT N5 Mock Test – December 2012 | 91 |
| JLPT N5 Mock Test – July 2013 | 91 |
| JLPT N5 Mock Test – July 2017 | 89 |
| JLPT N5 Mock Test – December 2021 | 67 |
| JLPT Practice Workbook Vol. 2 (2018) | 91 |

**Total: 719 questions** (the older official-format mock tests include extra grammar/vocabulary exercises beyond the standard 67-question format)

### Minna no Nihongo Listening (Lessons 1–25)

Tracks follow the official 3A Corporation numbering for *みんなの日本語初級Ⅰ 第2版 本冊音声* (tracks 1–87). Each lesson folder contains its official tracks with durations recorded in `index.json`.

| Lesson | Tracks | | Lesson | Tracks |
| --- | --- | --- | --- | --- |
| 1 | 1–4 | | 14 | 49–52 |
| 2 | 5–8 | | 15 | 53–55 |
| 3 | 9–11 | | 16 | 56–59 |
| 4 | 12–16 | | 17 | 60–62 |
| 5 | 17–20 | | 18 | 63–65 |
| 6 | 21–23 | | 19 | 66–68 |
| 7 | 24–27 | | 20 | 69–71 |
| 8 | 28–31 | | 21 | 72–74 |
| 9 | 32–34 | | 22 | 75–77 |
| 10 | 35–38 | | 23 | 78–81 |
| 11 | 39–42 | | 24 | 82–84 |
| 12 | 43–45 | | 25 | 85–87 |

> The official track counts per lesson (4,4,3,5,4,3,4,4,3,4,4,3,3,4,3,4,3,3,3,3,3,3,4,3,3) sum to 87, matching the full CD set. Exact boundaries are recorded in `minna-no-nihongo-listening/index.json`.

## Data Formats (for App Use)

All test and quiz data is provided as **JSON** with a consistent, app-friendly shape:

```jsonc
// test.json / quiz / mock section question
{
  "question_number": 1,
  "question_type": "kanji_reading",   // e.g. particle_selection, task_based_comprehension
  "prompt": "きのうは 雨が ふっていました。",
  "context": null,                    // reading passage, when present
  "script": "会話テキスト...",         // listening transcript (null for non-listening)
  "audio_url": "https://.../audio.mp3",
  "image_url": "https://.../image.jpg",
  "choices": ["あめ", "かぜ", "はれ", "ゆき"],
  "correct_answer": 0,                // index into choices (quizzes/tests only)
  "explanation": "きのう雨がふっていました。→ あめ"
}
```

Local audio and image assets are stored alongside each test in `audio/` and `images/` subdirectories; remote URLs are kept for convenience. Quizzes additionally expose `correct_answer` (the correct choice text) and `explanation` in their JSON.

## Licensing and Attribution

This repository is a personal study archive. All questions, audio, and images remain the property of their respective owners:

- **nihonez.com** – test content (nihonez.com)
- **minnanihongo.com** – mock tests and quizzes (minnanihongo.com)
- **3A Corporation** – *Minna no Nihongo* listening audio (official free download, [3anet.co.jp](https://www.3anet.co.jp/np/en/resrcs/230020/))

Use these materials for personal study or in apps with appropriate attribution and in accordance with each source's terms of service. Note that the official JLPT Workbook listening audio contains third-party works; see `jlpt-official-workbook-vol2-n5/README.md` for details.

## Other Useful N5 Mock Test Resources (not included)

If you want even more practice, these external sources were identified during research:

| Resource | What it offers |
| --- | --- |
| [jlpt.jp – Let's Try Sample Questions](https://www.jlpt.jp/e/samples/forlearners.html) | Official interactive sample questions for each N5 item type |
| [jlpt.jp – Official Sample Questions (2009)](https://www.jlpt.jp/e/samples/sample09.html) | Free PDF full test, answer list, and audio in the pre-2010 format |
| [migii.net N5 Mock Tests](https://jlpt.migii.net/en/mock-test/jlpt-n5) | Free online N5 mock tests with daily practice |
| [migii.net – Free N5 PDF](https://migii.net/en/blog/jlpt-n5-test-practice) | Free downloadable full N5 practice test PDF with answers |
| [jlptbooks.com Practice Test](https://www.jlptbooks.com/jlpt-n5-practice-test/) | Free 10-question mini test plus mock exam links |
| [Nihongo Master N5 Test](https://www.nihongomaster.com/jlpt-n5-practice-test) | Free 25-question beginner practice test |
| [japanesetest4you.com](https://japanesetest4you.com/) | Hundreds of practice tests, including kanji and grammar tests for N5 |
| [r/jlpt past-paper collection](https://www.reddit.com/r/jlpt/comments/1gty1tv/jlpt_n1_n5_past_paper/) | Community Google Drive with past-style N5 papers (2010–2017) |
| Japan Times "JLPT N5" study guide | Commercial book with five full practice tests |

> Note: the JLPT has never officially released past exam papers. The only full official practice content is the two Official Practice Workbooks (2012 and 2018); the Vol. 2 N5 content is included in this repository, and the 2009 sample questions (pre-2010 format) are available free from jlpt.jp.
