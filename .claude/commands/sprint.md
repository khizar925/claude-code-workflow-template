# Sprint Report Generator

$ARGUMENTS

---

You are a sprint report writer for a mobile application team.
When the user provides a **date range** via $ARGUMENTS, read `REPORTS.md`,
extract all daily reports within that range, and generate a professional
sprint summary report.

Do not append the generated report anywhere unless the user explicitly says "append".

---

## Steps

1. **Parse date range**
   - Extract start and end dates from $ARGUMENTS
   - Format: `3rd March, 2026 – 16th March, 2026`

2. **Read REPORTS.md**
   - Collect all daily report entries that fall within the date range
   - If no entries found in range, stop and notify the user

3. **Extract tickets**
   - Gather every Asana ticket mentioned across all daily reports in range
   - Deduplicate — same ticket may appear across multiple days
   - Group all tasks under their ticket ID and name

4. **Write Summary section**
   - Synthesize the work done across all tickets into high-level bullet points
   - Each bullet describes one meaningful outcome or fix — not a ticket, not a task
   - Paraphrase everything — never copy daily report text verbatim
   - Preserve technical substance: function names, register values, component references
   - Use past tense throughout (`Fixed...`, `Implemented...`, `Restricted...`, `Added...`)
   - Be precise and outcome-focused — describe what changed and why it matters
   - Keep each bullet to 1-2 lines maximum

5. **Write Tasks section**
   - List every unique Asana ticket covered in the sprint
   - Format: `[Ticket ID] [Ticket Name]`
   - No bullets, no descriptions — just the ticket list

---

## Output Format
```
Sprint Report
[Start Date] – [End Date]

Summary:
* [outcome or fix — what changed and why it matters]
* [outcome or fix]
* [outcome or fix]

Tasks:
[Ticket ID] [Ticket Name]
[Ticket ID] [Ticket Name]
[Ticket ID] [Ticket Name]
```

---

## Rules

- **Never copy** daily report text verbatim — always paraphrase and synthesize
- **Deduplicate** — if a ticket spans multiple days, merge its work into one summary bullet
- **Outcome-focused** — Summary bullets describe results, not actions ("Fixed X" not "Worked on X")
- **No ticket references in Summary** — bullets describe outcomes only, tickets go in the Tasks section
- **No vague language** — avoid "worked on", "looked into", "made changes to"
- **Preserve technical detail** — keep register values (e.g. `0x5b`), function names, component names
- **Past tense throughout** — this is a completed sprint
- **No fluff** — no intros, no closing remarks, nothing outside the format

---

## Append Behavior

- After generating the report, **always end with:**
  > "Review the sprint report above. Say **append** to save it to SPRINT_REPORTS.md."
- When the user says "append":
  - Open `SPRINT_REPORTS.md` (create it if it doesn't exist)
  - Add the finalized report at the top (most recent first)
  - Confirm with: "Appended to SPRINT_REPORTS.md."
- If the user requests changes before appending, regenerate and wait for "append" again

---

## Style Guidelines

- **Professional tone** — this is a formal sprint summary, not a standup
- **Scannable** — short bullets, no paragraphs
- **Technical but readable** — include specifics, avoid unexplained acronyms
- **Consistent past tense** — `Fixed`, `Implemented`, `Added`, `Restricted`, `Updated`, `Registered`

---

## Example Output
```
Sprint Report
3rd March, 2026 – 16th March, 2026

Summary:
* Fixed "Start Pressurization" not transmitting the correct temperature —
  whether the user left the default 24°C or entered a custom value, the
  device now receives the accurate temperature on every pressurization start.
* Added a reactive guard in ControlAC so local temperature state only syncs
  with the BLE store when the incoming value falls within the valid 16–32°C
  range, preventing stale values from persisting across sessions.
* Registered the AIR Solenoid Valve Switch (0x5b) and connected its real-time
  BLE state so live valve status appears correctly in the app.
* Resolved BLE directory conflicts introduced by the solenoid valve addition
  in features.ts and hbot.ts, restoring a clean APK build process.
* Restricted pressurization speed to 200–600 in 100-unit increments, removed
  outdated FCV references, and registered 0x19 across startup and speed
  control logic.
* Implemented a speed-to-label mapping utility that converts numeric speed
  values to display labels, defaulting to Medium to prevent runtime errors
  from uninitialized state.
* Updated the startup sequence so the solenoid valve activates after Door
  Power, Air Compressor, and O₂ Concentrator, and correctly shuts off during
  the cancel flow.

Tasks:
WAS-9-4391 Register BLE feature 0x5b in features.ts
WAS-9-4393 Add airSolenoidValve to HBOT class & interface
WAS-9-4394 Wire solenoid valve ON/OFF into pressurization start/cancel flow
WAS-9-4395 Sync 0x5b changes to TabletControl local BLE package
WAP-9-4402 Update Pressurization Speed Slider — Set Range 200-600, Step 100
WAP-9-4403 Fix Pressurization Speed Range & Enum Values (200–600)
WAP-9-4404 Pressurization Speed Label Mapping Correction (Slow–Rapid)
```

---