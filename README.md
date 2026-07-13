# New Hires Map — College of Liberal Arts

`new-hires-map.html` is a single, self-contained file: no libraries, no internet
connection, no build step. Each pin marks the university where a new hire
studied; hovering (or tabbing to) a name shows the city, university, degree,
and area of study. Everything below is done by opening the file in a text
editor or a browser.

## Editing people

Open `new-hires-map.html` in any text editor and search for `EDIT YOUR PEOPLE
HERE`. Each person is one entry in the `PEOPLE` list:

```js
{ name:"Paige Pellaton", department:"POLS", city:"Davis", state:"CA",
  lat:38.5449, lon:-121.7405, university:"UC Davis", degree:"PhD",
  major:"Political Science",
  label:{dx:10, dy:7, anchor:"start"} },
```

- **lat / lon** — search the web for `"<city> <state> coordinates"` and copy
  the two numbers. Latitude is the positive one (north); longitude is negative
  for the US (west). Pins land on the exact spot, Alaska and Hawaii included.
- **label** (optional) — nudges where the name sits so labels don't overlap.
  `dx` moves the name right (+) or left (−), `dy` down (+) or up (−).
  `anchor:"start"` puts the name to the right of the dot, `"end"` to the left,
  `"middle"` centered below (the default). The California cluster in the
  current data is a worked example: coastal names hang left over the Pacific,
  inland names go right over the desert.
- Two people at the same university (the two UC Davis and two USC hires) can
  share identical coordinates — give each a different `label` offset and both
  names stay hoverable.

The title and subtitle are near the top of the file, marked with
`<!-- EDIT: page title and subtitle -->`. The roster table under the map
builds itself from the same list — never edit it by hand.

After editing, double-click the file to open it in a browser and check that
every comma and quote survived. If the map comes up blank, a comma is missing.

## Print / export to PDF

Click **Print / save as PDF** on the page (or Ctrl/Cmd-P) and choose "Save as
PDF" as the destination. It is preset to letter-size landscape: the map fills
page 1 with names at roughly 10-point type, and the full roster table
(department, university, city, degree, area of study) prints on page 2 — so
the hover details are on paper too. If the greens come out white, enable
"Background graphics" in the print dialog.

## Hosting + embedding in Drupal 10

**OneDrive will not work** — it never serves HTML files as web pages, only as
downloads or previews, so an iframe pointing at OneDrive shows nothing.

Best options, in order:

1. **Your own Drupal server (recommended).** Ask your web admin to upload
   `new-hires-map.html` to the site's public files area
   (`/sites/default/files/`). It's one static file, no server code. Same-origin
   means no iframe restrictions at all.
2. **GitHub Pages** — free, reliable, no server: create a public repository,
   upload the file, enable Pages in Settings. Note the page contents (the
   names) become public on GitHub itself, which they would be on your site
   anyway.
3. **Netlify Drop** (drop.netlify.com) — drag the file onto the page, get a
   URL. Free tier is fine for this.

Then in Drupal, add this to any page that allows full HTML / iframes:

```html
<iframe src="https://YOUR-URL/new-hires-map.html"
        title="Map of the United States showing the universities where new College of Liberal Arts hires studied"
        width="100%" height="820" style="border:none;"
        loading="lazy"></iframe>
```

Keep the `title` attribute — it is required for accessibility. Adjust `height`
to taste (820px suits a desktop page width; the map scales itself to the
iframe's width).

## Accessibility (WCAG 2.1 AA)

Already built in: every pin is keyboard-reachable with Tab (ordered west to
east) and announces name, university, city, degree, and area of study to
screen readers; the hover card also appears on keyboard focus, stays up while
hovered, and dismisses with Esc (WCAG 1.4.13); a real `<table>` version of all
the data sits under the map ("View the full roster as a table"); text contrast
exceeds AA on all the greens; focus outlines are visible; animation respects
reduced-motion settings. Nothing relies on color alone or on hovering alone.
