# Plan for AITEST-1: Visualización de Hora Actual en Página Estática

## Overview
Create a single `index.html` file that displays the current time in 24-hour format (`HH:MM:SS`) and updates every second using vanilla JavaScript.

---

## Tech Stack
- **HTML5**: Structure and content.
- **Inline CSS3**: Basic styling for layout and readability.
- **Vanilla JavaScript**: Use `Date` object and `setInterval` for real-time updates.

---

## Constraints
1. **Single File**: All code must be contained in `index.html`.
2. **No External Dependencies**: No libraries, frameworks, or external resources.
3. **Real-Time Updates**: Time must refresh every second.
4. **Design**: Clean, centered layout with high contrast and readable sans-serif font.

---

## Implementation Steps
1. **HTML Structure**:
   - Create a `<div>` element to display the time.
   - Add a centered `<h1>` title "Current Time".

2. **CSS Styling**:
   - Use inline CSS for simplicity.
   - Center the content both vertically and horizontally.
   - Ensure high contrast and readability.

3. **JavaScript Logic**:
   - Use `setInterval` to update the time every second.
   - Format the time using `Date` object in 24-hour format (`HH:MM:SS`).

---

## Example Workflow
1. User opens `index.html` in a browser.
2. Page loads with a centered title and initial time.
3. Time updates automatically every second without page reload.

---

## Validation
- Verify the page renders correctly in modern browsers.
- Confirm the time updates every second.
- Ensure the design is clean and accessible.