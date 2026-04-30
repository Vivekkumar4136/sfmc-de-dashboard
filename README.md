# SFMC Data Extension Dashboard

A reusable **Salesforce Marketing Cloud (SFMC)** CloudPage that gives you a clean, searchable, and paginated view of **all Data Extensions** in your Business Unit — including live record counts, full folder paths, and created/modified dates.

---

##  What It Does

Managing hundreds of Data Extensions in SFMC can be overwhelming. This dashboard solves that by pulling all DE metadata into one place with powerful filtering — no more clicking through folders one by one.

---

##  Features

-  **Search** by DE Name or Customer Key
-  **Filter by Folder** using a dropdown
-  **Date Range Filter** on Created Date
-  **Pagination** — configurable (5 / 10 / 20 / 50 rows per page)
-  **Jump to any page** directly
-  **Live Record Count** for every DE using `DataExtensionRowCount`
- ️ **Full Folder Path** — shows complete hierarchy, not just parent folder
-  **Mobile Responsive** layout
-  Skips `QueryStudioResults` DEs automatically (noise reduction)

---

## ️ Tech Stack

| Layer | Technology |
|---|---|
| Server-side logic | SSJS (Server-Side JavaScript) |
| API calls | WSProxy (`Script.Util.WSProxy`) |
| Row count | AMPscript (`DataExtensionRowCount`) |
| Frontend | HTML / CSS / Vanilla JavaScript |
| Hosting | SFMC CloudPages |

---

##  Columns Displayed

| Column | Description |
|---|---|
| DE Name | Name of the Data Extension |
| Customer Key | External Key of the DE |
| Folder Path | Full folder hierarchy path |
| Created Date | Date the DE was created |
| Modified Date | Date the DE was last modified |
| Record Count | Live count of records in the DE |

---

## ️ How It Works

### Folder Path Resolution
Instead of showing just the immediate parent folder, the dashboard **recursively builds the full folder path** by:
1. Fetching all `DataFolder` objects with their parent references via WSProxy
2. Walking up the parent chain to construct the complete path (e.g. `Data Extensions/Campaigns/Region/SubFolder`)

### Data Fetching
- Uses `WSProxy.retrieve()` with `BatchSize: 300` and **pagination loop** (`HasMoreRows`) to fetch ALL DEs — no matter how many exist in the BU
- Runs entirely server-side on CloudPage load via `<script runat="server">`

### Frontend Filtering & Pagination
- All filtering and pagination is handled client-side with Vanilla JS
- No external libraries or frameworks needed

---

##  How to Use

1. Log in to your **Salesforce Marketing Cloud** account
2. Go to **CloudPages** → Create a new **Code Resource** or **Landing Page**
3. Paste the contents of `DE_Dashboard.html` into the editor
4. **Update the folder dropdown** options to match your BU's folder structure (or remove them — the search filter works without them)
5. **Publish** the CloudPage
6. Open the published URL — the dashboard loads automatically

> ️ **Note:** This CloudPage must be published in the context of an authenticated SFMC session or secured appropriately, as it uses WSProxy which requires server-side execution.

---

##  File Structure

```
sfmc-de-dashboard/
│
└── DE_Dashboard.html      # Single file — complete dashboard (SSJS + HTML + CSS + JS)
```


##  Use Cases

- Quickly audit all DEs in a BU
- Find DEs by name or key during development/debugging
- Identify empty or unused DEs (record count = 0)
- Track recently created or modified DEs using date filters
- Onboard new team members — gives instant visibility into BU structure


Author
Built by an SFMC Developer as a reusable internal reporting tool.
If this helped you, leave a star on the repo and connect on LinkedIn!


License
MIT License — free to use, modify, and distribute.

