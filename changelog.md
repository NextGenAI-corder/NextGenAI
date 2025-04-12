### 2025年4月7日版 【誤記訂正】
- 第5章、6章のX Bot開発の本文中Webhookという文字を排除し、修正しました。
- Code5-1
  - 改定前：Webhookで受信
  - 改定後：X APIで受信
- Code5-2
  - 改定前：Webhookで送信
  - 改定後：X APIで送信
 - Code6-2
   - 改定前：Webhook受信ハンドラー
   - 改定後：メンション受信ハンドラー
 - Code6-3
   - 改定前：Webhookで受信 
   - 改定後：X APIでメンションを受け取る
 - Code6-4
   - 改定前：LINE向け送信処理 
   - 改定後：X向け送信処理に修正
 - Code6-5
   - 改定前：Webhookサーバー起動
   - 改定後：X Botサーバー起動に修正
#### 例
- Code5-1
  - 改定前
  ```
  def get_mentions():
    headers = {"Authorization": f"Bearer {BEARER_TOKEN}"}
    url = "https://api.twitter.com/2/tweets/search/recent?query=@your_bot_handle"
    
    res = requests.get(url, headers=headers)
    return res.json().get("data", [])
  ```
  - 改定後
  ```
  def get_mentions():
    headers = {"Authorization": f"Bearer {BEARER_TOKEN}"}
    url = "https://api.twitter.com/2/tweets/search/recent?query=@your_bot_handle"
    
    res = requests.get(url, headers=headers)
    return res.json().get("data", [])
  ```
 - Code5-2
   - 改定前
   ```
   def send_reply(reply_token, message):
       payload = {
          "replyToken": reply_token,
          "messages": [{"type": "text", "text": message}]
       }
       jsonData, _ := json.Marshal(payload)
       req, _ := http.NewRequest("POST", "https://api.twitter.com/2/direct_messages/events/new.json", 
       bytes.NewBuffer(jsonData))
       req.Header.Set("Content-Type", "application/json")
       req.Header.Set("Authorization", "Bearer " + bearerToken)
    ```
   - 修正後
   ```
   def send_reply(tweet_id, message):
       headers = {
        "Authorization": f"Bearer {BEARER_TOKEN}",
        "Content-Type": "application/json"
       }
       payload = {
        "text": message,
        "reply": {"in_reply_to_tweet_id": tweet_id}
       }
       url = "https://api.twitter.com/2/tweets"
       requests.post(url, headers=headers, json=payload)
    ```
