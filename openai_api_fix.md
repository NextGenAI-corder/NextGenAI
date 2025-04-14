## OpenAI API v1.0以降への対応について

---

### ❗修正：`openai.Completion.create()` の廃止

書籍および初期コードにて、以下の記述が使用されています：

```python
response = openai.Completion.create(
    model="gpt-3.5-turbo",
    prompt="こんにちは",
    max_tokens=50
)
```
このコードは openai>=1.0.0 では使用できず、実行時にエラーとなります。

✅ 修正後コード（最新版対応）
OpenAIライブラリ v1.0.0 以降では、以下のように書き換えてください：
```python
from openai import OpenAI
client = OpenAI(api_key="YOUR_OPENAI_API_KEY")

response = client.chat.completions.create(
    model="gpt-3.5-turbo",
    messages=[{"role": "user", "content": message}],
    max_tokens=50
)
```
📘 本書記載コードを使用する場合は、ライブラリを v1.0 以降で運用する前提で、
必ずこの修正を行ってください。
