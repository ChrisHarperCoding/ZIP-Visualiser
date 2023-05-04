# ZIP Visualiser
Here's a simple example using HTML, CSS, and JavaScript to visualize the contents of a ZIP file:

Create an HTML file (index.html):
xml
Copy code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ZIP File Contents Visualizer</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>ZIP File Contents Visualizer</h1>
    <input type="file" id="zipFileInput" accept=".zip">
    <div id="fileList"></div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.7.1/jszip.min.js"></script>
    <script src="script.js"></script>
</body>
</html>
Create a CSS file (styles.css) for styling:
css
Copy code
body {
    font-family: Arial, sans-serif;
    margin: 20px;
}

h1 {
    text-align: center;
}

input[type="file"] {
    display: block;
    margin: 20px auto;
}

#fileList {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

.file {
    background-color: #f1f1f1;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin: 5px;
    padding: 10px;
    text-align: center;
}
Create a JavaScript file (script.js) to handle the ZIP file:
javascript
Copy code
const zipFileInput = document.getElementById("zipFileInput");
const fileList = document.getElementById("fileList");

zipFileInput.addEventListener("change", async (event) => {
    const file = event.target.files[0];

    if (file) {
        try {
            const zip = await JSZip.loadAsync(file);
            fileList.innerHTML = "";

            zip.forEach((relativePath, zipEntry) => {
                const div = document.createElement("div");
                div.classList.add("file");
                div.textContent = relativePath;
                fileList.appendChild(div);
            });
        } catch (error) {
            console.error("Error reading ZIP file:", error);
            fileList.innerHTML = "<p>Error reading ZIP file. Please try again.</p>";
        }
    } else {
        fileList.innerHTML = "";
    }
});
Save all the files in the same directory and open the index.html file in your browser. You should now see a simple website that allows you to upload a ZIP file and view its contents.
Please note that this example uses the JSZip library (https://stuk.github.io/jszip/) for handling ZIP files. The library is loaded directly from a CDN in the HTML file. If you want to download and host the library yourself, visit their GitHub repository: https://github.com/Stuk/jszip
