LINEのWebhook検証では、"events" フィールドを含まないダミーPOSTが送られます。  
このため、初期コードにある以下のような記述では KeyError が発生し、検証が失敗します。

---

## ✅ 修正版コード（Flask対応）

```python
@app.route("/", methods=["POST"])
def webhook():
    data = request.get_json()
    print("受信データ:", data)

    if not data.get("events"):
        return "NO EVENTS", 200

    try:
        user_message = data["events"][0]["message"]["text"]
        reply_token = data["events"][0]["replyToken"]

        response_text = chat_with_gpt(user_message)

        headers = {
            "Content-Type": "application/json",
            "Authorization": f"Bearer {LINE_ACCESS_TOKEN}"
        }

        body = {
            "replyToken": reply_token,
            "messages": [{
                "type": "text",
                "text": response_text
            }]
        }

        requests.post(
            "https://api.line.me/v2/bot/message/reply",
            headers=headers,
            data=json.dumps(body)
        )

    except Exception as e:
        print("エラー:", e)
        return "ERROR", 200
```
📌 補足事項
$ ngrok http 5000 実行後に表示されるURL（例：https://xxxx.ngrok.io）に /webhook を付けて
　LINE Developers の「Webhook URL」欄に設定してください。
