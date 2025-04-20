3．JSONファイルからプロンプトを取り込む
プロンプトをさらに精妙に書けばChatGPTがそれに応えてBotも貴方の意思に忠実に答えます。
ここでは、JSONファイルに条件毎の回答を設定しコードで読ませてプロンプトを取り込む方法を紹介します。

条件毎の応答を設定したJSONの例
![image](https://github.com/user-attachments/assets/98ae4eff-9e53-428f-908f-fb501dd30ae9)
Q&Aを設定したテキストファイル

![image](https://github.com/user-attachments/assets/89b97b8a-27de-4dd1-b539-4902294372c9)


Python版
Code9-1
```python
import json

def load_prompt(filename):
    with open(filename, encoding="utf-8") as f:
        return json.load(f)

def get_response(prompt_data, user_input):
    for item in prompt_data:
        if item["条件"] in user_input:
            return item["応答"]
    return "すみません、その質問にはまだ対応していません。"

if __name__ == "__main__":
    prompt_data = load_prompt("prompt_data.json")
    user_input = input("質問をどうぞ：")
    response = get_response(prompt_data, user_input)
    print("BOTの応答：", response)
```
Go版
Code9-2
```
package main

import (
	"encoding/json"
	"fmt"
	"os"
	"strings"
)

type QA struct {
	Condition string `json:"条件"`
	Response  string `json:"応答"`
}

func main() {
	data, err := os.ReadFile("prompt_data.json")
	if err != nil {
		panic(err)
	}

	var qas []QA
	if err := json.Unmarshal(data, &qas); err != nil {
		panic(err)
	}

	fmt.Print("質問をどうぞ：")
	var input string
	fmt.Scanln(&input)

	for _, qa := range qas {
		if strings.Contains(input, qa.Condition) {
			fmt.Println("BOTの応答：", qa.Response)
			return
		}
	}
	fmt.Println("すみません、その質問にはまだ対応していません。")
}
```
