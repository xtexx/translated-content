---
title: issue の作成と作業のガイドライン
slug: MDN/Community/Issues
l10n:
  sourceCommit: 269fa421f0a79b18f6000a26baebe30c74571b1f
---

協力者として、 issue （課題）を[報告](#issue_の報告に関するガイドライン)したり[作業](#issue_を作業するためのガイドライン)したりすることができます。
issue を報告すると、その issue はトリアージ（優先順位付け）されます。 issue の[トリアージ](#issue_のトリアージに関するガイドライン)は、通常、メンテナーやオーナーの役割を割り当てられた人たちが行います。

## 参加に関する全般的なガイドライン

issue を報告するとき、あるいは issue の会話に参加するとき、自分の入力したものがプロジェクト全体の進展に寄与していることを常に確認してください。あなたが開いた issue とあなたのコメントは、建設的で話題に即したものであり、単なるノイズになっていないかどうか考えてみてください。

次のようにしてください。

- issue を提出する前に、スタッフやコミュニティと[ディスカッション](/ja/docs/MDN/Community/Communication_channels#チャットルーム)を行う必要があるかどうかを検討してください。ディスカッションを使用することで、様々な視点から意見を聞き、合意された行動方針に収束させることができます。そうすることで、 issue を集中させ、生産的にすることができます。
- issue を提出した後は、自分で問題を修正してみてください。詳しくは、[協力ガイド](https://github.com/mdn/content/blob/main/CONTRIBUTING.md)（英語）をご覧ください。
- 質問がある場合は、 issue を提出するのではなく、 [MDN Web Docs チャットルーム](/ja/docs/MDN/Community/Communication_channels#チャットルーム)を使用して質問してください。

次のようなことは避けてください。

- 複数の話題についてディスカッションしようとしたり、本筋から外れたコメントをしたりして、 issue を複雑にすること。
- 漠然とした質問をするために、たくさんの issue を開くこと。
- まず自分で問題を解決しようとせずに質問をすること。

## issue の報告に関するガイドライン

[issue](https://docs.github.com/ja/issues/tracking-your-work-with-issues/about-issues) は、バグを追跡するために使用されます。 issue は、単一の実行可能なタスク、または関連のある実行可能なタスクの集合でなければならず、明確な結果がなければなりません。

### issue を提出する前に

MDN Web Docs のコンテンツやウェブサイトの外観に関するバグを見つけたと思ったら、[関連するリポジトリー](/ja/docs/MDN/Community/Our_repositories)で現在開かれている issue を検索して、他に誰もその issue を報告していないことを確認してください。

### issue の報告

発見した問題の種類に応じて、 [MDN の GitHub リポジトリー](MDN/Community/Our_repositories)で issue を提出することで報告することができます。
issue で指定された情報が不完全な場合、 [issue のトリアージプロセス](#情報の完全性について_issue_を検討する)で詳細情報の提供が要求されることがあります。

issue を開くためのヒントをいくつか示します。

- 適切なカテゴリーを選んで、 issue を報告してください。例えば、コンテンツのバグを報告するには、`mdn/content` リポジトリーにある [Content issue](https://github.com/mdn/content/issues/new?assignees=&labels=needs+triage&template=content-bug.yml) テンプレートを使用します。
- issue を報告するにあたって、十分な情報を提供してください。
  - **issue のタイトル**は、必要なアクションを簡潔に伝えるものでなければなりません。
  - **issue の説明**は、バグとその解決に必要なアクションを明確に記述している必要があります。また、その issue を解決するために完了すべきタスクやサブタスクが掲載されていなければなりません。他にも、以下のようなガイドラインがあります。
    - 説明フィールドを使用して、チェックリストを使用してタスクやサブタスクの状態を示しましょう。
    - issue へのコメントではなく、 issue の説明でタスクの状態を更新しましょう。 issue に複数の部分がある場合、説明文の中で[タスクリスト](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/about-task-lists)を使用してください。これは、様々なタスクの状態を判断するために issue のコメントをスクロールする必要がなくなるので、他のユーザーにとって便利です。
    - issue のコメントは、 issue 解決に役立つ詳細や文脈に限定すべきです。
- 以下のような状況に陥った場合は、[GitHub の MDN のディスカッション](https://github.com/orgs/mdn/discussions)に会話を移動してください。
  - issue を明確にするためにディスカッションが必要になった場合。
  - issue を開いた後にディスカッションが始まった場合。
  - この issue について、解決に向けた明確な合意が得られていない場合。
  - 対処中にタスクの完了のための要件が増えたり、作業が不明確になったりした場合。
- 軽微で小さなバグについては、[自分自身で変更を行い](#issue_を自分で修正)、プルリクエストを送信してください。

### タスクリストの issue の作成

開く issue がバグ報告ではなく、一連のタスクの実行である場合、 issue を[タスクリスト](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/about-task-lists)として作成することができます。説明文には、タスクを実行するための背景や理由を記述します。実行可能なタスクがすべてチェックリストとして掲載されていることを確認してください。

例を示します。

```markdown
// issue のタイトル
節が CSS プロパティテンプレートで定義された順序に従っていることを確認する。

### 説明

CSS プロパティページのテンプレートは[こちら](/ja/docs/MDN/Writing_guidelines/Page_structures/Page_types/CSS_property_page_template)で定義されています。
この issue のタスクリストは、文書化された CSS プロパティをテンプレートと比較し、準拠のためにプロパティページの変更を追跡するために使用されます。

### チェックするページの一覧

- [x] [accent-color](/ja/docs/Web/CSS/accent-color) - チェック済み、OK
- [ ] [backdrop-filter](/ja/docs/Web/CSS/backdrop-filter)
- [ ] [letter-spacing](/ja/docs/Web/CSS/letter-spacing) - `アクセシビリティの考慮` と `国際化の考慮` の節を `仕様書` の節の前に移動するプルリクエストを開いた
```

## issue を作業するためのガイドライン

issue を受け持った場合、これはきちんと時間内に作業を完了することが期待されていることを忘れないでください。代入されてから 1 週間経っても作業が進まなかったり、必要な作業ができなくなったりした場合は、コメントを残し、 issue の割り当てを解除してください。

これは、 issue に対して作業するための全般的な手順です。

1. **issue を探します。** 協力する issue を探しているなら、[`good first issue`, `help wanted`](#他のラベルを設定する) または [`p3`](#優先度ラベルを設定する) ラベルのついた issue を探してみてください。ほとんどのリポジトリーにこのようなラベル付けの issue があります。あなたのスキルセットに適した issue を選んでみてください。作業する issue を探すのに有益なもう一つの場所は、[MDN Contributors Task Board](https://github.com/orgs/mdn/projects/25)です。このプロジェクトビューは、複数のリポジトリーから開いている issue を一覧表示します。この一覧は、あなたが興味を持っているトピック（`Labels` 列）をもとにフィルタリングすることができます。 issue のトリアージ過程で取得されるいくつかの [ラベル](#他のラベルを設定する) の説明を参照してください。

   > [!NOTE]
   > `needs triage` ラベルの付いた issue は、MDN Web Docs コアチームがまだその issue をレビューしていないので、作業を始めない方がよいことを示します。

2. **issue を自分に割り当てます。** 作業したい issue を見つけたら、その issue が他の人に割り当てられていないことを確認します。その issue に作業したい旨をコメントで追加し、もし可能であれば、[その issue を自分自身に割り当ててください](https://docs.github.com/ja/issues/tracking-your-work-with-issues/using-issues/assigning-issues-and-pull-requests-to-other-github-users#assigning-an-individual-issue-or-pull-request)。

3. **調査を行います。** ほとんどの issue は、作業を始める前に何らかの調査を必要とします。
   - 行う必要がある作業を調べてください。もし質問が必要なら、 [MDN Web Docs チャットルーム](/ja/docs/MDN/Community/Communication_channels#チャットルーム)で助けを求めてください。
   - その issue がよく説明されていて、作業がかなり明白であるなら、先に進んで実行してください。
   - その issue が十分に説明されていない場合や、何が必要なのかわからない場合は、遠慮なく投稿者を @ メンションして、より詳細な情報を依頼してください。

4. **変更を行います。** リポジトリーをフォークし、ブランチを作成します。自分の作業を行って、リポジトリーで[プルリクエスト](/ja/docs/MDN/Community/Pull_requests)を開いてください。プルリクエストの説明で[その issue を参照](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue)してください。プルリクエストで更新したファイルに応じて、プルリクエストにレビュアーが自動的に割り当てられます（トピック領域ごとのチームは、[CODEOWNERS](https://github.com/mdn/content/blob/main/.github/CODEOWNERS) ファイルで定義されています）。

   プルリクエストを開いた後、変更を加えたりレビューのフィードバックを取り入れたりする時間がもうないことに気づいた場合、できるだけ早くプルリクエストのコメントでチームに知らせてください。これは、チームが他の興味を持っている協力者を割り当てて、プルリクエストの作業を完了させ、リンクされた issue を閉じさせるのに役立ちます。

5. プルリクエストがレビューされ、マージされた後、そのリンクされた issue を閉じられたとマークすることができます。プルリクエストを開いた際に `Fixes #<issue>` という文言を入れると、プルリクエストがマージされた際に、その issue は自動的に閉じられます。

### issue を自分で修正

もしバグを見つけたら — それがウェブサイトのルック＆フィールの issue であれ、文書の誤りであれ — 自分自身で修正することができます。どのように協力できるかは、[協力ガイド](https://github.com/mdn/content/blob/main/CONTRIBUTING.md)を読んでください。

誤字脱字やちょっとした文の改善など、小さなバグであったり、議論の余地のない修正が含まれる場合は、変更点を添えてプルリクエストを送信してください。

その他の種類のバグについては、 [issue を開く](#issue_の報告に関するガイドライン)ことから始めてください。その issue に取り組む意思を示すコメントを追加し、可能であれば、提案する解決策や issue を修正するための手順を記述してください。
MDN Web Docs チームがその issue が正当なものであることを確認し、提案された解決策を承認するために、その issue がトリアージされるのを待ちましょう。

> [!NOTE]
> issue のトリアージが行われる前にプルリクエストを開くと、リンクされた issue が無効と判断されたり、解決策が MDN Web Docs チームが期待するものと一致しない場合、あなたの時間と労力が無駄になってしまう可能性があります。
> issue のトリアージが完了したら、その issue を自分に割り当ててください。

[issue に取り組む際のガイドライン](#issue_を作業するためのガイドライン)を使用し、以下のように適切なソースを更新して、 issue を修正するようにしてください。

- MDN Web Docs のコンテンツ（英語）は [mdn/content](https://github.com/mdn/content) リポジトリー
- MDN Web Docs の翻訳コンテンツは [mdn/translated-content](https://github.com/mdn/translated-content) リポジトリー
- MDN Web Docs ウェブサイトのルック＆フィールは [mdn/yari](https://github.com/mdn/yari) リポジトリー

各リポジトリーには、どのように使用するかをガイドするための有益な情報が記載されています。
詳しい情報は、 [GitHub の主なリポジトリー](/ja/docs/MDN/Community/Our_repositories)を参照してください。

## issue のトリアージに関するガイドライン

MDN Web Docs の GitHub 組織のメンテナーまたはオーナーであれば、 1 つまたは複数の MDN Web Docs リポジトリーのその issue のトリアージに責任を負います。

トリアージの全体的なプロセスには、[全般的なタスク](#全般的なトリアージ作業)と[ issue 特有のタスク](# issue 特有のトリアージタスク)があります。

### 全般的なトリアージ作業

- issue を開くと、その issue に `needs triage` ラベルが自動的に設定されます。このラベルを検索すると、[トリアージが必要な issue ](# issue 特有のトリアージタスク)を探すことができます。協力者およびその他メンバーは、 issue がトリアージされるまで、この issue に対して作業をしてはいけません。（トリアージ担当者は、その issue をトリアージした後、`needs triage` ラベルを削除することを忘れないでください。）

- [mdn/content リポジトリー](https://github.com/mdn/content/issues)では、追加の `Content:` ラベル、例えば `Content:CSS` や `Content:WebAPI` などが自動的に issue に設定されます。これは、その issue で言及されているMDN URLに基づいて設定されます。このコンテンツ特有のラベルを使用して、特定のトピック領域でトリアージすべき issue を探していくことができます。

- その issue が en-US 以外のアクティブなロケールに関するものであれば、 `l10n-fr`、`l10n-zh`、`l10n-ja` などの適切なラベルを設定してください。それらのロケールのチームがその issue をピックアップし、トリアージします。

- issue のトリアージは、常に積極的に行う必要はありません。毎週 30 分など、自分の担当領域で定期的に issue のトリアージを行うための補助的な時刻を設定してください。トリアージは会議の中で行う必要はありませんし、皆と同じ時刻に行う必要もありません が、トリアージされていないバグのバックログが多くなりすぎないように、定期的に行う必要があります。

- 毎週送られてくる issue のトリアージとは別に、古いバグのリストを見直して、停滞しているもの、閉じる必要のあるもの、もう関係のないものがないかどうかを確認しましょう。30 日間活動のないその issue には、自動的に `idle` ラベルが設定されます。
  - 割り当てられた issue で、開いたままのものがあれば、割り当てられた人が進捗しているかどうか調べてください。割り当てられてから 1 週間経っても進展がない場合は、まだその issue に取り組む時間があるのかどうか尋ねてみてください。さらに 1 週間経っても進展がない場合は、割り当てを解除し、その issue を他に関心を持つ協力者に利用できるようにすることを示すコメントを残してください。
  - その issue を修正するためのプルリクエストが開かれているにもかかわらず、1 週間レビューされていない場合は、レビュアーに優しく ping を打って、その issue に手を付けられるかどうか要請してみましょう。
  - もしその issue を修正するためのプルリクエストが 1 週間後にレビューコメントへの対応を待っているのなら、作者にレビューへの対応が可能かどうか依頼してください。さらに 1 週間が経過したら、時間があれば自分でレビューコメントを修正するか、プルリクエストを閉じて関連の issue の割り当てを解除するかしてください。

### issue 特有のトリアージタスク

それぞれの issue をトリアージする際に従うべきガイドラインは以下のとおりです。

#### issue が有効かどうか検討する

issue に対して妥当性を検討する際には、次のような点に留意する必要があります。

- 提起されたその issue が妥当かどうか、修正されることで読者やウェブサイトのコンテンツが改善されるかどうかを確認してください。
- 修正された場合の影響が小さいか、サイト全体に及ぶかを評価してください。
- その issue の修正がまずディスカッションを必要とするかどうかを評価し、その場合は代わりに[ディスカッション](https://github.com/orgs/mdn/discussions)を開くように指摘してください。
- その issue が[執筆ガイドライン](/ja/docs/MDN/Writing_guidelines/Writing_style_guide)や[テンプレート](/ja/docs/MDN/Writing_guidelines/Page_structures/Page_types)に従っているかどうかを調べてください。
- リンクの追加に関する提案が、[外部リンクポリシー](/ja/docs/MDN/Writing_guidelines/Writing_style_guide#external_links)に従っているかどうか調べてください。

#### 情報の完全性について issue を検討する

それぞれの issue を以下のチェックリストに照らして検討し、その issue に、誰かがそのバグの作業を始めるための記述された情報が含まれていることを確認してください。

- issue がある MDN Web Docs ページの URL、または issue が複数のページに存在する場合は MDN Web Docs ページの URL の例。
- issue を見つけた MDN Web Docs ページの具体的な見出しまたは節。
- 不正確な情報、役に立たない情報、不完全な情報、または不足している情報の明確な説明。

上記の情報のいずれかが存在しない場合、その issue の作成者にこれらの情報を提供するよう依頼し、`needs info` ラベルをその issue に追加してください。その情報の詳細が提供された後に、 issue のトリアージを再開してください（その後、`needs info`ラベルを削除することができます）。作成者から回答を得るまで、最長で 1 週間ほど待っても issue ありません。

#### 優先度ラベルを設定する

各バグについて、その issue の重要度に応じた優先度ラベルを設定し、最も重要な issue ・領域に作業したい人が作業しやすいようにしてください。

- 重大な issue 。その issue がサイトのどこに現れているかにかかわらず、できるだけ早く修正する必要があります。そのような issue は、MDN の評判に深刻なダメージを与えたり、ユーザーに危害を加えたりする可能性があります。その issue の例としては、不正なコードスニペットが記載されており、実運用で使用された場合、深刻なセキュリティ issue を引き起こす可能性があるものや、マルウェア、冒涜、ポルノ、ヘイトスピーチなどの好ましくないコンテンツ、またはそうしたコンテンツへのリンクが挙げられます。
  - ラベル: `p0` （直ちに対応を行う）

- 重要な issue: この種類の issue は、ページの有用性に深刻な影響を与える可能性があります。例えば、大量の古い情報、動作しない複雑で重要なコード例、文章が稚拙で理解しにくい部分が大量にある、リンク切れが多数ある、などです。
  - ラベル: `p1` （早めに対応を行う）または `p2` （早めに対応を行うが、より優先度の高い issue を優先する）

- 軽微な issue: これは、既存のコンテンツをより良くすることができるが、学習に影響を与えないか、軽微な影響しか与えない、改善 issue の種類です。この種類の issue は積極的に計画されるものではないので、これらの issue を修正するための協力者の手助けは歓迎され、大いに感謝されます。その issue を修正することは、投稿プロセスに慣れ始めた初心者の協力者に、必要な練習を提供することにもなります。例としては、タイプミス、文法の間違い、リンク切れ、少量の古い情報や悪い文、うまく動作しないコードスニペットなどが挙げられます。
  - ラベル: `p3` （いつ対応するか指定しない）

一般的に、重大な issue はすぐに修正されるべきであり、MDN Web Docs のスタッフや仲間によって処理される可能性が高いものです。

#### 有用な情報を追加する

可能であれば、その issue を修正するために協力者の助けとなる情報を追加してください。情報は、手順や一般的な手法、修正された他の同様の issue へのリンク、参考資料などの形でかまいません。よく練られた計画や手順は、特に `good first issue` とラベル付けされている issue では必要で、新しい協力者をすばやく立ち上げるのに役立ちます。このタスクは5分から10分程度の時間に設定することができます。

例えば、トリアージする人は、トリアージしている issue に以下のような情報を追加することができます。

```md
その issue を修正する人は、以下のことが必要です。

- 見出し X の下の最初の段落を更新し、 Y の issue を修正しましょう。
- X の説明を追加しましょう。
- リンク X で互換性データを更新しましょう。
```

#### 他のラベルを設定する

次に、以下のラベルを適宜設定します。

- `effort: small`, `effort: medium`, `effort: large`: 協力者の中には、バグを修正するのに必要な時間と労力に基づいてバグを検索したい人もいます。ですから、できれば、必要な労力の見積もりを提供するようにしてください。
- `good first issue`: その issue の修正が実に単純で、その issue を修正することが、プロセスを習得しつつある新人にとって良い練習になる場合、その issue にこのラベルを設定ししてください。
- `help wanted`: その issue が、そのトピックについて知っている人、または慣れることができる人からの助けを必要とする場合、このラベルを設定します。このラベルはよく使用されるもので、自分の慣れることや専門分野のオープンソースプロジェクトで作業するための issue を検索するために、このラベルを使用する協力者もいます。
- `broken link external`: 外部ページへのリンク切れが issue である場合、このラベルを設定してください。
- `document not written`: issue がまだ書かれていない必要な文書に関係している場合、通常はリンクがその文書を指しているため、このラベルを設定します。
- `needs content update`: `mdn/content` リポジトリーと同様の修正を他のリポジトリーに行う必要がある場合の issue に、このラベルを設定してください。

  > [!NOTE]
  > トリアージプロセスが完了したら、 `needs triage` のラベルを剥がしてください。
