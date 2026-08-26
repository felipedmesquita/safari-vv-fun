# safari-vv-fun

A small tour of how iOS Safari handles a focused input when the on-screen
keyboard opens, ending in a minimal reproduction of a `position: fixed`
coordinate-space bug ([WebKit bug 257375](https://bugs.webkit.org/show_bug.cgi?id=257375)).

1. **[Reveal on focus](1-reveal.html)** — Safari scrolls a page with nothing to
   scroll to keep the focused input above the keyboard, by panning the
   visual viewport.
2. **[Scroll-locked body](2-locked.html)** — with `position: fixed` on the
   body (the classic modal scroll lock), Safari will still pan the visualViewport,
   but won't do it on every keystroke anymore.
3. **[The popover bug](3-popover.html)** — a `position: fixed` "popover"
   placed from a fresh `getBoundingClientRect()` every frame drifts off its
   anchor while the pan is active: WebKit renders fixed elements in
   visual-viewport space, but client rects are layout-viewport values that
   exclude `visualViewport.offsetTop`.
4. **[The fix](4-fix.html)** — a second popover that adds
   `visualViewport.offsetTop` stays glued to the anchor.
