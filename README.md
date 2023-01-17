# CSV2Table2Excel.github.io

#### Display any CSV file as a searchable, filterable, pretty HTML table. 
#### Export HTML table to valid excel file effortlessly. Using HTML, CSS , JavaScript. 

# Usage

**Element for upload file**
``` 
<input type="file" acccept=".csv" id="picker"> 
```
###### Accepts only CSV files.

## CSV file to HTML table
###### In index.html 

```
<script>
window.onload = () => {
            var read = new FileReader();
            var picker = document.getElementById("picker");
            var table = document.getElementById("table");
            picker.onchange = () => read.readAsText(picker.files[0]);
            read.onloadend = () => {
                let csv = read.result;
                // Remove existing table data 
                table.innerHTML = "";
                // split csv file data into rows
                let rows = csv.split("\n");
                for (let row of rows) {
                    let clearedRows = row.replaceAll(",,", ", -- ,")   
                    let cols = clearedRows.match(/(?:\"([^\"]*(?:\"\"[^\"]*)*)\")|([^\",]+)/g);
                    let tr = table.insertRow();
                    for (let col of cols) {
                        let td = tr.insertCell();
                        td.innerHTML = col;
                    }
                }
            };
        };
</script>
```

## HTML table to Excel file 
###### Add script tag 
```
<script type="text/javascript" src="https://unpkg.com/xlsx@0.15.1/dist/xlsx.full.min.js"></script>
```
###### Java Script code for Export HTML table data to Excel file
```
<script>
 function ExportToExcel(type, fn, dl) {
            var elt = document.getElementById('table');
            var wb = XLSX.utils.table_to_book(elt, { sheet: "sheet1" });
            return dl ?
                XLSX.write(wb, { bookType: type, bookSST: true, type: 'base64' }) :
                XLSX.writeFile(wb, fn || ('MySheetName.' + (type || 'xlsx')));
        }
</script>
```
