<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Generate VLESS URLs</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #e3f2fd;
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
            animation: fadeIn 0.5s ease-in-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        h2 {
            color: #00796b;
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
            transition: border-color 0.3s ease;
        }

        input[type="text"]:focus {
            border-color: #00796b;
        }

        button {
            background-color: #00796b;
            color: #fff;
            border: none;
            border-radius: 5px;
            padding: 12px 0;
            width: 100%;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s ease;
            margin-bottom: 20px;
        }

        button:hover {
            background-color: #004d40;
        }

        #vlessUrls {
            display: none;
            background-color: #f8f9fa;
            padding: 20px;
            border-radius: 5px;
            white-space: pre-wrap;
            color: #495057;
            overflow-x: auto;
            margin-top: 20px;
            text-align: left;
        }

        #copyAllBtn {
            display: none;
            background-color: #00796b;
            color: #fff;
            border: none;
            border-radius: 5px;
            padding: 12px 0;
            width: 100%;
            cursor: pointer;
            font-size: 16px;
            margin-top: 20px;
            transition: background-color 0.3s ease;
        }

        #copyAllBtn:hover {
            background-color: #004d40;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Generate VLESS URLs</h2>
        <label for="uuid">UUID:</label>
        <input type="text" id="uuid" name="uuid" required>
        <button type="button" onclick="generateVlessUrls()">Generate VLESS URLs</button>

        <div id="vlessUrls"></div>
        <button id="copyAllBtn" onclick="copyAllToClipboard()">Copy All Configurations</button>
    </div>

    <script>
        // Hardcoded IP database
        const ipDatabase = [
            "170.238.234.217",
            "92.223.76.30",
            "92.223.116.233",
            "41.210.189.22",
            "92.38.168.14",
            "92.223.76.23",
            "80.93.215.6",
            "5.101.219.5",
            "92.223.116.227",
            "46.49.10.237",
            "185.76.48.122"
        ];

        function generateVlessUrls() {
            const uuidInput = document.getElementById('uuid');
            const uuid = uuidInput.value.trim();

            // Validate UUID format
            if (!isValidUUID(uuid)) {
                alert("Please enter a valid UUID.");
                return;
            }

            const port = "80";
            const encryption = "none";
            const security = "none";
            const type = "ws";
            const host = "pentaserver.ir";
            const path = "%2Fasrnovin-Speed%2Casrnovin-Speed%2Casrnovin-Speed%2Casrnovin-Speed%2Casrnovin-Speed%2Casrnovin-Speed%2Casrnovin-Speed%2Casrnovin-Speed%2Casrnovin-Speed%2Casrnovin-Speed%2Casrnovin-Speed%2Casrnovin-Speed%2Cwp-admin%3Fed%3D2048";

            let vlessUrlsHTML = "";

            for (let i = 0; i < ipDatabase.length; i++) {
                const ip = ipDatabase[i];
                const configNumber = i + 1;
                const fragment = `Config${configNumber}`;
                const vlessUrl = `vless://${uuid}@${ip}:${port}?encryption=${encryption}&security=${security}&type=${type}&host=${host}&path=${path}#${fragment}`;
                vlessUrlsHTML += `<p>${vlessUrl}</p>`;
            }

            const vlessUrlsDiv = document.getElementById('vlessUrls');
            vlessUrlsDiv.innerHTML = vlessUrlsHTML;
            vlessUrlsDiv.style.display = 'block';

            const copyAllBtn = document.getElementById('copyAllBtn');
            copyAllBtn.style.display = 'block';
        }

        function isValidUUID(uuid) {
            const uuidRegex = /^[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}$/;
            return uuidRegex.test(uuid);
        }

        function copyAllToClipboard() {
            const vlessUrlsDiv = document.getElementById('vlessUrls');
            const tempInput = document.createElement('textarea');
            const urls = Array.from(vlessUrlsDiv.querySelectorAll('p')).map(p => p.innerText).join('\n');
            tempInput.value = urls;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand('copy');
            document.body.removeChild(tempInput);
            alert('All configurations copied to clipboard');
        }
    </script>
</body>
</html>
