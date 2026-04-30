SFMC Data Extension Dashboard
A reusable Salesforce Marketing Cloud (SFMC) CloudPage that gives you a clean, searchable, and paginated view of all Data Extensions in your Business Unit — including live record counts, full folder paths, and created/modified dates.

What It Does
Managing hundreds of Data Extensions in SFMC can be overwhelming. This dashboard solves that by pulling all DE metadata into one place with powerful filtering — no more clicking through folders one by one.

Features:-

Search by DE Name or Customer Key
Filter by Folder using a dropdown
Date Range Filter on Created Date
Pagination — configurable (5 / 10 / 20 / 50 rows per page)
⏩ Jump to any page directly
Live Record Count for every DE using DataExtensionRowCount
️ Full Folder Path — shows complete hierarchy, not just parent folder
Mobile Responsive layout
Skips QueryStudioResults DEs automatically (noise reduction)


️ Tech Stack
LayerTechnologyServer-side logicSSJS (Server-Side JavaScript)API callsWSProxy (Script.Util.WSProxy)Row countAMPscript (DataExtensionRowCount)FrontendHTML / CSS / Vanilla JavaScriptHostingSFMC CloudPages

Columns Displayed
ColumnDescriptionDE NameName of the Data ExtensionCustomer KeyExternal Key of the DEFolder PathFull folder hierarchy pathCreated DateDate the DE was createdModified DateDate the DE was last modifiedRecord CountLive count of records in the DE

️ How It Works:-

Folder Path Resolution:
Instead of showing just the immediate parent folder, the dashboard recursively builds the full folder path by:
Fetching all DataFolder objects with their parent references via WSProxy
Walking up the parent chain to construct the complete path (e.g. Data Extensions/Campaigns/Region/SubFolder)

Data Fetching:
Uses WSProxy.retrieve() with BatchSize: 300 and pagination loop (HasMoreRows) to fetch ALL DEs — no matter how many exist in the BU
Runs entirely server-side on CloudPage load via <script runat="server">

Frontend Filtering & Pagination :
All filtering and pagination is handled client-side with Vanilla JS
No external libraries or frameworks needed
