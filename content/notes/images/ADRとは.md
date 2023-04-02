---
title: ADRとは
date: "2023-02-02"
---

## 概要

Architectural Decision Records の略で、Michael Nygard 氏（以下、マイケル）が発案したんだ。

マイケルは、アメリカのソフトウェア開発者で特に大規模なシステムの設計や運用に関する専門家として知られているよ。

彼は、「Relese It!」という本を出していて第２版は 2018 年に出版されているよ。日本でも「Release It! 本番用ソフトウェア製品の設計とデプロイのために」という本が出てる。

ADR は**アーキテクチャの決定に関するプロセスを記録する**もので、ドキュメンテーションの一つの手法として知られているよ。

アーキテクチャが技術や時代の進歩だったり、いろんな要件によって変更しないといけない時にドキュメントも変えないといけないよね？でも、ドキュメントにはそのプロセスやそれらを決定するに至った経緯などを詳細に載せるとかえって理解が容易でなくなる。だから、ドキュメントには結果しか載せられない。ただ、そうすると経緯を知らない人や話し合いに参加していない人はドキュメントだけを見て「何でこんなアーキテクチャを使ってるんだ？」とか「こっちの技術を使った方がいいのに。。。」というような不満が出てきたりするのは想像できるよね。こういう問題を解決するために作られたのが、ADR ってわけさ。

ただ、アーキテクチャだけに縛る必要はどこにもないのさ。そう、意思決定のプロセスを残すことは往々にして未来のための財産になり得る。事実、MADR という ADR の派生系みたいなものでは、「Architectural Decision Records」ではなく「Any Decision Records」に変更されている。詳しくは[Github レポジトリ](https://github.com/adr/madr)か[ドキュメント](https://adr.github.io/madr/)を見ると良いかもね。

---

## 使い方（基本）

詳しい使い方とかテンプレートや例などは Github のレポジトリにあるから、以下の URL を見ておくれ。ここではざっくりとした使い方を説明するよ。

URL： https://github.com/joelparkerhenderson/architecture-decision-record

ADR は markdown で基本的には書かれることが多いよ。構成要素としては以下の 5 つがシンプルで分かりやすく、マイケルが提案しているテンプレートでもあるんだ。

- タイトル(Title)
- ステータス(Status)
- コンテキスト(Context)
- 決定(Decision)
- 影響(Consequences)

一応、マイケルが提案した時の投稿を貼っておくね。英語ができる人は一度読んでみてもいいかもしれないね。

URL： https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions

一つずつ詳しく説明していくね。

### タイトル(Title)

ADR には重複のない連番を振り、タイトルには連番を含めた短い名前をつけるんだ。例えば、「ADR 0001：CSS フレームワークは TailwindCSS を利用する」とか「ADR 0009：GCP ではなく AWS を使用する理由」みたいな感じかな。

### ステータス(Status)

- 合意していない場合は「提案（proposed）」
- 合意された場合は「承認（accepted）」
- 後に ADR を決定を変更または取り消した場合「棄却（rejected）」、置き換えられた決定を参照して「非推奨（deprecated）」または「置き換え（superseded）」とマークされることもあるよ。

### コンテキスト(Context)

そもそも、満たすべき要件は何なのか？どういう要素を備えているべきなのか？みたいな理想の状態を説明するんだ。
もしくは、組織の現状やキャパシティなどでもいい、とにかく **「意思決定する上で満たすべき条件」** と **「意思決定しなければならない理由」**を書くみたいな感じかな。

### 決定(Decision)

決定した明確な理由、他の選択をしない理由、採用する上でどのように実現するに至るのかのプロセスなどを書こう。

### 影響(Consequences)

決定を適用した後のポジティブ・ネガティブどちらの影響も記録しよう。

markdown にまとめるとこんな感じかな。

```markdown
# Title

## Status

proposed / accepted / rejected / deprecated / superseded

## Context

-
-
-

## Decision

「」

## Consequences

Positive

-
-
-

Negative

-
-
-
```

---

## 使い方（実践）

ここでは MADR の方法を学んでみようと思うよ。MADR とは Markdown and Any Decision Records の略だよ。

ちなみに、MADR 以外にも Y-Statements っていう分派もあるらしい。詳しくは、この [Medium](https://medium.com/olzzio/y-statements-10eb07b5a177)みてね。

[ドキュメント](https://adr.github.io/madr/)にある Examples を見ていこう。

ドキュメントには Short Version と Long Version の二つがあり、これらを使い分けると良い見たいだね。

### Short Version

以下は DeepL で翻訳したものだよ。

```markdown
# 高度なテストアサーションを行うには Plain JUnit5 を使用する

## コンテクストと問題提起

読みやすいテストアサーションを書くには？
高度なテストのための読みやすいテストアサーションをどのように書くか？

## 考えられる選択肢

- Plain JUnit5
- Hamcrest
- AssertJ

## 決定事項

選択されたオプション 「Plain JUnit5 は標準的なフレームワークであり、他のフレームワークの機能は、新しい依存関係を追加することの利点を上回らないためです。
```

- タイトル（Title）
- コンテキストと問題提起（Context and Probrem Statement）
- 考えられる選択肢（Considered Options）
- 決定事項（Decision Outcome）

この 4 つで構成されていて、とてもシンプルだね。これよりももっと詳細に記録を残したい場合は以下の Long Version を使うといい。

### Long Version

以下は、Template から引っ張ってきたものを翻訳して、ある程度わかりやすくしたものだよ。

```markdown
---
status: { 提案 | 棄却 | 承認 | 非推奨 | … | ADR-0005 <0005-example.md> に置き換わりました }
date: { YYYY-MM-DD 最終更新日 }
deciders: { 意思決定を行う人のリスト }
consulted: { 意見を求める人、および双方向のコミュニケーションが可能な人のリスト。 }
informed: { このADRを見るべき対象、および意思決定の議論に関わらなかった人 }
---

# 解決した問題と解決策の短いタイトル

## コンテクストと問題提起

例えば、2 ～ 3 文を使った自由形式や、説明的なストーリーの形で、文脈と問題提起を記述する。
質問形式で問題を明確にし、コラボレーションボードや課題管理システムへのリンクを追加するとよいでしょう。

## 意思決定要因

- {意思決定要因 1、大切にしたい基準、直面している課題 …}
- {意思決定要因 2、大切にしたい基準、直面している課題 …}
- …

## 考えられる選択肢

- {選択肢 1}
- {選択肢 2}
- {選択肢 3}
- …

## 決定事項

選択された選択肢: "{選択肢 1}"、理由は〜〜〜〜。

### 影響

- Good：ポジティブな影響 …
- Bad：ネガティブな影響 …
- …

## 検証プロセス

ADR の実装がどのように検証されるか？
例：ドラフト（decider） → レビュー（conslted） → 更新（decider）

## 選択肢の長所と短所

### 選択肢 2

簡単な説明

- Good：ポジティブな影響
- Neutral：中立的な影響
- Bad：ネガティブな影響
- …

…

## 追加情報

決定をどの期間までにどのように実現する必要があるか、または再検討する必要があるかどうかなど。
```

Long Version ではフロントマターが採用されているみたい。

- status
- date
- deciders
- consulted
- informed

の 5 つが基本だけど、適宜削除したり変更しても良いみたいだね。意思決定フレームワークに「DACI」なるものがあるみたいだけど、こういうのを参考にしてるのかな？🤔

Short Version との違いとしては

- 意思決定要因（Decision Drivers）
- 検証プロセス（Validation）
- 選択肢の長所と短所（Pros and Cons of the Options）
- 追加情報（More Information）

の 4 つが増えたね。

検証プロセスについては、AWS の[ADR プロセス](https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/adr-process.html)のフローチャートを見てもらった方が早いよ。

紹介した全部の項目を採用する必要はないみたいなので、適宜削除したり改変したりしたら良さそうだね。
