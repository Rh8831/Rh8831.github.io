<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Replace ID in JSON</title>
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

    .button-group {
        display: flex;
        justify-content: space-between;
        margin-bottom: 20px;
    }

    .button-group button {
        background-color: #00796b;
        color: #fff;
        border: 2px solid transparent;
        border-radius: 5px;
        padding: 12px;
        cursor: pointer;
        font-size: 16px;
        transition: background-color 0.3s ease, transform 0.3s ease, border-color 0.3s ease;
        width: 30%;
    }

    .button-group button:hover {
        background-color: #004d40;
        transform: scale(1.05);
    }

    .button-group button:active {
        background-color: #00796b;
        transform: scale(1);
    }

    .button-group button.selected {
        background-color: #851355;
    }

    button.replace-btn {
        background-color: #00796b;
        color: #fff;
        border: none;
        border-radius: 5px;
        padding: 12px 0;
        width: 100%;
        cursor: pointer;
        font-size: 16px;
        transition: background-color 0.3s ease;
    }

    button.replace-btn:hover {
        background-color: #004d40;
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
        background-color: #00796b;
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
        background-color: #004d40;
    }

    .copy-icon {
        margin-right: 10px;
    }
</style>

<script>
    var packets = "1-2";
    var length = "50-100";
    var interval = "3-5";

    function setWifiValues() {
        packets = "1-3";
        length = "50-100";
        interval = "3-5";
        highlightButton('wifi');
    }

    function setMciValues() {
        packets = "1-2";
        length = "20-50";
        interval = "10-15";
        highlightButton('mci');
    }

    function setMtnValues() {
        packets = "1-5";
        length = "100-150";
        interval = "10-15";
        highlightButton('mtn');
    }

    function highlightButton(buttonId) {
        var buttons = document.querySelectorAll('.button-group button');
        buttons.forEach(button => button.classList.remove('selected'));
        document.getElementById(buttonId).classList.add('selected');
    }

    function replaceId() {
        var idInput = document.getElementById("idInput").value;
        var id = extractId(idInput);

        if (id) {
            var jsonData = JSON.parse(`{
                "remarks": "90z944qb (IRCF Fragment)",
                "log": {
                    "access": "",
                    "error": "",
                    "loglevel": "warning"
                },
                "inbounds": [
                    {
                        "tag": "socks",
                        "port": 10808,
                        "listen": "127.0.0.1",
                        "protocol": "socks",
                        "sniffing": {
                            "enabled": true,
                            "destOverride": [
                                "http",
                                "tls"
                            ],
                            "routeOnly": false
                        },
                        "settings": {
                            "auth": "noauth",
                            "udp": true,
                            "allowTransparent": false
                        }
                    },
                    {
                        "tag": "http",
                        "port": 10809,
                        "listen": "127.0.0.1",
                        "protocol": "http",
                        "sniffing": {
                            "enabled": true,
                            "destOverride": [
                                "http",
                                "tls"
                            ],
                            "routeOnly": false
                        },
                        "settings": {
                            "auth": "noauth",
                            "udp": true,
                            "allowTransparent": false
                        }
                    }
                ],
                "outbounds": [
                    {
                        "tag": "proxy",
                        "protocol": "vless",
                        "settings": {
                            "vnext": [
                                {
                                    "address": "cdn.discordapp.com",
                                    "port": 8880,
                                    "users": [
                                        {
                                            "id": "${id}",
                                            "alterId": 0,
                                            "email": "t@t.tt",
                                            "security": "auto",
                                            "encryption": "none",
                                            "flow": ""
                                        }
                                    ]
                                }
                            ]
                        },
                        "streamSettings": {
                            "network": "ws",
                            "wsSettings": {
                                "path": "/asrnovin-ArV2ray,asrnovin-ArV2ray,asrnovin-ArV2ray,asrnovin-ArV2ray,asrnovin-ArV2ray,asrnovin-ArV2ray,asrnovin-ArV2ray,asrnovin-ArV2ray,asrnovin-ArV2ray,asrnovin-ArV2ray,asrnovin-ArV2ray,asrnovin-ArV2ray?ed=2048",
                                "headers": {
                                    "Host": "2.V2ray.debian.org.fxp.debian.org.speedtest.net.らわなさらわ.drinternet.host"
                                }
                            },
                            "sockopt": {
                                "dialerProxy": "fragment",
                                "tcpKeepAliveIdle": 100,
                                "mark": 255,
                                "tcpNoDelay": true
                            }
                        }
                    },
                    {
                        "tag": "fragment",
                        "protocol": "freedom",
                        "settings": {
                            "domainStrategy": "AsIs",
                            "fragment": {
                                "packets": "${packets}",
                                "length": "${length}",
                                "interval": "${interval}"
                            }
                        },
                        "streamSettings": {
                            "sockopt": {
                                "tcpNoDelay": true,
                                "tcpKeepAliveIdle": 100
                            }
                        }
                    },
                    {
                        "tag": "direct",
                        "protocol": "freedom",
                        "settings": {}
                    },
                    {
                        "tag": "block",
                        "protocol": "blackhole",
                        "settings": {
                            "response": {
                                "type": "http"
                            }
                        }
                    }
                ],
                "routing": {
                    "domainStrategy": "AsIs",
                    "rules": [
                        {
                            "type": "field",
                            "inboundTag": [
                                "api"
                            ],
                            "outboundTag": "api",
                            "enabled": true
                        },
                        {
                            "id": "5627785659655799759",
                            "type": "field",
                            "port": "0-65535",
                            "outboundTag": "proxy",
                            "enabled": true
                        }
                    ]
                }
            }`);

            document.getElementById("output").innerText = JSON.stringify(jsonData, null, 4);
            document.getElementById("output").style.display = "block"; // Display the JSON output
            document.getElementById("copyButton").style.display = "block"; // Display the "Copy JSON" button
        } else {
            alert("Invalid ID input! Please provide a valid ID.");
        }
    }
    
    function extractId(input) {
        var match = input.match(/[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}/);
        return match ? match[0] : null;
    }
    
    function copyJson() {
        var copyText = document.getElementById("output");
        var range = document.createRange();
        range.selectNode(copyText);
        window.getSelection().removeAllRanges();
        window.getSelection().addRange(range);
        document.execCommand("copy");
        window.getSelection().removeAllRanges();
        alert("Copied JSON to clipboard!");
    }
</script>
</head>
<body>
    <div class="container">
        <h2>Replace ID in JSON</h2>
        <label for="idInput">Enter new ID:</label>
        <input type="text" id="idInput" placeholder="Enter new ID">
        <div class="button-group">
            <button id="wifi" onclick="setWifiValues()">Wifi</button>
            <button id="mci" onclick="setMciValues()">MCI</button>
            <button id="mtn" onclick="setMtnValues()">MTN</button>
        </div>
        <button class="replace-btn" onclick="replaceId()">Replace ID</button>
        <pre id="output"></pre>
        <button id="copyButton" class="copy-button" onclick="copyJson()">
            <i class="fas fa-copy copy-icon"></i>Copy JSON
        </button>
    </div>
</body>
</html>
