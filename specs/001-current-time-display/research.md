# Research: Current Time Display

## Technical Decision: Time Update Mechanism

**Decision**: Use `setInterval(updateTime, 1000)` to update the clock.

**Rationale**: 
- `setInterval` is standard for recurring tasks with a specific interval.
- For a simple clock, a 1-second precision is sufficient and doesn't require the high-frequency rendering of `requestAnimationFrame`.
- Minimal overhead and highly compatible across all target browsers.

**Alternatives considered**:
- `requestAnimationFrame`: Better for smooth animations, but overkill for a text update once per second.
- `setTimeout` recursively: Similar to `setInterval`, but slightly more complex to implement for this simple case.

## Technical Decision: Layout Centering

**Decision**: Use CSS Flexbox on the `body` element.

**Rationale**:
- `display: flex; justify-content: center; align-items: center;` is the modern standard for perfect centering.
- Simple to implement with minimal inline CSS.
- Highly compatible and responsive.

**Alternatives considered**:
- Absolute positioning with transforms: Older method, more verbose.
- CSS Grid: Also works, but Flexbox is slightly more intuitive for a single centered container.
