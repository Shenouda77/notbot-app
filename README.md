<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>$NOTBOT Reclaimer</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #0d1117;
            color: #ffffff;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            text-align: center;
        }
        .container {
            background: #161b22;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            border: 1px solid #30363d;
            width: 90%;
            max-width: 400px;
        }
        h1 { color: #58a6ff; }
        button {
            background-color: #238636;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            font-size: 16px;
            cursor: pointer;
            margin-top: 20px;
            width: 100%;
        }
        button:hover { background-color: #2ea043; }
        #status { margin-top: 20px; font-size: 14px; color: #8b949e; }
    </style>
</head>
<body>

<div class="container">
    <h1>$NOTBOT Reclaimer</h1>
    <p>Unlock trapped SOL from empty accounts instantly.</p>
    <button id="connectBtn">Connect Wallet</button>
    <div id="status">Waiting for connection...</div>
</div>

<script>
    const connectBtn = document.getElementById('connectBtn');
    const statusDiv = document.getElementById('status');

    async function connectWallet() {
        // 1. التحقق إذا كانت المحفظة مثبته في المتصفح الحالي (حالة الكمبيوتر أو متصفح فانتوم)
        if (window.solana && window.solana.isPhantom) {
            try {
                const resp = await window.solana.connect();
                statusDiv.innerText = "Connected: " + resp.publicKey.toString().slice(0, 8) + "...";
                statusDiv.style.color = "#3fb950";
                // هنا يمكنك إضافة كود إرسال العنوان للسيرفر
            } catch (err) {
                statusDiv.innerText = "Connection rejected by user.";
                statusDiv.style.color = "#f85149";
            }
        } 
        // 2. إذا لم نجد المحفظة (أنت في متصفح تيليجرام)، قم بالتحويل لمتصفح فانتوم
        else {
            statusDiv.innerText = "Redirecting to Phantom Browser...";
            const currentUrl = window.location.href;
            // هذا الرابط هو السحر الذي يفتح تطبيق فانتوم مباشرة
            const deepLink = `https://phantom.app/ul/browse/${encodeURIComponent(currentUrl)}`;
            window.location.href = deepLink;
        }
    }

    connectBtn.addEventListener('click', connectWallet);
</script>

</body>
</html>
