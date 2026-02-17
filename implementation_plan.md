# Implementation Plan - Mobile "Zoom Out" Responsiveness

The user wants the website to look identical on mobile as it does on desktop, just "zoomed out" to fit the screen. This is because the layout is tightly coupled to background images with "frames".

## Current Issues
- `clamp()` minimums prevent text from scaling down enough on small screens.
- `aspect-ratio: 16/9` on `100vw` containers makes sections very short on mobile.
- Header and Footer elements overlap because they don't have enough width.

## Proposed Solution: Global Scaling
Instead of rewriting all CSS for responsiveness, we will implement a global "zoom" or "scale" that forces the desktop layout (1200px width) to fit the mobile screen width.

### Steps
1. **Reset Viewport**: Set viewport to `width=device-width, initial-scale=1` to ensure we get the real device width.
2. **Body/HTML Styling**: 
   - Set `min-width: 1200px` on the body to prevent wrapping.
   - Set `overflow-x: hidden` to prevent scrollbars.
3. **Scaling Script**: 
   - Add a small inline script in `index.html` that uses `document.documentElement.style.zoom` (or `transform: scale`) to fit the 1200px width into the actual screen width.
   - `zoom` is generally smoother for this as it doesn't leave layout gaps, but we need to ensure compatibility.

### Why this works
- It preserves the exact layout ratios.
- All absolute positioning with percentages will remain perfectly aligned with the background image frames.
- It fulfills the specific user request to "zoom out".

## Testing
- Verify on mobile (390px width).
- Verify on tablet (768px+).
- Ensure desktop (1200px+) remains unchanged.
