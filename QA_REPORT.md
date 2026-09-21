# Independent Android QA sample — two real devices

**Application:** Fossify Calculator 1.4.0  
**Devices:** Samsung Galaxy M51 and Redmi Note 9 Pro Max  
**Test period:** 19–20 September 2026, India. **Scope:** selected repeatable checks, not full-app certification or an affiliation with the app developer.

## Real-device functional verification

| Scenario | M51 | Redmi Note 9 Pro Max |
|---|---|---|
| Addition: 7 + 8 | 15 — PASS (earlier verified) | 15 — PASS (earlier verified) |
| Subtraction: 9 - 4 | 5 — PASS | 5 — PASS |
| Multiplication: 6 × 7 | 42 — PASS | 42 — PASS |
| Division: 8 ÷ 2 | 4 — PASS | 4 — PASS |
| Decimal addition: 1.5 + 2.25 | 3.75 — PASS | 3.75 — PASS |
| Negative result: 3 - 8 | -5 — PASS | -5 — PASS |
| Decimal division: 9 ÷ 4 | 2.25 — PASS | 2.25 — PASS |

The six new cases on each phone were run on the real UI using input locations read from Android UI hierarchy. Expressions and results were checked in subsequent XML. Each new case has cleared, expression and result screenshots. Across four runs, 36 private PNGs and 24 XML files passed SHA-256 checks. Addition is an earlier separately verified direct run. Arithmetic direct runs do **not** have CI Job IDs.

## Lifecycle and controlled CI workload

| Bounded check | M51 | Redmi Note 9 Pro Max |
|---|---|---|
| Home → app return | Job #230, DONE/PASS; app PID unchanged | Job #231, DONE/PASS; app PID unchanged |
| 30-minute controlled CI stress | Job #225, PASS; 1,801.91s; 97 metrics samples; 13 verified workload receipts | Job #235, PASS; 1,801.60s; 120 metrics samples; 14 verified workload receipts |
| Process-absent cold launch | Job #228, PASS | Direct approved test PASS; process absent before launch, Android TotalTime 316ms (single run, no CI Job ID) |

The stress runs used a bounded CI/host workload with periodic device/UI checks, **not** 30 minutes of continuous tapping and not a normalized phone-speed benchmark. Recorded device temperature was 34.8–35.4°C on M51 and 35.4–35.6°C on RN9. Laptop CPU samples reached 100%; laptop temperature was not available, so no measured laptop thermal claim is made. M51 ran on 19 September; RN9 ran on 20 September. Earlier blocked/failed attempts are preserved in private CI history; only the named PASS receipts support this table.

## Static accessibility and diagnostic observations

Earlier static UI XML checks found 16/16 target controls with text or content descriptions and 16/16 target bounds at least 48dp per phone. On M51, a user subsequently listened to TalkBack and confirmed correct spoken names for a sampled traversal of numeric, operator, and toolbar controls. The reported label sequence is not a system audio recording or a complete per-swipe accessibility-focus trace. One reported "Unlabeled" announcement remains an unconfirmed container-versus-button investigation, not a verified button defect. RN9 live spoken output was later confirmed by the user in a separate sampled follow-up; full focus-order tracing and whole-app WCAG conformance were not performed. Short diagnostic samples (~27–28 seconds) showed no matching target-app crash/ANR markers, which cannot establish crash-free operation.

## Evidence, limits, and independence

The attached sanitized screenshots show selected actual calculator results with the phone status/navigation bars cropped away. Originals remain private. See `CASE_MATRIX.csv` for per-case status, method, and CI Job ID scope; see `EVIDENCE_MANIFEST_SHA256.txt` for hashes of release files. Private UI dumps, serials, logs, user-account content, and full device screenshots are excluded.

This is an independent practice QA portfolio artifact based on an installed third-party application. It does **not** imply employment by or endorsement from its developer, comprehensive app certification, comparative performance ranking, or completion of the unrun accessibility cases. No phone data wipe, uninstall, factory reset, ROM change, laptop restart, antivirus disable, or screen/sleep-setting change was part of this release work. No public profile or website was updated by preparing these files.

## Supplemental sampled color-contrast check

Four pixel-pair contrast ratios were measured from previously captured cropped screenshots. See `CONTRAST_SAMPLED_ONLY.md` for measured values, method and limitations. **A complete contrast or WCAG audit remains NOT_RUN.**

## Remaining limitations and live M51 TalkBack follow-up

RN9 live speech was initially NOT_RUN; official TalkBack and Google TTS were subsequently installed and sampled speech was user-confirmed, as described in the latest follow-up. The M51 user personally reported that TalkBack correctly spoke Calculator buttons, including an extended traversal through number keys, operators, and toolbar actions. These are **USER_VERIFIED_SAMPLE** spoken-label observations, not independently captured voice or an exhaustive screen-reader audit. The user also heard "Unlabeled" in one traversal. A subsequent read-only UI inspection found one unnamed focusable ScrollView container, but no evidence linking that specific container to the announcement or establishing an unlabeled calculator key. The later user assessment was that M51 spoke correctly. Treat this as **REPRODUCTION_PENDING**, not a confirmed defect or a confirmed pass for every screen-reader element.

TalkBack was turned off at the user's request after testing. Read-back confirmed all three original M51 secure Accessibility values: enabled services `null`, accessibility enabled `0`, touch exploration enabled `0`. The four sampled color-contrast pixel pairs are not a whole-screen or WCAG audit. RN9 cold start was separately completed with user authorization, as detailed above. Neither device was reset or wiped; no antivirus or Windows sleep/display settings were changed.

This remains a bounded independent practice sample. No public profiles or websites were updated, and no claim of app-developer endorsement is made.

## Additional verified functional and static checks

Scope: Fossify Calculator 1.4.0 on Samsung Galaxy M51 and Redmi Note 9 Pro Max only. Evidence is private and verified with SHA-256; this public package includes the case matrix and only four previously privacy-cropped screenshots. Direct new tests have no CI Job IDs.

| Bounded check | M51 | Redmi Note 9 Pro Max |
|---|---|---|
| 0 ÷ 5 | Result 0 — PASS | Result 0 — PASS |
| 12 × 12 | Result 144 — PASS | Result 144 — PASS |
| 9 ÷ 0 then equals | The result field displayed `9÷0`; OBSERVED_ONLY, no assumed correct error requirement | The result field displayed `9÷0`; OBSERVED_ONLY, no assumed correct error requirement |
| Recovery after 9 ÷ 0 | Clear current expression, 2 + 2 = 4, same app PID — PASS | Clear current expression, 2 + 2 = 4, same app PID — PASS |
| Static currently visible Calculator controls | 20/20 keys have text/description; 23/24 interactive/focusable nodes named — PASS_STATIC_ONLY | 20/20 keys have text/description; 23/24 interactive/focusable nodes named — PASS_STATIC_ONLY |

The unnamed focusable element on each device is `org.fossify.math:id/main_nested_scrollview`, a ScrollView container, not a calculator key. This is a candidate for the M51 user's earlier "Unlabeled" spoken item, **not proven to be that accessibility-focus target or a confirmed defect**. M51 sampled TalkBack spoken-label checking was user-verified and TalkBack was disabled afterward; the original three secure Accessibility settings were restored. RN9 has no suitable screen-reader identified in a read-only installed-package/service inventory, so RN9 live screen-reader speech and focus tests remain NOT_RUN. Installing or enabling a new screen reader was outside these bounded checks.

A full WCAG/whole-screen contrast audit, every possible input and unit conversion, extended real-device continuous-interaction stress, every locale/orientation, and independently recorded screen-reader focus traces are NOT_RUN. Earlier 30-minute CI workload tests were periodic device checks under CI/host workload, not 30 minutes of nonstop Calculator taps. No reset, app data wipe, uninstall, laptop restart, antivirus disable, phone ROM/network change, or Windows screen/sleep change was performed. Earlier trial failures remain in private job history; this public package makes no blanket crash-free or full-app certification claim.


## Live RN9 screen-reader follow-up — 20 September 2026

Google LLC Android Accessibility Suite (TalkBack 17.0.1) and Google LLC Speech Recognition & Synthesis were installed via their official Play Store listings, with Play Store temporarily enabled then restored to disabled. An initial TalkBack session did not speak because the RN9 lacked an available text-to-speech service; Google TTS was then installed and selected. Android subsequently reported the TalkBack spoken-feedback service enabled/bound, touch exploration on and Calculator foreground. **User confirmed that TalkBack now speaks and works well**: this is USER_VERIFIED_SAMPLE, not a captured recording or a fully mapped per-swipe focus-order test. The RN9 full-screen accessibility/WCAG audit remains NOT_RUN. TalkBack is left ON awaiting user's decision about restoring settings. The newly installed official Android Accessibility Suite and Google TTS are not uninstalled.

M51 user clarification: the earlier “Unlabeled” utterance occurred after touching blank space, not a Calculator button. This is USER_CLARIFIED_NON_BUTTON; no Calculator button defect has been established and the earlier unnamed focusable ScrollView was not independently linked to an accessibility-focus event. M51 baseline Accessibility settings remain restored. No public account or website was updated.


## September 20, 2026 final post-test correction
RN9 TalkBack was turned OFF at the user's request and its original three Accessibility settings were verified restored (enabled_accessibility_services=null, accessibility_enabled=0, touch_exploration_enabled=0). The two official Google applications remain installed; Play Store was returned to disabled. This supersedes earlier interim statements that RN9 TalkBack was left ON. The user's spoken-audio check covered sampled Calculator navigation, not complete focus order or WCAG conformance.

## Four additional bounded real-device regression cases
On M51 and RN9, 25+17=42 and 8-3=5 passed independently. RN9 regression was tested in its observed landscape UI, without changing its rotation setting. Results and private original screenshots/XML are on the owner's computer; SHA-256 was verified before inclusion in this matrix. No CI Job IDs were generated for these direct runs. Earlier temporary blocked attempts were test-harness orientation, connection or expression-format issues, not confirmed app failures.
