# street-rescue
# Street Rescue

A field notebook for people who pick up street dogs. Log a dog at the roadside in about thirty seconds, follow it through treatment, and print an adoption poster when it is ready for a home.

The whole app is a single HTML file. No server, no database, no build step, no dependencies to install. Open it and it works.

**Live site:** https://your-username.github.io/street-rescue/

---

## What it does

**Report a dog in the street.** Urgency, location, what is wrong, an optional photo. A button pins your GPS coordinates so someone else can find the same spot, and the case detail links out to maps.

**Follow a case through five stages** — reported, picked up, in treatment, ready to adopt, adopted. Each case keeps a care log you add to as things happen: vet visits, medicines, deworming, vaccinations.

**Set follow-ups.** Give a case a date and a note, like a second vaccination or a dressing change. Overdue ones turn red on the card, today's turn amber, and the overview lists what is actually due.

**Track what you spend.** Log vet fees and medicines against each dog. The app totals it per case, all-time, and over the last thirty days — the figures you need when asking a shelter or a donor for help.

**Print an adoption poster.** One A4 sheet per dog with the photo, age, health status, your story about the dog and your phone number.

**Share a case as text**, ready to paste into WhatsApp or read down the phone to a vet.

**Keep the numbers you call** — vets, shelters, volunteers, the animal ambulance — with tap-to-dial, stored on the device so they work with no signal.

**See where you stand.** Counts by stage, a six-month chart of reports against adoptions, vaccination and sterilisation cover, average days in care.

Dogs logged without a photo get a coat-coloured portrait drawn from their own record, so a list of eight cards stays scannable instead of showing eight identical grey boxes.

## Getting started

Download `index.html` and open it in any browser. That is the entire installation.

Sample cases load on first run so you can look around — eight dogs across all five stages, with care logs, costs and follow-ups, plus four contacts. When you start using it for real, tap **Clear samples**. That removes only the samples and never touches a case you entered. You can load them again from the Backup panel.

Keyboard shortcuts: `n` opens a new report, `/` jumps to search, `Esc` closes any panel.

## Where your data lives

In your own browser, on your own device. Nothing is uploaded, there is no account, and no analytics run.

Two consequences worth understanding:

- **Clearing site data erases everything.** Use **Backup → Save backup file** regularly. That file is also how you move cases to another phone or hand them to whoever takes over.
- **Each visitor to the published site gets their own empty copy.** Two volunteers on the same link do not see each other's dogs. A genuinely shared list would need a server and a database, which this project deliberately does not have.

If a browser blocks local storage, the app says so plainly and keeps working in memory rather than pretending your work is saved.

Photos are shrunk to 900px on the device before being stored, because a phone photo is several megabytes and browser storage holds only a few. If storage fills, the app tells you and suggests exporting a backup.

## Publishing it

Any static host will serve it. See [PUBLISHING.md](PUBLISHING.md) for step-by-step instructions for Netlify Drop and GitHub Pages.

Serve it over HTTPS. The camera and location button are disabled by browsers on plain `http://`.

## How it is built

Plain HTML, CSS and JavaScript in one file — no framework, no bundler. The file you edit is the file that runs.

- **Storage** is `localStorage`, wrapped so a blocked or full store degrades honestly rather than failing silently.
- **Anything loaded from storage or a backup file is rebuilt field by field**, so a hand-edited or corrupted file cannot break the app or smuggle markup into the page.
- **Layout** is one set of markup with a media query: a phone gets top tabs and a thumb-height action bar, a desktop gets a sidebar workspace. No JavaScript reads the window width.
- **Charts** are hand-drawn SVG. **Icons** are an inline sprite. **PDFs and posters** use a print stylesheet rather than a rendering library.
- Motion is skipped entirely for anyone with reduced motion turned on.

Data is stored under the key `street-rescue.v1`. Backup files are plain JSON and a CSV export is available for spreadsheets.

## Known limits

- Single device, single person. No sync, no shared list, no accounts.
- Offline works after the first visit, but the first load needs a connection for the fonts. Making it reliably offline and installable to a home screen needs a service worker and a web manifest — not yet added.
- Storage caps out at a few megabytes, which in practice means roughly a hundred dogs with photos. Export and prune before you get there.
- The duplicate-report check matches on location text only. It warns once and then trusts you.

## Licence

MIT. Use it, change it, give it to another rescue group.
