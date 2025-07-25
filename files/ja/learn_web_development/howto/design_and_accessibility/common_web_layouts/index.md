---
title: 一般的なウェブレイアウトには何が含まれているのか
slug: Learn_web_development/Howto/Design_and_accessibility/Common_web_layouts
l10n:
  sourceCommit: 479ea4c8bff4b900a7968413287c77dde2b0c20f
---

ウェブサイトのページをデザインする際、最も一般的なレイアウトを把握しておくとよいでしょう。

<table class="standard-table">
  <tbody>
    <tr>
      <th scope="row">前提条件:</th>
      <td>
        ウェブプロジェクトで<a href="/ja/docs/Learn_web_development/Howto/Design_and_accessibility/Thinking_before_coding">何を実現したいのか</a>について既に考えていること。
      </td>
    </tr>
    <tr>
      <th scope="row">目標:</th>
      <td>
        ウェブページのどこに何を置くか、どのように置くかを学びます。
      </td>
    </tr>
  </tbody>
</table>

## 概要

ウェブデザインについて語るのには理由があります。ウェブデザインは白紙の状態からスタートし、さまざまな方向へ展開することができます。また、あまり経験がない場合、白紙のページから始めるのは少し怖いかもしれません。 25 年以上の経験を持つ私たちが、サイト設計に役立つ共通の経験則をお教えします。

モバイルウェブに新たに注目が集まっている現在でも、主流のウェブページはほぼすべてこのパーツから作られています。

- ヘッダー
  - : サイト内の全ページの上部に表示されます。すべてのページに関連する情報（サイト名やロゴなど）と、使いやすいナビゲーションシステムが含まれています。
- 本文
  - : 最大の領域で、現在のページに固有のコンテンツを含みます。
- サイドにあるもの
  - : 1) 本文を補完する情報。 2) ページ間で共有される情報。 3) 代替ナビゲーションシステム。実際、すべてがこのページの本文で絶対には必要でないものです。
- フッター
  - : 本サイトの各ページの下部に表示されます。ヘッダーと同様、法的な通知や連絡先など、あまり目立たないグローバルな情報が含まれています。

これらの要素は、すべてのフォームファクターで非常に一般的ですが、さまざまな方法でレイアウトすることができます。以下に例を示します（**1** はヘッダー、 **2** はフッター、 **A** は本文、 **B1, B2** はサイドにあるものを表します）。

**1 列レイアウト**。特にモバイルブラウザーでは、小さな画面の中でごちゃごちゃしないようにすることが重要です。

![1 列レイアウトの例。本文が一番上で、その下にサイド記事が積み重なっています。](1-col-layout.png)

**2 列レイアウト**。タブレットは中型の画面であるため、タブレットをターゲットによく使用されます。

![基本的な 2 列レイアウトの例。左列にサイド記事、右列に本文を配置。](2-col-layout-right.png) ![基本的な 2 列レイアウトの例。右列にサイド記事、左列に本文を配置。](2-col-layout-left.png)

**3 列レイアウト**。画面の大きなデスクトップのみに適しています。（ただし、デスクトップユーザーのの多くは、全画面表示よりも小さなウィンドウで見ることを好みます）。

![基本的な 3 列レイアウトの例。左右の列にサイド記事、中央の列に本文。](3-col-layout.png) ![もう一つの 3 列レイアウトの例。左側が横並び、右側の列が本文です。](3-col-layout-alt.png) ![もう一つの 3 列レイアウトの例。右側が横並び、左側の列が本文です。](3-col-layout-alt2.png)

それらを一斉に混ぜ合わせるところから、本当の楽しみが始まるのです。

![混合レイアウトの例。本文が上、その下にサイド記事が横に並んでいます。](1-col-layout-alt.png) ![混合レイアウトの例。左列に本文、右列にサイド記事を積み重ねたもの。](2-col-layout-left-alt.png) ![混合レイアウトの例。左列にサイド記事、右列に本文を配置し、本文の下にサイド記事を配置したもの。](2-col-layout-mix.png) ![混合レイアウトの例。 1 行目の左側に本文、同じ行の右側に 1 つ目のサイド記事、2 行目に 2 つ目のサイド記事が行全体に配置。](2-col-layout-mix-alt.png)…

これらはあくまで例であり、レイアウトは自由です。画面上でコンテンツが動くこともありますが、常にヘッダー（1）を一番上に、フッター（2）を一番下に置いていることにお気づきでしょうか。また、本文（A）は最も重要なので、ほとんどの空間をそれに充てます。

これらは、みなさんが描くことのできる経験則です。もちろん、複雑なデザインや例外もあります。他の記事では、レスポンシブなサイト（画面の大きさに従って変化するサイト）や、ページごとにレイアウトが異なるサイトのデザイン方法について説明します。今のところ、サイト全体でレイアウトを統一するのが最善です。

## アクティブラーニング

_利用可能なアクティブラーニングはまだありません。[ぜひ協力をご検討ください](/ja/docs/MDN/Community/Getting_started)。_

## より深く掘り下げる

ここで、有名なウェブサイトから、もう少し具体的な例を取り上げてみましょう。

### 1 列レイアウト

一般的な 1 列レイアウトで、ひとつのページにすべての情報を直線的に提供するものです。

![1 列レイアウトの例](screenshot-product.jpg) ![ヘッダー、本文、サイド記事の積み重ね、フッターの1列レイアウト](screenshot-product-overlay.jpg)

とても簡単です。ただ、たくさんの人がデスクトップ PC からサイトを閲覧することに変わりはないので、デスクトップでも使いやすく、読みやすいコンテンツにしてください。

### 2 列レイアウト

ブログは通常、 2 つの列を持っています。太い列は本分用で、細い列は横に並べるもの（ウィジェット、副次ナビゲーションレベル、広告など）用の列です。

![ブログの 2 列レイアウトの例](screenshot-blog.jpg) ![左列に本文を配置した 2 列組みのレイアウト。](screenshot-blog-overlay.jpg)

この例では、ヘッダーのすぐ下にある画像 (B1) を見てください。これは本文と関係がありますが、本文はこれがなくても意味をなすので、この画像を本文と考えることも、横に並んでいるコンテンツと考えることもできます。それはどうでもいいことです。重要なのは、ヘッダーの下に何かを置く場合、それは本文か、本文に直接関連するものでなければならないということです。

### 罠

**[MICA](https://www.mica.edu/about-mica/)**. これはちょっとやっかいですね。3 列レイアウトのように見えます。

![偽の 3 列レイアウトの例](screenshot-education.jpg) ![3 列組みのレイアウトに見えますが、実は補助的なものが浮動しています。](screenshot-education-overlay.jpg)

しかし、そうではありません。 B1 と B2 は本文の周りに浮かんでいるのです。 "float" という単語を覚えておいてください。 {{Glossary("CSS")}} について学び始めると、ピンとくるはずです。

なぜ 3 列レイアウトだと思ったのでしょうか？右上の画像が L 字型だから、 B1 が移動した本文の補助列のように見えるから、そして MICA ロゴの "M" と "I" が縦の力線を作成しているからです。

これは、古典的なレイアウトがデザインの創造性を支えている良い例です。シンプルなレイアウトは実装が簡単ですが、この分野では自分の創造性を発揮する余地を与えてください。

### より巧妙なレイアウト

**The Opera de Paris**.

![巧妙なレイアウトの例。](screenshot-opera.jpg) ![これは 2 列レイアウトですが、ヘッダーが本文コンテンツに重なっています。](screenshot-opera-overlay.jpg)

基本的には 2 列レイアウトですが、視覚的にレイアウトを崩すような工夫があちこちに見受けられます。特に、ヘッダーが本文の画像に重なっていること。ヘッダーのメニューの曲線と画像の下部の曲線が結びついて、ヘッダーと本文は技術的には完全に別物であるにもかかわらず、一つのもののように見えます。 Opera の例は MICA の例よりも複雑に見えますが、実際には簡単に実装できます（正確には、「簡単」というのは相対的な概念です）。

このように、基本的なレイアウトだけでも、魅力的なウェブサイトを作ることができます。自分の好きなウェブサイトを保有し、ヘッダー、フッター、本文、サイドコンテンツはどこにあるのか、自問してみてください。これはうまくいくデザイン、いかないデザインのヒントになります。
