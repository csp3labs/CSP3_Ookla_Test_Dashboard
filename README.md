# CSP3 Ookla Live Test Dashboard — User Guide

How to read and use the dashboard, plus a list of everything it can do. The same content is available inside the dashboard: press **❓ Help** in the top toolbar.

---

## 1. What the dashboard does

The CSP3 Ookla Speedtest Logger on each tester's phone adds one row to a shared Google Sheet for every test. This dashboard reads that sheet live and shows how the network performed: pass rates, averages, failures, charts, a map of where each test was taken, and a log of every test. Times are shown in Philippine time (PHT, UTC+8).

## 2. Quick tour

| Area | What it is |
| :--- | :--- |
| **Header** | Title, sync status, and the toolbar buttons (below) |
| **Threshold Settings** | The 4G and 5G download/upload limits that decide pass or fail |
| **Main Test Summary** | Totals, pass rates and averages |
| **Failure Count Breakdown** | Which limit each failed test missed |
| **Multi-Select & Dynamic Filters** | Narrow everything to the tests you care about |
| **Charts** | Throughput, latency and signal strength of the latest 15 tests |
| **Interactive Test Location Map** | Pins for every test, with map/satellite/dark views |
| **Live Test Logs** | Every filtered test, with editable remarks |

### Toolbar buttons

| Button | What it does |
| :--- | :--- |
| ⏱️ **Auto Refresh: ON/OFF** | Refreshes the data every 30 seconds. Click to switch off or on |
| 📥 **Export CSV** | Downloads the filtered tests as a CSV file |
| 📊 **Export Excel (.xlsx)** | Downloads the filtered tests as an Excel file |
| 🔄 **Refresh Data** | Reloads the sheet right now |
| ▾ **Collapse all** / ▸ **Expand all** | Hides or shows every section at once |
| ❓ **Help** | Opens the built-in help |

The status line under the title shows **Connecting…**, **Syncing…**, **Live & Synced** (data is current) or **Sync Failed** (see Troubleshooting).

## 3. Step-by-step

1. **Check the status.** Wait for *Live & Synced*. New tests appear automatically while Auto Refresh is ON.
2. **Set the thresholds.** In *Threshold Settings* enter the minimum acceptable Mbps for 4G download, 4G upload, 5G download and 5G upload. Defaults: **4G 5 / 1**, **5G 25 / 3**. Everything recalculates the moment you change a value. **Reset Limits** brings the defaults back. Limits are not saved when you reload the page.
3. **Filter the data** (section 5). Every number, chart, pin and table row follows the filters.
4. **Read the summary** (section 4) and the failure breakdown.
5. **Look at the charts**, then the **map** (section 6).
6. **Open the log table**, click a row to find it on the map, and add remarks if needed (section 7).
7. **Export** the filtered result (section 8).
8. **Hide** the sections you do not need (section 9).

## 4. Reading the numbers

### Main Test Summary

| Card | Meaning |
| :--- | :--- |
| **Total Logs** | Number of tests that match your filters (the small text shows the overall total) |
| **Valid Samples** | Tests with a usable result: **PASS** plus **BELOW THRESHOLD** |
| **5G Passing** / **4G Passing** | Passed tests / all tests of that technology, with the percentage |
| **Avg Download / Upload / Latency** | Average of the valid samples only |

### Test status

| Status | Meaning | Valid sample? |
| :--- | :--- | :--- |
| 🟢 **PASS** | Download and upload both meet the limits for the test's technology | Yes |
| 🟠 **BELOW THRESHOLD** | A usable result, but the download or upload is under the limit | Yes |
| 🔴 **FAILED / NULL** | No usable result: download or upload is missing or zero, or the test was logged as failed | No |

A test counts as **5G** if its technology text contains "5G" (for example *5G/NSA*), and as **4G** if it contains "4G" or "LTE".

### Failure Count Breakdown

For 4G and for 5G, every failed test (below threshold or failed/null) is counted **once**:

| Counter | A test is counted here when… |
| :--- | :--- |
| **DL Failure** | only the download missed its limit |
| **UL Failure** | only the upload missed its limit |
| **DL & UL Failed** | both missed their limits, or nothing could be measured. These tests are *not* also counted in DL or UL |

Example (5G limits 25 / 3): a test with 10 Mbps down and 5 Mbps up counts under **5G DL Failure**; 40 down and 1 up counts under **5G UL Failure**; 10 down and 1 up counts only under **5G DL & UL Failed**. For each technology, the three counters add up to its number of failed tests.

## 5. Filters

| Filter | How it works |
| :--- | :--- |
| **Date** | Show one day (Philippine date) |
| **Start Hour / End Hour** | Show tests between two hours of the day (Philippine time). Both ends are inclusive, for example 08:00 to 17:59 |
| **Status** | PASS, BELOW THRESHOLD and/or FAILED / NULL |
| **Testers**, **Server Names**, **City / Locations**, **Technologies** | Pick one or more entries |
| **Search Keyword** | Matches tester, city, server, status, remarks or technology |

* **Select several items** in a list with **Ctrl/Cmd + click** (on a phone, tap each item).
* Nothing selected means "no restriction". Several items in the same filter mean *any of them*; different filters combine as *all of them*.
* **Deselect All Multi-Selects** clears the lists only; **Clear Filters** resets everything including date, hours and search.
* Your selections stay in place when the data refreshes, and new testers or servers appear in the lists automatically.
* Filters keep working while the filter section is hidden. If the numbers look low, check the filters.

## 6. Charts and map

**Charts** show the latest 15 filtered tests: **Throughput** (download on the left axis, upload on the right), **Latency**, and **Signal Strength (RSRP)**. Failed tests are left out of the throughput and latency charts.

**Map**
* Switch the base map at the top-right: **Map**, **Satellite** or **Dark**.
* **📍 Find my location** (round crosshair button at the top-left) shows where you are with a blue pin and zooms to it. Your browser will ask for permission the first time.
* Pins: 🟢 pass, 🟠 below threshold, 🔴 failed. Click a pin for the tester, time, speeds, latency, signal, server and remarks.
* The map zooms to fit all pins of the current filter whenever the data or filters change.

### Importing your own map layers

Use **📂 Import layers** above the map (or drag files onto the map) to add reference data such as site lists, sector polygons or boundaries.

| Format | What the file needs |
| :--- | :--- |
| **CSV / tab-delimited text** (`.csv`, `.tsv`, `.txt`, `.tab` exported as text) | A **lat** and **lon** column (or *latitude* / *longitude*, *x* / *y*) in degrees, or a **WKT** / **geometry** column. Comma, tab or semicolon separators are detected automatically |
| **Shapefile** | A `.zip` containing the `.shp`, `.dbf` and `.prj`, or select the `.shp`, `.dbf` and `.prj` files together. The `.prj` is needed unless the data is already in latitude/longitude |
| **GeoPackage** (`.gpkg`) | Every feature layer in the file is added as its own layer. Common local coordinate systems (WGS84, Web Mercator, Philippine UTM and PRS92) are converted automatically |
| **GeoJSON** (`.geojson`, `.json`) | Coordinates in latitude/longitude |

* Each imported layer appears as a chip under the toolbar with a **tick** to show or hide it, a **colour picker**, **⌖** to zoom to it and **✕** to remove it.
* Click a point, line or area to see its attributes in a popup.
* Your test pins always stay on top of imported layers.
* Layers last until you reload the page. Very large files show the first 50,000 features.
* **MapInfo TAB/MAP files cannot be read by a browser.** In MapInfo or QGIS, export the table to GeoPackage, Shapefile or CSV and import that file instead.
* Shapefile and GeoPackage import load a helper library the first time, so they need an internet connection.

## 7. Test log and remarks

* The table lists every filtered test. **Click a row** to jump to its pin on the map.
* **Remarks:** press **✏️ Edit**, type a note, then press **💾 Save**. The note is written back to the Google Sheet and appears in the table, the map popup, search and exports. If saving fails the button shows **❌ Retry**.

## 8. Exporting

* **Export CSV** and **Export Excel** save **only the tests currently shown** (after filters), with **every column of the Google Sheet** (including the raw cell information), plus two extra first columns: **Status Category** and **Time (PHT)**.
* File names are `CSP3_Ookla_Log_YYYY-MM-DD.csv` and `.xlsx`.
* **On iPhone/iPad** the share sheet opens: choose **Save to Files**.
* If rows were added since the last refresh, press **Refresh Data** first, then export.

## 9. Hiding and showing sections

* Every section has a small **▾ Hide / ▸ Show** button beside its title (each of the three charts too). Hidden sections keep only their title.
* **Collapse all** / **Expand all** in the toolbar do all sections at once.
* Your choice is remembered in the browser you use.

## 10. Feature list

**Data**
* Live data from the shared Google Sheet; automatic refresh every 30 seconds (switchable) and manual refresh
* Philippine time everywhere (UTC+8)

**Analysis**
* Editable 4G/5G download and upload thresholds, applied instantly
* Valid-sample logic that excludes failed/null tests from averages and charts
* 4G and 5G pass rates
* Failure breakdown that counts each failed test once (DL only, UL only, both)
* Everything follows the active filters

**Filters**
* Date, start and end hour, status, testers, servers, cities, technologies, keyword search
* Multi-select with Ctrl/Cmd + click, Deselect All, Clear Filters; selections survive refreshes

**Visuals**
* Throughput, latency and signal-strength charts
* Google map with Map, Satellite and Dark views, find-my-location button, colour-coded pins with detail popups and a legend
* Click a table row to focus its pin
* Import your own layers (CSV / tab-delimited, Shapefile, GeoPackage, GeoJSON) with colour, show/hide, zoom and remove controls

**Log and export**
* Full test log with status badges
* Editable remarks saved to the sheet
* CSV and Excel export of the filtered rows with all sheet columns; iPhone/iPad share-sheet support

**Layout**
* Hide/Show for every section, Collapse all / Expand all, remembered between visits
* Dark theme with opti / CSP3 branding, pattern background and tab icon
* Works on desktop and phone
* Built-in Help (❓ Help)

## 11. Troubleshooting

| Problem | What to do |
| :--- | :--- |
| **Sync Failed** | Check your internet connection and that the Apps Script link is still deployed, then press **Refresh Data** |
| Numbers or charts look too low | Check the filters, including the hidden filter section; press **Clear Filters** |
| **Export failed — Apps Script does not return all sheet fields** | The Apps Script needs the full-sheet option (`?view=full`); ask the sheet owner to update it |
| **Export failed — sheet changed since the last refresh** | Press **Refresh Data**, then export again |
| Map shows grey squares | The map tiles did not load; check your connection and reload the page |
| A layer will not import | CSV: check the *lat* / *lon* columns are in degrees (or add a WKT column). Shapefile: include the `.prj` (use a `.zip`). MapInfo TAB: export to GeoPackage, Shapefile or CSV first. Shapefile and GeoPackage need an internet connection for their helper library |
| Find my location does nothing | Allow location access for the page in your browser. Some embedded views block it |
| A remark did not save | The button shows **Retry**; check your connection and try again |
| The page looks unstyled or has no charts/map | The page needs internet access to load its libraries; reconnect and reload |
| Everything resets after reload | Thresholds and filters are not saved between visits (only hidden sections are) |

## 12. Glossary

* **DL / UL** — download / upload speed in Mbps.
* **4G / LTE, 5G / NSA** — mobile technology of the test. NSA is 5G that uses a 4G anchor.
* **RSRP** — signal strength in dBm; closer to zero is stronger (−80 is better than −110).
* **Valid sample** — a test with a usable result (pass or below threshold).
* **PHT** — Philippine time, UTC+8.
* **Threshold** — the minimum acceptable speed for a technology and direction.
