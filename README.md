<!DOCTYPE html>
<html lang="or">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bro - Tuma Smart Sathi</title>
    <style>
        body { font-family: Arial, sans-serif; background-color: #121212; color: white; margin: 0; padding: 0; display: flex; flex-direction: column; height: 100vh; }
        .header { background-color: #1f1f1f; padding: 15px; text-align: center; font-size: 24px; font-weight: bold; border-bottom: 1px solid #333; }
        .chat-box { flex: 1; padding: 20px; overflow-y: auto; display: flex; flex-direction: column; gap: 10px; }
        .message { padding: 10px 15px; border-radius: 15px; max-width: 80%; line-height: 1.4; }
        .bot { background-color: #333; align-self: flex-start; border: 1px solid #444; }
        .user { background-color: #007bff; align-self: flex-end; }
        .input-area { display: flex; padding: 10px; background-color: #1f1f1f; border-top: 1px solid #333; }
        input { flex: 1; padding: 12px; border: none; border-radius: 5px; outline: none; background: #333; color: white; margin-right: 10px; font-size: 16px; }
        button { padding: 12px 20px; border: none; background-color: #007bff; color: white; border-radius: 5px; cursor: pointer; font-size: 16px; font-weight: bold; }
    </style>
</head>
<body>
    <div class="header">Bro 🤝 (AI)</div>
    <div class="chat-box" id="chat-box">
        <div class="message bot">Bhai, mu "Bro". Ebe mu pura smart heigaichi. Tume gapa suniba, kasta share kariba ba jaha chahiba amey katha heba. Kuha kana heichi?</div>
    </div>
    <div class="input-area">
        <input type="text" id="user-input" placeholder="Tuma katha lekhantu...">
        <button onclick="sendMessage()">Send</button>
    </div>

    <script>
        // TALA LINE RE "EITHI_TUMA_API_KEY_PAKAO" JAGA RE TUMA COPY KARITHIBA API KEY PASTE KARA (Inverted comma "" bhitare rakhiba)
        const API_KEY = "AQ.Ab8RN6IGGLVfdfsn-ecZF2U7tuqRLRSK_0Q9Key5Pu7qC6P-8Q"; 

        async function sendMessage() {
            let inputField = document.getElementById("user-input");
            let input = inputField.value;
            if (input.trim() === "") return;

            let chatBox = document.getElementById("chat-box");
            
            chatBox.innerHTML += `<div class="message user">${input}</div>`;
            inputField.value = "";
            chatBox.scrollTop = chatBox.scrollHeight;

            let botDiv = document.createElement("div");
            botDiv.className = "message bot";
            botDiv.innerText = "Bro bhabuchi...";
            chatBox.appendChild(botDiv);
            chatBox.scrollTop = chatBox.scrollHeight;

            try {
                let response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${API_KEY}`, {
                    method: "POST",
                    headers: { "Content-Type": "application/json" },
                    body: JSON.stringify({
                        contents: [{
                            parts: [{ text: `Tuma naa 'Bro'. Tume gote close Odia sanga. User breakup re kasta pauchi ba advice maguchi. Sabu reply strictly Odia bhasa re (kintu English alphabet/Latin script re) daba. Basic, friendly au bhai bhalia katha heba. User ra katha: ${input}` }]
                        }]
                    })
                });

                let data = await response.json();
                botDiv.innerText = data.candidates[0].content.parts[0].text;
            } catch (error) {
                botDiv.innerText = "Bhai, network re kichi problem achi. Puni try kara.";
            }
            chatBox.scrollTop = chatBox.scrollHeight;
        }
    </script>
</body>
</html>
