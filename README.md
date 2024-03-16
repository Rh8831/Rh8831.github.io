<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Replace ID in JSON</title>
<style>
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
        background-color: #f9f9ed; /* Dark Charcoal */
        color: #3F418D; /* Bright Yellow */
    }
    .container {
        max-width: 600px;
        margin: 50px auto;
        padding: 20px;
        background-color: #f9f9ed; /* Dark Charcoal */
        border-radius: 5px;
        box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    h2 {
        text-align: center;
        color: #3F418D; /* Bright Yellow */
    }
    label {
        font-weight: bold;
        margin-bottom: 10px;
        display: block;
        color: #3F418D; /* Bright Yellow */
    }
    input[type="text"] {
        width: 100%;
        padding: 10px;
        margin-bottom: 20px;
        border: 1px solid #3F418D; /* Bright Yellow */
        border-radius: 3px;
        background-color: #f9f9ed; /* Dark Charcoal */
        color: #3F418D; /* Bright Yellow */
    }
    button {
        display: block;
        width: 100%;
        padding: 10px;
        color: #f9f9ed; /* Dark Charcoal */
        background-color: #3F418D; /* Bright Yellow */
        border: none;
        border-radius: 3px;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }
    button:hover {
        background-color: #3F418D; /* Darker Yellow */
    }
    pre {
        background-color: #f9f9ed; /* Dark Charcoal */
        padding: 20px;
        border-radius: 3px;
        white-space: pre-wrap;
        color: #3F418D; /* Bright Yellow */
    }
    .copy-button {
        display: none;
        width: 100%;
        padding: 10px;
        margin-top: 20px;
        color: #f9f9ed; /* Dark Charcoal */
        background-color: #3F418D; /* Bright Yellow */
        border: none;
        border-radius: 3px;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }
    .copy-button:hover {
        background-color: #3F418D; /* Darker Yellow */
    }
</style><script>
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
            document.getElementById("copyButton").style.display = "block";
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
        <input type="text" id="idInput">
        <button onclick="replaceId()">Replace ID</button>
        <pre id="output"></pre>
        <button id="copyButton" class="copy-button" onclick="copyJson()">Copy JSON</button>
    </div>
</body>
</html>
