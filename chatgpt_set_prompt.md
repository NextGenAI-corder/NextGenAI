Code3-1(app.py)、他ChatGPT連携関数及びprompt設定部分
```python
# 🤖 ChatGPTとやり取りする関数（シンプルなプロンプト処理）
def chat_with_gpt(message):
    response = openai.Completion.create(
        model="gpt-3.5-turbo",  # 使用するOpenAIモデル
        prompt="応答メッセージ",  # ユーザーのメッセージを入力として送る
        max_tokens=50           # 応答の最大トークン数
    )
    return response.choices[0].text.strip()
```
このpromptの部分を以下の様に設定すると
prompt = f"私は今日は夜勤なので返信できない状況です。以下のメッセージにその旨を添えて返答してください：{message}"

相手が「今ひま？」と送った場合、BOTは
「ごめん！今日は夜勤なので翌朝まで返信できません。」のように自動で返してくれます。
つまり、あなたの思いや設定をプロンプトに込めることで、あなたの分身のようなBOTが
LINE上で自然に応答するようになるのです。
また、このChatGPT連携部分のプロンプト設定は方法はXでも、またPythonでもGoでも基本的に同じです。
