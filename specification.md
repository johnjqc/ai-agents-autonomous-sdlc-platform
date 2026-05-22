# Specification for AITEST-1: Visualización de Hora Actual en Página Estática

## User Story
As a system user, I want to access a static HTML file that displays the current time so that I can quickly view the system time in a direct and simple way.

---

## Acceptance Criteria

### Scenario 1: Basic Page Rendering
- **Given**: The user opens `index.html` in any modern web browser.
- **When**: The page has fully loaded.
- **Then**: A clean layout must be displayed with a centered title reading "Current Time".

### Scenario 2: Time Display and Format
- **Given**: The page is displayed in the browser.
- **When**: The clock text is shown.
- **Then**: The time must follow the 24-hour format (`HH:MM:SS`), e.g., `14:35:08`.

### Scenario 3: Real-Time Update
- **Given**: The user stays on the page without reloading.
- **When**: The system time changes.
- **Then**: The displayed time must update automatically every second using basic JavaScript.

---

## Technical Specifications
- **File**: Single self-contained file named `index.html`.
- **Technologies**: HTML5, inline CSS3, vanilla JavaScript (`Date` object).
- **Design**: Readable sans-serif font, clean background, high-contrast text, and centered layout.

---

## Constraints
- No external dependencies (e.g., libraries, frameworks).
- Pure client-side implementation.