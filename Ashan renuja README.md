- 👋 Hi, I’m @summerbaby121
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
summerbaby121/summerbaby121 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
from flask import Flask, request
import requests

app = Flask(__name__)

@app.route('/webhook', methods=['POST'])
def webhook():
    data = request.json
    phone_number = data['messages'][0]['from']
    message = data['messages'][0]['text']['body']

    # Response logic
    reply = "Hello! I'm your bot. You said: " + message

    # Send a response via WhatsApp API
    send_message(phone_number, reply)
    return "Message Sent"

def send_message(to, message):
    url = "https://api.twilio.com/your-api-endpoint"
    payload = {
        "to": to,
        "message": message
    }
    headers = {"Authorization": "Bearer your_api_key"}
    requests.post(url, json=payload, headers=headers)

if __name__ == '__main__':
    app.run(port=5000)
    
