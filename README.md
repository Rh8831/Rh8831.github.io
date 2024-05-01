<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Generate VLESS URI</title>
<style>
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
        background-color: #f8f9fa;
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 100vh;
    }
    .container {
        background-color: #fff;
        border-radius: 8px;
        box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
        padding: 30px;
        max-width: 400px;
        width: 100%;
        text-align: center;
    }
    h2 {
        color: #3F418D;
        margin-bottom: 20px;
    }
    label {
        font-weight: bold;
        color: #6C757D;
        margin-bottom: 10px;
        display: block;
    }
    input[type="text"] {
        width: 100%;
        padding: 12px;
        border: 1px solid #ced4da;
        border-radius: 5px;
        margin-bottom: 20px;
        box-sizing: border-box;
    }
    button {
        background-color: #3F418D;
        color: #fff;
        border: none;
        border-radius: 5px;
        padding: 12px 0;
        width: 100%;
        cursor: pointer;
        font-size: 16px;
        transition: background-color 0.3s ease;
    }
    button:hover {
        background-color: #30336b;
    }
    pre {
        display: none; /* Initially hide */
        background-color: #f8f9fa;
        padding: 20px;
        border-radius: 5px;
        white-space: pre-wrap;
        color: #495057;
        overflow-x: auto;
        margin-top: 20px;
        text-align: left;
    }
    .copy-button {
        display: none; /* Initially hide */
        background-color: #3F418D;
        color: #fff;
        border: none;
        border-radius: 5px;
        padding: 12px 0;
        width: 100%;
        cursor: pointer;
        font-size: 16px;
        transition: background-color 0.3s ease;
        margin-top: 20px;
    }
    .copy-button:hover {
        background-color: #30336b;
    }
</style>
<script>
    function replaceId() {
        var userInput = document.getElementById("idInput").value;
        var id = extractId(userInput);
        if (id) {
            var uri = 'vless://' + id + 
                '@tamin.ir:443?encryption=none&security=tls&sni=tamin.ir&' +
                'alpn=h2%2Chttp%2F1.1&fp=chrome&type=ws&' +
                'host=jfhnf-038d47646f-kfjcfjfkso.apps.ir-thr-ba1.arvancaas.ir&' +
                'path=%2Fws#%E2%AD%90Nimbaha%20%F0%9F%87%AE%F0%9F%87%B7%20--%3E%20%F0%9F%87%B3%F0%9F%87%B1%20%F0%9F%9A%80';

            document.getElementById("output").innerText = uri;
            document.getElementById("output").style.display = "block"; // Display the URI output
            document.getElementById("copyButton").style.display = "block"; // Display the "Copy URI" button
        } else {
            alert("Invalid input! Please provide a valid ID.");
        }
    }
    
    function extractId(input) {
        var match = input.match(/[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}/);
        return match ? match[0] : null;
    }
    
    function copyUri() {
        var copyText = document.getElementById("output");
        var range = document.createRange();
        range.selectNode(copyText);
        window.getSelection().removeAllRanges();
        window.getSelection().addRange(range);
        document.execCommand("copy");
        window.getSelection().removeAllRanges();
        alert("Copied URI to clipboard!");
    }
</script>
</head>
<body>
    <div class="container">
        <h2>Generate VLESS URI</h2>
        <label for="idInput">Enter new ID:</label>
        <input type="text" id="idInput" placeholder="Enter new ID">
        <button onclick="replaceId()">Generate URI</button>
        <pre id="output"></pre>
        <button id="copyButton" class="copy-button" onclick="copyUri()">
            Copy URI
        </button>
    </div>
</body>
</html>
