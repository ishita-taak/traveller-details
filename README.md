# Fly Fairly — Traveller Details

*Senior Product Designer Take-Home Assignment*

---

## Description

Fly Fairly is a modern flight booking platform focused on speed, clarity, and conversion. This prototype addresses one of the platform's highest-friction screens — the Traveller Details step for multi-passenger international bookings.

The design solves three core problems: cognitive overload from seeing all passengers at once, input errors that cause airline rejections and ops escalations, and user drop-off that occurs immediately before payment — the most expensive place in the funnel to lose a user.

**Key features:**

- One-traveller-at-a-time accordion stepper — reduces perceived form length
- Full APIS compliance — all 7 mandatory fields per passenger for international travel
- Dual-layer progress indicators — macro (booking journey) and micro (this page)
- Blur-only inline validation with dirty/touched state logic
- Cross-field validation — passport expiry checked against travel date
- Age validation per passenger type — adults (12+), children (2–11), infants (<2)
- Frequent flyer number validation per airline format
- Gradient progress bar on sticky bottom bar tied to card completion
- Smart defaults — India pre-selected for nationality and country of issue

---

## Installation

This prototype runs entirely in the browser with no build step, no framework, and no dependencies to install. Everything is vanilla HTML, CSS, and JavaScript.

### Prerequisites

- Any modern browser (Chrome, Safari, Firefox, Edge)
- A local server to avoid CORS issues with font imports (optional but recommended)

### Option 1 — Open directly

The simplest way. No server needed.

```bash
# Clone or download the project folder
# Open the file directly in your browser
open traveller-details.html
```

### Option 2 — Run with a local server (recommended)

Ensures Google Fonts and all assets load correctly.

```bash
# Using Python (comes pre-installed on most systems)
cd path/to/project
python3 -m http.server 8080

# Then open in browser
http://localhost:8080/traveller-details.html
```

```bash
# Alternatively, using Node.js
npx serve .

# Then open in browser
http://localhost:3000/traveller-details.html
```

### Project structure

```
fly-fairly/
├── traveller-details.html   # Main prototype file
├── design-system.css        # All design tokens and component styles
└── preview.html             # Design system token preview page
```

> All styles, logic, and markup are self-contained. The `design-system.css` file defines every colour, spacing value, border radius, and component token used across the prototype. No external CSS framework is used.

---

## Usage

### Running the prototype

Open `traveller-details.html` in a browser. The prototype simulates a DEL → LHR booking for 4 passengers (2 adults, 2 children aged 10).

### Interacting with the form

1. Review the flight summary card and contact details at the top
2. Expand the Adult 1 card — it opens automatically on load
3. Fill in each field — validation fires on blur (when you leave a field)
4. Save the card — the next traveller card auto-expands
5. Watch the gradient progress bar on the sticky bottom bar fill as each card is completed
6. Once all 4 travellers are saved, the Next button becomes active

### Testing validation edge cases

These specific inputs are worth testing to see error handling in action:

- Type a number in a name field — error fires immediately on keystroke
- Enter a single letter in a name field and tab away — minimum length error on blur
- Enter a passport expiry date before 1 May 2026 — cross-field validation error
- Enter a DOB that makes an adult under 12 — age validation error
- Enter a DOB that makes a child under 2 — infant classification error
- Enter month 13 in an expiry date field — fires as soon as both month digits are entered
- Check the frequent flyer checkbox, select IndiGo, enter letters — format error
- Check the frequent flyer checkbox and try to save without filling airline or number — both fields error simultaneously
- Tab through all fields without filling anything, then tap Save — required errors appear only at that point

### Viewing the design system

Open `preview.html` in a browser to see all design tokens rendered — colours, typography scale, spacing values, border radii, and component states.

---

## Design decisions

### 1. Reduce visual clutter

De-cluttering was applied throughout to highlight what is important and reduce noise at every level.

- Simplified the flight details card UI for easier scanability — route, time, and airline are immediately readable without competing elements
- Removed adult/child type pills from traveller cards to reduce the number of colours and labels on screen at any one time
- Baggage information removed from traveller cards entirely — it belongs in a separate step and conflating it with identity details creates unnecessary cognitive load
- Hint text and error messages share the same space below each field — hint text stays visible even during an error state because it is most useful precisely when something is wrong

### 2. Dual-layer progress for better orientation

Two levels of progress indicators answer different user anxieties simultaneously.

- **High-level stepper:** three steps (Traveller Details → Add-ons → Payment) give the user a map of the overall journey. Knowing there are only 3 steps total reduces abandonment anxiety.
- **Page-level progress bar:** a gradient fill line on the sticky bottom bar fills progressively as each traveller card is saved (25% → 50% → 75% → 100%). This answers the question "how much of this page is left" with a 2-second glance.

The two indicators are intentionally placed at different positions — the stepper at the top as a persistent orientation anchor, the gradient bar at the bottom near the primary CTA where the user's attention naturally falls before tapping Next.

### 3. Proactively handle edge cases and errors

Given this is a form-heavy screen, the experience is designed to minimise user effort and prevent errors upfront.

- Inline validation fires on blur only — errors appear when a user leaves a field, not while typing, preventing the most common form frustration of being penalised mid-thought
- On-keystroke errors for character-type violations only — typing a number in a name field errors immediately because it is unambiguously wrong, not a matter of incompleteness
- Dirty/touched state logic — empty fields never show errors on page load or initial focus
- Passport expiry cross-validated against travel date — catches a real airline rejection scenario before payment
- Age validation per passenger type with specific messages for each case including a dedicated infant error for under-2s

---

## Bold idea — traveller delegation via shareable link

> The biggest root cause of multi-passenger drop-off is not UX friction — it is information unavailability. The trip organiser does not have everyone's passport numbers memorised.

Each unfilled traveller card shows an "Ask them to fill this" button. Tapping it generates a unique link the organiser shares via WhatsApp. The co-traveller opens the link, fills only their own details, and the card auto-completes in the organiser's session.

The organiser sees a live completion status for all 4 travellers and can nudge co-travellers directly from the booking screen. This removes the information bottleneck entirely — redistributing the task to the people who actually hold the data — and works natively with WhatsApp, which is how most Indian families coordinate travel.

---

## Contributing

This is a take-home assignment prototype and is not open for external contributions. If you are reviewing this as part of the Fly Fairly hiring process and have feedback, please share it directly.

If you are forking this for your own use, the design system tokens in `design-system.css` are the right place to start for visual customisation. All component styles reference these tokens — changing a token updates every component that uses it.

---

## License

This project is submitted as part of a design assignment for Fly Fairly and is not licensed for redistribution or commercial use.

The prototype code is written from scratch and does not include any third-party libraries. The Poppins typeface is served via Google Fonts under the Open Font License. Inline SVG icons are derived from Google Material Symbols under the Apache License 2.0.

---

*Fly Fairly — Traveller Details Prototype*
