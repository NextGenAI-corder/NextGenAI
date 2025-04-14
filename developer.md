### LINE BOT構築に関する重要な補足（2025年4月以降）

2024年以降、LINE Developers から Messaging API チャネルを直接作成・設定することはできなくなりました。  
これにより、LINE BOTの初期構築手順が一部変更されています。

---

#### ✅ Messaging API の有効化について

BOTを有効にするには、以下の手順が必須です：

1. [LINE Official Account Manager](https://manager.line.biz) にログイン  
2. 対象のアカウントを開く  
3. メニューから「Messaging API」設定画面へ  
4. 「Messaging API を有効にする」を ON にする  
5. プライバシーポリシー・利用規約のURLを登録  
   （GitHubなどで公開ページを作成してください）

---

#### ✅ アクセストークンの取得

Messaging API 有効化が完了すると、  
[LINE Developers Console](https://developers.line.biz/console/) にて  
チャネルアクセストークン（ロングターム）を発行できるようになります。

🔗 [公式ドキュメント：アクセストークン取得手順](https://developers.line.biz/en/docs/messaging-api/channel-access-tokens/)

---

> ⚠ ご注意：この仕様変更により、開発初期段階でつまずく読者が増えています。  
> 最新手順は本GitHub上で随時更新していますので、書籍と合わせてご確認ください。

---

📘 Gitが初めての方でも、リンクをクリックして開くだけで読める形式にしています。  
できる限り丁寧にまとめていきますので、どうぞご安心ください。
