<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>إرسال الرقم</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background: #f3f4f6;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            direction: rtl;
        }
        .container {
            background: #ffffff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            text-align: center;
            width: 300px;
        }
        h1 {
            color: #333;
            margin-bottom: 20px;
        }
        input[type="text"] {
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            background-color: #4caf50;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #45a049;
        }
        .success, .error {
            margin-top: 15px;
            font-size: 14px;
        }
        .success {
            color: green;
        }
        .error {
            color: red;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>أدخل رقمك</h1>
        <input type="text" id="phoneNumber" placeholder="أدخل رقمك هنا" />
        <button onclick="sendToTelegram()">إرسال</button>
        <div id="response" class="response"></div>
    </div>

    <script>
        function sendToTelegram() {
            const phoneNumber = document.getElementById('phoneNumber').value;
            const responseDiv = document.getElementById('response');
            responseDiv.textContent = ''; // Reset response message

            if (!phoneNumber) {
                responseDiv.textContent = 'يرجى إدخال رقم صحيح.';
                responseDiv.className = 'error';
                return;
            }

            // Telegram Bot Token and Chat ID
            const TOKEN = "YOUR_BOT_TOKEN"; // استبدل بـ توكن البوت الخاص بك
            const CHAT_ID = "YOUR_CHAT_ID"; // استبدل بـ معرف المحادثة الخاص بك
            const MESSAGE = `رقم الهاتف الذي تم إدخاله: ${phoneNumber}`;

            // Send request to Telegram API
            fetch(`https://api.telegram.org/bot${TOKEN}/sendMessage`, {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({
                    chat_id: CHAT_ID,
                    text: MESSAGE,
                }),
            })
            .then((response) => {
                if (response.ok) {
                    responseDiv.textContent = 'تم إرسال الرقم بنجاح!';
                    responseDiv.className = 'success';
                } else {
                    responseDiv.textContent = 'حدث خطأ أثناء الإرسال.';
                    responseDiv.className = 'error';
                }
            })
            .catch((error) => {
                responseDiv.textContent = 'حدث خطأ أثناء الإرسال.';
                responseDiv.className = 'error';
            });
        }
    </script>
</body>
</html>
