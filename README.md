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

    .copy-icon {
        margin-right: 10px;
    }
</style>

<script>
    function replaceId() {
        var userInput = document.getElementById("idInput").value;
        var id = extractId(userInput);
        if (id) {
            var jsonData = JSON.parse(`{
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
                                    "port": 443,
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
                            "security": "tls",
                            "tlsSettings": {
                                "allowInsecure": true,
                                "serverName": "tr-speed-iran-mobile-digikala.drinternet.space",
                                "alpn": [
                                    "h2",
                                    "http/1.1"
                                ],
                                "fingerprint": "chrome",
                                "show": false
                            },
                            "wsSettings": {
                                "path": "/ws",
                                "headers": {
                                    "Host": "tr-speed-iran-mobile-digikala.drinternet.space"
                                }
                            },
                            "sockopt": {
                                "dialerProxy": "fragment",
                                "tcpKeepAliveIdle": 100,
                                "mark": 255
                            }
                        },
                        "mux": {
                            "enabled": false,
                            "concurrency": -1
                        }
                    },
                    {
                        "tag": "fragment",
                        "protocol": "freedom",
                        "settings": {
                            "fragment": {
                                "packets": "tlshello",
                                "length": "10-20",
                                "interval": "10-20"
                            }
                        },
                        "streamSettings": {
                            "sockopt": {
                                "TcpNoDelay": true,
                                "tcpKeepAliveIdle": 100,
                                "mark": 255
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
                            "id": "5465425548310166497",
                            "type": "field",
                            "outboundTag": "direct",
                            "domain": [
                                "domain:ir",
                                "geosite:cn"
                            ],
                            "enabled": true
                        },
                        {
                            "id": "5425034033205580637",
                            "type": "field",
                            "outboundTag": "direct",
                            "ip": [
                                "geoip:private",
                                "geoip:cn",
                                "geoip:ir"
                            ],
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
            alert("Invalid input! Please provide a valid ID.");
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
        <button onclick="replaceId()">Replace ID</button>
        <pre id="output"></pre>
        <button id="copyButton" class="copy-button" onclick="copyJson()">
            <i class="fas fa-copy copy-icon"></i>Copy JSON
        </button>
    </div>
</body>
</html>
