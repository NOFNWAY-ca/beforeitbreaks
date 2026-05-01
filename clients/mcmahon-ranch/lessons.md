# McMahon Ranch Lessons

- Keep the app single-file and field-ready. Preserve offline use and direct-edit simplicity.
- Use the unified `mr_app_v2` storage key and migrate from the old `ranch_*` keys instead of adding new scattered keys.
- Avoid `alert()` and `confirm()`. Use the shared modal and toast helpers for validation, warnings, and destructive actions.
- Medication inventory is tied to treatment records. Editing or deleting a treatment must return the old quantity before applying the new one.
- The service worker is included, but it only registers from an HTTP or HTTPS origin, not when the HTML is opened directly from `file://`.
