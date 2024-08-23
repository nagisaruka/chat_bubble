<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>リアルタイムチャット</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: transparent;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            color: #ffe596;
        }

        .chat-container {
            width: 250px;
            height: 450px;
            background-color: #384559;
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        .chat-window {
            padding: 5px;
            flex-grow: 1;
            overflow-y: auto;
            display: flex;
            flex-direction: column-reverse;
        }

        .chat-bubble {
            max-width: 75%;
            margin-bottom: 5px;
            padding: 8px;
            font-size: 12px;
            border-radius: 12px;
            background-color: #384559;
            color: #ffe596;
            position: relative;
            opacity: 1;
            transition: opacity 1s ease-out;
            border: 1px solid #ffe596;
            word-wrap: break-word;
        }

        .chat-bubble.user {
            align-self: flex-end;
        }

        .chat-bubble.fade-out {
            opacity: 0;
        }

        .input-container {
            display: flex;
            border-top: 1px solid #ffe596;
            padding: 5px;
            background-color: #384559;
            border-bottom-left-radius: 10px;
            border-bottom-right-radius: 10px;
        }

        .input-container input {
            flex-grow: 1;
            border: 1px solid #ffe596;
            padding: 5px;
            font-size: 12px;
            border-radius: 15px;
            margin-right: 5px;
            background-color: #384559;
            color: #ffe596;
        }

        .input-container button {
            padding: 5px 10px;
            font-size: 12px;
            border: 1px solid #ffe596;
            background-color: #384559;
            color: #ffe596;
            border-radius: 15px;
            cursor: pointer;
        }
    </style>
</head>
<body>

<div class="chat-container">
    <div class="chat-window" id="chat-window"></div>
    <div class="input-container">
        <input type="text" id="chat-input" placeholder="メッセージを入力...">
        <button onclick="sendMessage()">送信</button>
    </div>
</div>

<script>
    const chatWindow = document.getElementById('chat-window');
    const chatInput = document.getElementById('chat-input');
    let messages = [];

    function sendMessage() {
        const text = chatInput.value.trim();
        if (text === "") return;

        const bubble = document.createElement('div');
        bubble.className = 'chat-bubble user';
        bubble.textContent = text;

        chatWindow.insertBefore(bubble, chatWindow.firstChild);
        messages.push(bubble);

        // チャット欄がいっぱいになったら最初のチャットをフェードアウト
        if (chatWindow.scrollHeight > chatWindow.clientHeight) {
            const oldMessage = messages.shift();
            oldMessage.classList.add('fade-out');
            setTimeout(() => oldMessage.remove(), 1000); // フェードアウト後に削除
        }

        chatInput.value = '';
    }

    chatInput.addEventListener('keypress', function (e) {
        if (e.key === 'Enter') {
            sendMessage();
        }
    });
</script>

</body>
</html>
# chat_bubble
