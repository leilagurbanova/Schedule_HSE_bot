# Schedule_HSE_bot

Telegram bot that automates participant registration for cognitive science
experiments at HSE. Removes the manual back-and-forth between researcher,
participant, and the lab booking system.

## Why

Recruiting participants for an experiment usually means:
1. Researcher checks the lab booking system, finds free slots.
2. Participant gets contacted by email or messenger, picks a slot.
3. Researcher manually registers the participant on the booking system.

Steps 1 and 3 are pure overhead - the bot eliminates them.

## What it does

- **Reads available slots** from the [LabShake](https://labshake.org/) booking
  system by driving a real browser session (Playwright) and parsing the DOM.
- **Sends free slots to the participant** via Telegram.
- **When the participant picks a time**, the bot automatically registers them
  on LabShake - no researcher action required.
- The participant gets a confirmation; the researcher's calendar is filled
  without manual work.

## Stack

- **Python**
- **Playwright** - browser automation, used both to read available slots and to
  submit registrations on LabShake.
- **Telegram Bot API** - participant-facing interface.

## How it works

```
   ┌──────────────┐    Playwright    ┌──────────┐
   │  LabShake    │ ◄──────────────► │   Bot    │
   │ (booking UI) │   read + write   │          │
   └──────────────┘                  └────┬─────┘
                                          │ Telegram Bot API
                                          ▼
                                   ┌──────────────┐
                                   │ Participant  │
                                   │   (Telegram) │
                                   └──────────────┘
```

The bot polls LabShake for free experiment slots, formats them, and offers them
to the participant. On selection, it submits the registration form on LabShake
on the participant's behalf.

## Status

Personal project, built to solve a real recruiting bottleneck in a research
lab. Used at HSE.

---

**Author:** Leila Gurbanova
