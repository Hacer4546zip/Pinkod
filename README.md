<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Matn Yuborish Dasturi</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        input, button {
            margin: 5px 0;
            padding: 10px;
            width: 300px;
        }
        #messageContainer {
            margin-top: 20px;
            border: 1px solid #ccc;
            padding: 10px;
            max-height: 200px;
            overflow-y: auto;
        }
        .message {
            margin: 5px 0;
            padding: 5px;
            background-color: #f0f0f0;
        }
    </style>
</head>
<body>
    <h1>Foydalanuvchilarga Matn Yuborish</h1>
    <input type="text" id="inputField" placeholder="Matn yozing...">
    <button onclick="sendMessage()">Yuborish</button>
    <h2>Qabul qilingan Matnlar:</h2>
    <div id="messageContainer"></div>

    <script>
        // Broadcast Channel yaratish
        const channel = new BroadcastChannel('my_channel');

        // Jo'natish funksiyasi
        function sendMessage() {
            const inputData = document.getElementById('inputField').value;
            if (inputData) {
                channel.postMessage(inputData); // Xabarni jo'natish
                document.getElementById('inputField').value = ''; // Inputni tozalash
            }
        }

        // Qabul qilish funksiyasi
        channel.onmessage = function(event) {
            const messageContainer = document.getElementById('messageContainer');
            const newMessage = document.createElement('div');
            newMessage.className = 'message';
            newMessage.textContent = event.data; // Qabul qilingan xabarni ko'rsatish
            messageContainer.appendChild(newMessage); // Yangi xabarni ko'rsatish
            messageContainer.scrollTop = messageContainer.scrollHeight; // Oxirgi xabar ko'rinadi
        };
    </script>
</body>
</html>
