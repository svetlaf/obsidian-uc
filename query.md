
# 1. Derecho Civil II
## 1. Lista completa

```dataviewjs
const {fieldModifier: f} = this.app.plugins.plugins["metadata-menu"].api;
// --- CONFIGURATION ---

// The list of dates to create rows for in the table.
const datesToList = [
    "11-08-2025", "12-08-2025",
    "13-08-2025", "18-08-2025", "19-08-2025", "20-08-2025", "25-08-2025",
    "26-08-2025", "27-08-2025", "01-09-2025", "02-09-2025", "03-09-2025",
    "08-09-2025", "09-09-2025", "10-09-2025", "22-09-2025", "23-09-2025",     "24-09-2025", "29-09-2025", "30-09-2025", "01-10-2025", "06-10-2025",     "07-10-2025", "08-10-2025",
    "13-10-2025", "14-10-2025", "15-10-2025", "20-10-2025", "21-10-2025",
    "22-10-2025", "27-10-2025", "28-10-2025", "29-10-2025", "03-11-2025",
    "04-11-2025", "05-11-2025", "10-11-2025", "11-11-2025", "12-11-2025"
];

// The headers for your table columns.
const tableHeaders = ["Fecha", "Presente/Ausente", "Completitud"];

// --- SCRIPT LOGIC ---

// Find all pages with fileClass "clase" and asignatura "derecho-civil2".
const pages = dv.pages().where(p => p.fileClass === "clase" && p.asignatura === "derecho-civil2");

// Create a Map for quick lookup of pages by their date string.
const pagesByDate = new Map();
for (let page of pages) {
    if (page.fecha) {
        pagesByDate.set(page.fecha, page);
    }
}

// Build the data for each row of the table.
const tableRows = datesToList.map(dateStr => {
    const page = pagesByDate.get(dateStr);
    
    // --- LINKING LOGIC ---
    // Set default values for when no note is found.
    let dateCell = dateStr;
    let presentCell = "❌";
    let completeCell = "❌";

    // If a page is found for the date, create links.
    if (page) {
        // Determine the status and icon for each column.
        const isPresent = (page["presente/ausente"] === "presente");
        const isComplete = (page.Completitud === true || page.Completitud === "true");
        const presentIcon = isPresent ? "✅" : "❌";
        const completeIcon = isComplete ? "✅" : "❌";

        // Create the markdown links. The format is [[FilePath|DisplayText]].
        // 'page.file.path' gets the full path to the note.
        dateCell = `[[${page.file.path}|${dateStr}]]`;
        presentCell = `[[${page.file.path}|${presentIcon}]]`;
        completeCell = `[[${page.file.path}|${completeIcon}]]`;
    }
    
    // Return the array for the current row, which now contains links if a page was found.
    return [dateCell, presentCell, completeCell];
});

// Create and display the final table.
dv.table(tableHeaders, tableRows);
```



## 2. Asistencia

```dataviewjs
// --- CONFIGURATION ---

// The total number of scheduled classes for the subject.
const clasesTotales = 40;

// The attendance percentage required to be considered "Sufficient".
const umbralAsistencia = 60;

// --- SCRIPT LOGIC ---

// Find all pages that are for the target subject.
const pages = dv.pages().where(p => 
    p.fileClass == "clase" && 
    p.asignatura == "derecho-civil2"
);

// **CORRECTED LINE**: Count the absences by filtering the 'pages' collection.
const ausencias = pages.where(p => p["presente/ausente"] == "ausente").length;

const presencias = pages.where(p => p["presente/ausente"] == "presente").length;

// Calculate the number of classes attended.
const asistencias = presencias - ausencias;

// Calculate the attendance percentage. Avoid division by zero if there are no classes.
const porcentajeAsistencia = clasesTotales > 0 ? (asistencias / clasesTotales) * 100 : 0;

// Determine the final status based on the attendance threshold.
// NOTE: "SUFICIENTE" is assigned if attendance is greater than 50%.
const estado = porcentajeAsistencia > umbralAsistencia ? "SUFICIENTE" : "INSUFICIENTE";

// --- DISPLAY TABLE ---

// Define the headers for the summary table.
const headers = ["Clases Totales", "Ausencias", "Asistencia (%)", "Estado"];

// Create the single row of data for the table.
const rowData = [
    clasesTotales,
    ausencias,
    `${porcentajeAsistencia.toFixed(2)}%`, // Format percentage to 2 decimal places
    estado
];

// Render the final table.
dv.table(headers, [rowData]);
```


# 2. Derecho Procesal I

## 1. Tabla completa

```dataviewjs
const {fieldModifier: f} = this.app.plugins.plugins["metadata-menu"].api;
// --- CONFIGURATION ---

// The list of dates to create rows for in the table.
const datesToList = [
    "04-08-2025", "06-08-2025", "08-08-2025", "11-08-2025", "13-08-2025",
    "18-08-2025", "20-08-2025", "22-08-2025", "25-08-2025", "27-08-2025",
    "29-08-2025", "01-09-2025", "03-09-2025", "05-09-2025", "08-09-2025",
    "10-09-2025", "12-09-2025", "15-09-2025", "17-09-2025", "22-09-2025",
    "24-09-2025", "26-09-2025", "29-09-2025", "01-10-2025", "03-10-2025",
    "06-10-2025", "08-10-2025", "10-10-2025", "13-10-2025", "15-10-2025",
    "17-10-2025", "20-10-2025", "22-10-2025", "24-10-2025", "27-10-2025",
    "29-10-2025", "03-11-2025", "05-11-2025", "07-11-2025", "10-11-2025",
    "12-11-2025", "14-11-2025"
];

// The headers for your table columns.
const tableHeaders = ["Fecha", "Presente/Ausente", "Completitud"];

// --- SCRIPT LOGIC ---

// Find all pages with fileClass "clase" and asignatura "derecho-procesal".
const pages = dv.pages().where(p => p.fileClass == "clase" && p.asignatura == "derecho-procesal1");

// Create a Map for quick lookup of pages by their date string.
const pagesByDate = new Map();
for (let page of pages) {
    if (page.fecha) {
        pagesByDate.set(page.fecha, page);
    }
}

// Build the data for each row of the table.
const tableRows = datesToList.map(dateStr => {
    const page = pagesByDate.get(dateStr);
    
    // Set default values for when no note is found.
    let dateCell = dateStr;
    let presentCell = "❌";
    let completeCell = "❌";

    // If a page is found for the date, create links.
    if (page) {
        // Determine the status and icon for each column.
        const isPresent = (page["presente/ausente"] == "presente");
        const isComplete = (page.Completitud == true || page.Completitud == "true");
        const presentIcon = isPresent ? "✅" : "❌";
        const completeIcon = isComplete ? "✅" : "❌";

        // Create the markdown links.
        dateCell = `[[${page.file.path}|${dateStr}]]`;
        presentCell = `[[${page.file.path}|${presentIcon}]]`;
        completeCell = `[[${page.file.path}|${completeIcon}]]`;
    }
    
    // Return the array for the current row.
    return [dateCell, presentCell, completeCell];
});

// Create and display the final table.
dv.table(tableHeaders, tableRows);
```


## 2.  Asistencia

(No es obligatoria)




# 3. Derecho Internacional Público

```dataviewjs
const {fieldModifier: f} = this.app.plugins.plugins["metadata-menu"].api;
// --- CONFIGURATION ---

// The list of dates to create rows for in the table.
const datesToList = [
    "04-08-2025", "06-08-2025", "08-08-2025", "11-08-2025", "13-08-2025",
    "18-08-2025", "20-08-2025", "22-08-2025", "25-08-2025", "27-08-2025",
    "29-08-2025", "01-09-2025", "03-09-2025", "05-09-2025", "08-09-2025",
    "10-09-2025", "12-09-2025", "15-09-2025", "17-09-2025", "22-09-2025",
    "24-09-2025", "26-09-2025", "29-09-2025", "01-10-2025", "03-10-2025",
    "06-10-2025", "08-10-2025", "10-10-2025", "13-10-2025", "15-10-2025",
    "17-10-2025", "20-10-2025", "22-10-2025", "24-10-2025", "27-10-2025",
    "29-10-2025", "03-11-2025", "05-11-2025", "07-11-2025", "10-11-2025",
    "12-11-2025", "14-11-2025"
];

// The headers for your table columns.
const tableHeaders = ["Fecha", "Presente/Ausente", "Completitud"];

// --- SCRIPT LOGIC ---

// Find all pages with fileClass "clase" and asignatura "derecho-procesal".
const pages = dv.pages().where(p => p.fileClass == "clase" && p.asignatura == "derecho-internacional-publico");

// Create a Map for quick lookup of pages by their date string.
const pagesByDate = new Map();
for (let page of pages) {
    if (page.fecha) {
        pagesByDate.set(page.fecha, page);
    }
}

// Build the data for each row of the table.
const tableRows = datesToList.map(dateStr => {
    const page = pagesByDate.get(dateStr);
    
    // Set default values for when no note is found.
    let dateCell = dateStr;
    let presentCell = "❌";
    let completeCell = "❌";

    // If a page is found for the date, create links.
    if (page) {
        // Determine the status and icon for each column.
        const isPresent = (page["presente/ausente"] == "presente");
        const isComplete = (page.Completitud == true || page.Completitud == "true");
        const presentIcon = isPresent ? "✅" : "❌";
        const completeIcon = isComplete ? "✅" : "❌";

        // Create the markdown links.
        dateCell = `[[${page.file.path}|${dateStr}]]`;
        presentCell = `[[${page.file.path}|${presentIcon}]]`;
        completeCell = `[[${page.file.path}|${completeIcon}]]`;
    }
    
    // Return the array for the current row.
    return [dateCell, presentCell, completeCell];
});

// Create and display the final table.
dv.table(tableHeaders, tableRows);
```



# 4. Derecho del trabajo
## 1. Lista completa

```dataviewjs
const {fieldModifier: f} = this.app.plugins.plugins["metadata-menu"].api;
// --- CONFIGURATION ---

// The list of dates to create rows for in the table.
const datesToList = [
	"05-08-2025", "07-08-2025", "12-08-2025", "13-08-2025",
	"14-08-2025", "19-08-2025", "20-08-2025", "21-08-2025", "26-08-2025",
	"27-08-2025", "28-08-2025", "02-09-2025", "03-09-2025", "04-09-2025",
	"09-09-2025", "10-09-2025", "11-09-2025",
	"23-09-2025", "24-09-2025", "25-09-2025", "30-09-2025", "01-10-2025",
	"02-10-2025", "07-10-2025", "08-10-2025", "09-10-2025", "14-10-2025",
	"15-10-2025", "16-10-2025", "21-10-2025", "22-10-2025", "23-10-2025",
	"28-10-2025", "29-10-2025", "30-10-2025", "04-11-2025", "05-11-2025",
	"06-11-2025", "11-11-2025", "12-11-2025", "13-11-2025"

];

// The headers for your table columns.
const tableHeaders = ["Fecha", "Presente/Ausente", "Completitud"];

// --- SCRIPT LOGIC ---

// Find all pages with fileClass "clase" and asignatura "derecho-procesal".
const pages = dv.pages().where(p => p.fileClass == "clase" && p.asignatura == "derecho-laboral");

// Create a Map for quick lookup of pages by their date string.
const pagesByDate = new Map();
for (let page of pages) {
    if (page.fecha) {
        pagesByDate.set(page.fecha, page);
    }
}

// Build the data for each row of the table.
const tableRows = datesToList.map(dateStr => {
    const page = pagesByDate.get(dateStr);
    
    // Set default values for when no note is found.
    let dateCell = dateStr;
    let presentCell = "❌";
    let completeCell = "❌";

    // If a page is found for the date, create links.
    if (page) {
        // Determine the status and icon for each column.
        const isPresent = (page["presente/ausente"] == "presente");
        const isComplete = (page.Completitud == true || page.Completitud == "true");
        const presentIcon = isPresent ? "✅" : "❌";
        const completeIcon = isComplete ? "✅" : "❌";

        // Create the markdown links.
        dateCell = `[[${page.file.path}|${dateStr}]]`;
        presentCell = `[[${page.file.path}|${presentIcon}]]`;
        completeCell = `[[${page.file.path}|${completeIcon}]]`;
    }
    
    // Return the array for the current row.
    return [dateCell, presentCell, completeCell];
});

// Create and display the final table.
dv.table(tableHeaders, tableRows);
```

## 2. Asistencia

```dataviewjs
// --- CONFIGURATION ---

// The total number of scheduled classes for the subject.
const clasesTotales = 41;

// The attendance percentage required to be considered "Sufficient".
const umbralAsistencia = 50;

// --- SCRIPT LOGIC ---

// Find all pages that are for the target subject.
const pages = dv.pages().where(p => 
    p.fileClass == "clase" && 
    p.asignatura == "derecho-laboral"
);

// **CORRECTED LINE**: Count the absences by filtering the 'pages' collection.
const ausencias = pages.where(p => p["presente/ausente"] == "ausente").length;

const presencias = pages.where(p => p["presente/ausente"] == "presente").length;

// Calculate the number of classes attended.
const asistencias = presencias - ausencias;

// Calculate the attendance percentage. Avoid division by zero if there are no classes.
const porcentajeAsistencia = clasesTotales > 0 ? (asistencias / clasesTotales) * 100 : 0;

// Determine the final status based on the attendance threshold.
// NOTE: "SUFICIENTE" is assigned if attendance is greater than 50%.
const estado = porcentajeAsistencia > umbralAsistencia ? "SUFICIENTE" : "INSUFICIENTE";

// --- DISPLAY TABLE ---

// Define the headers for the summary table.
const headers = ["Clases Totales", "Ausencias", "Asistencia (%)", "Estado"];

// Create the single row of data for the table.
const rowData = [
    clasesTotales,
    ausencias,
    `${porcentajeAsistencia.toFixed(2)}%`, // Format percentage to 2 decimal places
    estado
];

// Render the final table.
dv.table(headers, [rowData]);
```


# 5. Teología
## 1. Lista completa

```dataviewjs
const {fieldModifier: f} = this.app.plugins.plugins["metadata-menu"].api;
// --- CONFIGURATION ---

// The list of dates to create rows for in the table.
const datesToList = [
    "05-08-2025", "07-08-2025", "12-08-2025", "14-08-2025", "19-08-2025",
    "21-08-2025", "26-08-2025", "28-08-2025", "02-09-2025", "04-09-2025",
    "09-09-2025", "11-09-2025", "16-09-2025", "23-09-2025", "25-09-2025",
    "30-09-2025", "02-10-2025", "07-10-2025", "09-10-2025", "14-10-2025",
    "16-10-2025", "21-10-2025", "23-10-2025", "28-10-2025", "30-10-2025",
    "04-11-2025", "06-11-2025", "11-11-2025", "13-11-2025"
];

// The headers for your table columns.
const tableHeaders = ["Fecha", "Presente/Ausente", "Completitud"];

// --- SCRIPT LOGIC ---

// Find all pages with fileClass "clase" and asignatura "derecho-procesal".
const pages = dv.pages().where(p => p.fileClass == "clase" && p.asignatura == "teologia");

// Create a Map for quick lookup of pages by their date string.
const pagesByDate = new Map();
for (let page of pages) {
    if (page.fecha) {
        pagesByDate.set(page.fecha, page);
    }
}

// Build the data for each row of the table.
const tableRows = datesToList.map(dateStr => {
    const page = pagesByDate.get(dateStr);
    
    // Set default values for when no note is found.
    let dateCell = dateStr;
    let presentCell = "❌";
    let completeCell = "❌";

    // If a page is found for the date, create links.
    if (page) {
        // Determine the status and icon for each column.
        const isPresent = (page["presente/ausente"] == "presente");
        const isComplete = (page.Completitud == true || page.Completitud == "true");
        const presentIcon = isPresent ? "✅" : "❌";
        const completeIcon = isComplete ? "✅" : "❌";

        // Create the markdown links.
        dateCell = `[[${page.file.path}|${dateStr}]]`;
        presentCell = `[[${page.file.path}|${presentIcon}]]`;
        completeCell = `[[${page.file.path}|${completeIcon}]]`;
    }
    
    // Return the array for the current row.
    return [dateCell, presentCell, completeCell];
});

// Create and display the final table.
dv.table(tableHeaders, tableRows);
```


## 2. Asistencia
```dataviewjs
// --- CONFIGURATION ---

// The total number of scheduled classes for the subject.
const clasesTotales = 29;

// The attendance percentage required to be considered "Sufficient".
const umbralAsistencia = 75;

// --- SCRIPT LOGIC ---

// Find all pages that are for the target subject.
const pages = dv.pages().where(p => 
    p.fileClass == "clase" && 
    p.asignatura == "teologia"
);

// **CORRECTED LINE**: Count the absences by filtering the 'pages' collection.
const ausencias = pages.where(p => p["presente/ausente"] == "ausente").length;

const presencias = pages.where(p => p["presente/ausente"] == "presente").length;

// Calculate the number of classes attended.
const asistencias = presencias - ausencias;

// Calculate the attendance percentage. Avoid division by zero if there are no classe
const porcentajeAsistencia = clasesTotales > 0 ? (asistencias / clasesTotales) * 100 : 0;

// Determine the final status based on the attendance threshold.
// NOTE: "SUFICIENTE" is assigned if attendance is greater than 50%.
const estado = porcentajeAsistencia > umbralAsistencia ? "SUFICIENTE" : "INSUFICIENTE";

// --- DISPLAY TABLE ---

// Define the headers for the summary table.
const headers = ["Clases Totales", "Ausencias", "Asistencia (%)", "Estado"];

// Create the single row of data for the table.
const rowData = [
    clasesTotales,
    ausencias,
    `${porcentajeAsistencia.toFixed(2)}%`, // Format percentage to 2 decimal places
    estado
];

// Render the final table.
dv.table(headers, [rowData]);
```