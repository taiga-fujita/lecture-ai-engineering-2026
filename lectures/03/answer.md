# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：
素のLLMは、AIを扱うにあたっての一般論的な回答であったが、エージェントは、この講義に即した内容になっている。
- `--trace` で見えたツール呼び出し（ツール名と引数）：
| ツール名 | 引数 |
| --- | --- |
| search_glossary | ({'query': 'LoRA'}) |
| search_glossary | ({'query': 'QLoRA'}) |
- 1つの質問での LLM 呼び出し回数（`requests`）：2回
- 追加したツールと、docstring に書いた説明：
def make_quiz(lecture: int) -> str:
    """指定した回の用語集からランダムに用語を選んでクイズを作る。

    「第2回の確認問題を出して」のように、復習用の問題を求められた時に使う
    """
    terms = [term for term in load_glossary() if term["lecture"] == lecture]
    if not terms:
        return f"第{lecture}回の用語は用語集にありません。"
    term = random.choice(terms)
    question = f"「{term['term']}」とは何ですか？"
    print(question)
    show_answer = input("答えを表示するには yes と入力してください: ").strip().casefold() == "yes"
    quiz = {"question": question}
    if show_answer:
        quiz["answer"] = term["definition"]
        print(f"答え: {term['definition']}")
    return json.dumps([quiz], ensure_ascii=False)

## 宿題

- 取り組んだレベル：基礎
- やったこと：
- 結果：
- 気づき・疑問：
