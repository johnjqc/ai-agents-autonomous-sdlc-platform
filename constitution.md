# Minimal Constitution: Current Time Display (PoC)

## Objective
Create a single `index.html` file that:
1. Displays the current time in **24-hour format (HH:MM:SS)**.
2. Updates the time **every second** using vanilla JavaScript.
3. Shows a centered title: **"Current Time"**.

## Requirements
- **File**: `index.html` (self-contained, no external dependencies).
- **Technologies**: HTML5, inline CSS, vanilla JavaScript (`Date` object).
- **Design**: Basic layout with readable sans-serif font, clean background, and high-contrast text.

## Acceptance Criteria
1. **Page Rendering**: Displays a centered title "Current Time" when opened in a browser.
2. **Time Format**: Shows time in **24-hour format (HH:MM:SS)**.
3. **Real-Time Update**: Updates time automatically every second.

## Constraints
- **No external libraries or dependencies**.
- **Minimal styling**: Only enough to meet basic readability.
- **Vanilla JavaScript**: Use `setInterval` and `Date` object.

## Example Structure
```html
<!DOCTYPE html>
<html>
<head>
    <title>Current Time</title>
    <style>
        body { font-family: Arial; text-align: center; }
    </style>
</head>
<body>
    <h1>Current Time</h1>
    <div id="time">00:00:00</div>
    <script>
        // Update time every second
    </script>
</body>
</html>
```