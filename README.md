<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Check IP</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        body { font-family: sans-serif; text-align: center; padding: 20px; background-color: #f0f0f0; }
        .loader { font-size: 18px; font-weight: bold; color: #333; }
        #status { margin-top: 20px; color: green; font-weight: bold; }
    </style>
</head>
<body>
    <h3>Đang xác thực thiết bị...</h3>
    <div class="loader" id="loader">Vui lòng đợi...</div>
    <div id="status"></div>

    <script>
        let tg = window.Telegram.WebApp;
        tg.expand();

        async function getIP() {
            try {
                const response = await fetch('https://api.ipify.org?format=json');
                const data = await response.json();
                const userIp = data.ip;

                document.getElementById('loader').innerText = "IP của bạn: " + userIp;
                
                const sendData = JSON.stringify({
                    ip: userIp,
                    timestamp: Date.now()
                });

                tg.sendData(sendData);
                
            } catch (error) {
                document.getElementById('loader').innerText = "Lỗi! Vui lòng tắt VPN/4G và thử lại.";
            }
        }
        getIP();
    </script>
</body>
</html>
