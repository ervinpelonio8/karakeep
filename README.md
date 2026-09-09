# PDF highlighting verification

Local desktop Chrome and Android 16/API 36 emulator evidence for issue #836.
The Android screenshots come from a debug APK served by Metro; the floating gear
is Expo developer UI. They are unedited screenshots of the local fixture app.
The fixture contains two text pages with the same sentence and one vector-only page.

Reproduce: upload fixture.pdf, select text and save a color/note; reopen, edit and
delete it; zoom and check the overlay; save the same sentence separately on page 2
and navigate from the Highlights list; check that page 3 has no selectable text.
For a bookmarked-link PDF, host the same fixture on your own test server and bookmark it.
On Android, long-press, adjust the handles, then tap Highlight selected text.
Temporarily interrupt access to the local test server to exercise failed-save and
download retry behavior, then restore it and confirm only one record is saved.

Executed: 455 API tests and 43 web tests, desktop save/reopen/zoom/rotation, and
actual Android create/reopen/edit/delete, handle adjustment, page navigation,
textless page, fallback reader, download/delete failure and retry. Android testing
found and fixed a floating-selection-toolbar obstruction and initial DOM-props race.
Final review added a native owner check and rechecked the owner's selection editor.

Limits: real mobile-browser long-press has not been verified. Phone-width Chrome
checks and automated touch-selection tests passed, but are not real mobile-browser
runtime evidence. Physical devices, iOS, Safari/Firefox, production APK/Next build,
hosted CI and the complete Docker E2E matrix have not been verified.
The viewer displays one page at a time; selections do not span pages. Native
highlighting accepts PDFs up to 25 MiB. No OCR, drawing or embedded annotation export.
