# CAP Fluxx Converter

Converts new Fluxx XLSX partner reports to the 57-column CSV format required to overwrite the ArcGIS feature layer.

**Live tool:** https://franzenjb.github.io/CAP_Fluxx_Converter/

## How It Works

1. Drop the Fluxx XLSX file (`fluxx_cap_national_ops_summary_partner_map_*.xlsx`)
2. Tool maps 11 new columns → 57-column ArcGIS schema
3. Download `CAP_2025_Partnerships_IV.csv`
4. Upload to ArcGIS Online and let ESRI geocode addresses (~325 records)

## Current Column Mapping

| Fluxx XLSX (New) | ArcGIS CSV (Required) |
|---|---|
| CAP Partner | Name |
| Street Address | Street |
| Street Address 2 | Street2 |
| City | City |
| State | State (normalized to `US-XX`) |
| Postal Code | Zip Code |
| County | Jurisdiction Served |
| Primary Focus Area | Primary Focus |
| Website | Website |
| Impact | Partnership Impact |
| Collaboration | Collaboration |

## 46 Unmapped Fields (exported as empty)

These fields existed in the old system but are **not present** in the new Fluxx report:

- **MOU Status** — partner agreement status
- **Contact info** — Partner Contact, Title, Email, Phone
- **Secondary/Tertiary Focus**
- **Staffing** — Full-Time Staff, Part-Time Staff, Volunteers
- **Intent of Partnership**
- **Field Team**
- **26 Yes/No service capability columns** (meals, shelters, health, casework, etc.)
- **Media** — Flickr Link, Video1, Video2
- **Coordinates** — Latitude, Longitude, x, y (ESRI geocodes on upload)

## Pending — Waiting on Client Direction

- [ ] Confirm the 46 empty fields are acceptable or if Fluxx will add them
- [ ] Confirm row count drop is expected (old: ~840 → new: 327)
- [ ] Determine if feature layer schema should be simplified to match new report
- [ ] Confirm output filename stays `CAP_2025_Partnerships_IV.csv` or changes
- [ ] Determine if MOU Status / contact fields are coming from a separate source

## Tech

- Client-side only — single `index.html` with [SheetJS](https://sheetjs.com/) CDN
- Hosted on GitHub Pages, no backend needed
- State codes auto-normalized (`OR` → `US-OR`)
- Handles multiline text fields with proper CSV quoting
