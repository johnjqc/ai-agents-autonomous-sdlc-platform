# Data Model: Current Time Display

## Entities

### System Time
- **Description**: Represents the current local time of the client's machine.
- **Attributes**:
  - `hours`: 00-23 (24-hour format)
  - `minutes`: 00-59
  - `seconds`: 00-59
- **Source**: JavaScript `Date` object.
- **Validation**: Must be formatted as two-digit strings (padded with zeros).
