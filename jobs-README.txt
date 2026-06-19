==================================================================
 FASTREC JOB BOARD — how to edit the listings
==================================================================

The jobs shown on the website come from a list of simple records.
Each job has these fields:

  title      Job title              e.g. "Class 1 (HGV) Driver"
  category   One of EXACTLY these:  warehouse | driving | manufacturing | forklift
             (this controls the colour tag AND the filter buttons)
  type       Free text badge        e.g. "Temp", "Permanent", "Temp → Perm"
  location   Town and postcode      e.g. "Leeds · LS10"
  pay        Pay rate               e.g. "£15.50 / hr"  or  "£28,000 – £32,000 / yr"
  shift      Shift / notes          e.g. "Multi-drop · Days"
  role       (optional) pre-selects the dropdown on the application form.
             Use one of:
               Warehouse / Picking
               Driving (HGV / Van)
               Manufacturing / Production
               Forklift (FLT)
               Other / Not sure

You have THREE ways to manage the jobs. Pick whichever suits you.

------------------------------------------------------------------
 OPTION 1 — Edit the page directly (works everywhere, no hosting)
------------------------------------------------------------------
Open index.html in a text editor and find the line:

    const DEFAULT_JOBS = [

Edit, add or remove the rows there. Each row looks like:

    { title: 'Warehouse Operative', category: 'warehouse', type: 'Temp',
      location: 'Sheffield · S9', pay: '£11.80 – £13.20 / hr',
      shift: 'Days & Nights · Immediate', role: 'Warehouse / Picking' },

Save the file and refresh the browser. Done.

------------------------------------------------------------------
 OPTION 2 — Edit jobs.json (once the site is hosted online)
------------------------------------------------------------------
Edit the file "jobs.json" in this folder. It contains the same list
in plain JSON. When the website is hosted on a web server / host
(http or https), the page loads jobs.json automatically and it
overrides the built-in list — so you only edit jobs.json.

NOTE: This does NOT work when you just double-click index.html to open
it from your computer (browsers block local files from reading other
local files). It only takes effect once the site is published online.
While testing locally, use Option 1.

------------------------------------------------------------------
 OPTION 3 — Manage jobs from a Google Sheet (no code at all)
------------------------------------------------------------------
1. Create a Google Sheet. Put these column headers in row 1
   (lowercase, exactly):
        title   category   type   location   pay   shift   role
2. Fill one job per row underneath.
3. File ▸ Share ▸ set "Anyone with the link" can VIEW.
4. Copy the sheet ID from its URL — the long code between /d/ and /edit:
        https://docs.google.com/spreadsheets/d/THIS_IS_THE_ID/edit
5. Build a data URL using the free opensheet service (sheet tab is
   usually called "Sheet1"):
        https://opensheet.elk.sh/THIS_IS_THE_ID/Sheet1
6. Open index.html, find:
        sheetUrl: ''
   and paste your URL inside the quotes:
        sheetUrl: 'https://opensheet.elk.sh/THIS_IS_THE_ID/Sheet1'
   Save. Now editing the Google Sheet updates the website (after a
   refresh). Like Option 2, this works on the hosted site, not on a
   double-clicked local file.

------------------------------------------------------------------
 Priority order
------------------------------------------------------------------
If sheetUrl is set, the Google Sheet is used.
Otherwise jobs.json is used (when hosted).
If neither can be reached, the built-in DEFAULT_JOBS list shows.
==================================================================
