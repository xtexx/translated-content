---
title: サーバーサイドウェブフレームワーク
slug: Learn_web_development/Extensions/Server-side/First_steps/Web_frameworks
original_slug: Learn/Server-side/First_steps/Web_frameworks
l10n:
  sourceCommit: 4bddde3e2b86234eb4594809082873fc5bf00ee3
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/Server-side/First_steps/Client-Server_overview", "Learn/Server-side/First_steps/Website_security", "Learn/Server-side/First_steps")}}

前の記事では、ウェブクライアントとサーバー間の通信、HTTP リクエストとレスポンスの性質、およびウェブブラウザーからのリクエストにレスポンスするためにサーバーサイドウェブアプリケーションが実行する必要があることについて説明しました。この知識をもとに、ウェブフレームワークがどのようにこれらのタスクを単純化できるかを探り、最初のサーバーサイドウェブアプリケーションのためのフレームワークをどのように選択するかを考えてみましょう。

<table>
  <tbody>
    <tr>
      <th scope="row">前提条件:</th>
      <td>
        HTTP リクエストを処理して応答するサーバー側コードがどのようなものかに関する基本的な理解（<a
          href="/ja/docs/Learn/Server-side/First_steps/Client-Server_overview"
          >クライアント・サーバーの概要</a
        >を参照）
      </td>
    </tr>
    <tr>
      <th scope="row">目的:</th>
      <td>
        ウェブフレームワークがどのようにサーバーサイドコードの開発/保守を簡素化するかを理解し、読者が自分自身でフレームワークを選択することを考えられるようになること。
      </td>
    </tr>
  </tbody>
</table>

次の節では、実際のウェブフレームワークから取得したコードフラグメントを使用していくつかのポイントを説明します。今では**すべて**が理解できない場合でも、心配しないでください、フレームワーク固有のモジュールコードを通して作業していきますので。

## 概要

サーバーサイドウェブフレームワーク (別名「ウェブアプリケーションフレームワーク」)は、ウェブアプリケーションの作成、保守、および拡張を容易にするソフトウェアフレームワークです。適切なハンドラーへの URL のルーティング、データベースとのやり取り、セッションとユーザー認証のサポート、出力のフォーマット (HTML、JSON、XML など)、ウェブ攻撃に対するセキュリティの向上など、一般的なウェブ開発タスクを簡素化するツールとライブラリーを提供します。

次のセクションでは、ウェブフレームワークによってウェブアプリケーションの開発がどのように容易になるかについて、もう少し詳しく説明します。次に、ウェブフレームワークを選択するために使用できる基準のいくつかを説明し、次にいくつかの選択肢をリストします。

## ウェブフレームワークで何ができるか

ウェブフレームワークは、一般的なウェブ開発操作を簡素化するためのツールとライブラリーを提供します。サーバーサイドのウェブフレームワークを使う*必要*はありませんが、使用することを強くお勧めします。それはあなたの人生をずっと楽にするでしょう。

このセクションでは、ウェブフレームワークによって提供されることが多い機能の一部について説明します (必ずしもすべてのフレームワークがこれらの機能のすべてを提供するわけではありません！)。

### HTTP リクエストとレスポンスを直接操作

前回の記事で見たように、ウェブサーバーとブラウザーは HTTP プロトコルを介して通信します。サーバーはブラウザーからの HTTP リクエストを待ってから HTTP レスポンスで情報を返します。ウェブフレームワークを使用すると、これらのリクエストとレスポンスを処理するためのサーバーサイドコードを生成する単純化された構文を作成できます。これは、低レベルのネットワークプリミティブよりも、より簡単な、より高レベルのコードと対話する、より簡単な仕事を持つことを意味します。

以下の例は、Django (Python) ウェブフレームワークでどのように機能するかを示しています。すべての "view" 関数 (リクエストハンドラー) はリクエスト情報を含む `HttpRequest` オブジェクトを受け取り、フォーマットされた出力 (この場合は文字列) と共に `HttpResponse` オブジェクトを返す必要があります。

```python
# Django view function
from django.http import HttpResponse

def index(request):
    # Get an HttpRequest (request)
    # perform operations using information from the request.
    # Return HttpResponse
    return HttpResponse('Output string to return')
```

### 適切なハンドラーにリクエストをルーティングする

ほとんどのサイトは、別々の URL からアクセス可能なさまざまなリソースを数多く提供します。これらすべてを 1 つの関数で処理するのは管理が難しいため、ウェブフレームワークは URL パターンを特定のハンドラー関数にマッピングするための単純なメカニズムを提供します。ベースとなるコードを変更することなく特定の機能を提供するために使用される URL を変更できるため、このアプローチにはメンテナンスの面でも利点があります。

フレームワークが異なると、マッピングに異なるメカニズムを使用します。たとえば、Flask (Python) ウェブフレームワークは、デコレーターを使用してビュー関数への経路を追加します。

```python
@app.route("/")
def hello():
    return "Hello World!"
```

Django は開発者が URL パターンとビュー関数の間の URL マッピングのリストを定義することを期待しています。

```python
urlpatterns = [
    url(r'^$', views.index),
    # example: /best/myteamname/5/
    url(r'^(?P<team_name>\w.+?)/(?P<team_number>[0-9]+)/$', views.best),
]
```

### リクエスト内のデータに簡単にアクセスできるようにする

データはさまざまな方法で HTTP リクエストにエンコードできます。サーバーからファイルまたはデータを取得するための HTTP `GET` リクエストは、URL 引数または URL 構造内で必要なデータをエンコードすることができます。サーバー上のリソースを更新するための HTTP `POST` リクエストは、代わりに更新情報をリクエストの本文内に「POST データ」として含めます。HTTP リクエストはまた、現在のセッションまたはユーザーに関する情報をクライアント側のクッキーに含めることができます。

ウェブフレームワークは、この情報にアクセスするためのプログラミング言語に適したメカニズムを提供します。
たとえば、Django がすべてのビュー関数に渡す `HttpRequest` オブジェクトには、対象の URL にアクセスするためのメソッドとプロパティ、リクエストの種類 (HTTP `GET` など)、`GET` または `POST` 引数、cookie、セッションデータなどが含まれます。Django は URL マッパーで「キャプチャパターン」を定義することで URL の構造にエンコードされた情報を渡すこともできます (上のセクションの最後のコードを見てください)。

### データベースアクセスを抽象化および単純化する

ウェブサイトは、データベースを使用して、ユーザーと共有するための情報とユーザーに関する情報の両方を保存します。ウェブフレームワークは多くの場合、データベースの読み取り、書き込み、照会、および削除操作を抽象化するデータベース層を提供します。この抽象化層は、オブジェクトリレーショナルマッパー (ORM) と呼ばれます。

ORM を使用することには、2 つのメリットがあります。

- 基になるデータベースを使用するコードを必ずしも変更することなく、置き換えることができます。これにより、開発者は使用状況に基づいてさまざまなデータベースの特性を最適化できます。
- データの基本的な検証はフレームワーク内に実装できます。これにより、データが正しい種類のデータベースフィールドに格納されていること、正しい形式 (メールアドレスなど) であることを確認することが簡単かつ安全になり、いかなる意味でも悪意はありません (クラッカーはデータベースレコードの削除などの悪いことをするために特定の形式のコードを使用することができます)。

たとえば、Django のウェブフレームワークは ORM を提供し、レコードの構造を*モデル*として定義するために使用されるオブジェクトを参照します。モデルは格納されるべきフィールド*タイプ*を特定し、それはどの情報を格納することができるかについてのフィールドレベルの検証 (例えば、メールフィールドは有効なメールアドレスのみを許可する) を提供できます。フィールド定義では、最大サイズ、デフォルト値、選択リストのオプション、ドキュメントのヘルプテキスト、フォームのラベルテキストなども指定できます。コードとは別に変更されるかもしれない設定であるため、モデルは基礎となるデータベースについてのいかなる情報も述べません。

以下の最初のコードスニペットは、`Team` オブジェクト用の非常に単純な Django モデルを示しています。これは、チーム名とチームレベルを文字フィールドとして格納し、各レコードに格納する最大文字数を指定します。`team_level` は選択項目なので、表示される選択項目と保管されるデータの間のマッピング、およびデフォルト値も提供します。

```python
#best/models.py

from django.db import models

class Team(models.Model):
    team_name = models.CharField(max_length=40)

    TEAM_LEVELS = (
        ('U09', 'Under 09s'),
        ('U10', 'Under 10s'),
        ('U11', 'Under 11s'),
        # List our other teams
    )
    team_level = models.CharField(max_length=3,choices=TEAM_LEVELS,default='U11')
```

Django モデルはデータベースを検索するための簡単なクエリー API を提供します。これは、異なる基準 (正確、大文字と小文字を区別しない、より大きいなど) を使用して一度に多数のフィールドに対して一致させることができ、複雑なステートメント (たとえば、"Fr" で始まるチーム名、または "al" で終わるチーム名を持つ U11 チームの検索を指定できます) をサポートすることができます。

2 番目のコードスニペットは、すべての U09 チームを表示するための表示機能 (リソースハンドラー) を示しています。この場合、`team_level` フィールドのテキストが 'U09' であるすべてのレコード (この基準が、2 つの下線で区切られたフィールド名と一致タイプを持つ引数、つまり **`team_level__exact`** として `filter()` 関数に渡されることに注意してください) をフィルタリングしたいと指定します。

```python
#best/views.py

from django.shortcuts import render
from .models import Team

def youngest(request):
    list_teams = Team.objects.filter(team_level__exact="U09")
    context = {'youngest_teams': list_teams}
    return render(request, 'best/index.html', context)
```

### データのレンダリング

ウェブフレームワークは通常テンプレートシステムを提供します。これにより、ページが生成されたときに追加されるデータのプレースホルダーを使用して、出力文書の構造を指定できます。テンプレートは HTML の作成によく使用されますが、他の種類の文書も作成できます。

ウェブフレームワークは多くの場合、{{glossary("JSON")}} や {{glossary("XML")}} など、格納されているデータから他のフォーマットを簡単に生成するためのメカニズムを提供します。

たとえば、Django テンプレートシステムでは、"double-handlebars" 構文 (例えば `\{{ variable_name }}`) を使って変数を指定することができます。これは、ページがレンダリングされるときにビュー関数から渡された値に置き換えられます。テンプレートシステムは式のサポート (構文: `{% expression %}`) も提供します。これによりテンプレートは、渡されたリスト値を繰り返すような単純な操作を実行できます。

> [!NOTE]
> Jinja2 (Python)、handlebars (JavaScript)、moustache (JavaScript) など、他の多くのテンプレートシステムでも同様の構文が使用されています。

以下のコードスニペットはこれがどのように機能するかを示しています。前のセクションの「最年少チーム」の例を続けると、HTML テンプレートにはビューによって `youngest_teams` というリスト変数が渡されます。HTML スケルトンの内部には、最初に `youngest_teams` 変数が存在するかどうかを確認し、次に for ループ内でそれを繰り返す式があります。各イテレーションで、テンプレートはチームの `team_name` 値をリストアイテムに表示します。

```django
#best/templates/best/index.html

<!DOCTYPE html>
<html lang="en">
  <body>
    {% if youngest_teams %}
      <ul>
        {% for team in youngest_teams %}
          <li>\{{ team.team_name }}</li>
        {% endfor %}
      </ul>
    {% else %}
      <p>利用できるチームがありません。</p>
    {% endif %}
  </body>
</html>
```

## ウェブフレームワークの選び方

使いたいと思うかもしれないほとんどすべてのプログラミング言語には多数のウェブフレームワークが存在します (次のセクションでもっと人気のあるフレームワークの一部をリストします)。選択肢が多すぎると、どのウェブフレームワークが新しいウェブアプリケーションの最適な出発点になるかを判断するのが難しくなります。

決定に影響を与える可能性がある要因の一部は以下のとおりです。

- **学ぶ努力:** ウェブフレームワークを学ぶための努力は、基礎となるプログラミング言語、その API の一貫性、その文書の品質、およびそのコミュニティの規模と活動に慣れているかどうかによって異なります。まったくプログラミングの経験がない場合は、 Django を検討してください (上記の基準に基づいて学ぶのが最も簡単な方法の 1 つです)。 すでに特定のウェブフレームワークやプログラミング言語に関する豊富な経験を持っている開発チームの一員であれば、それにこだわるのは理にかなっています。
- **生産性:** 生産性とは、フレームワークに慣れれば新しい機能をどれだけ早く作成できるかを示す尺度であり、コードの作成と保守の両方の作業が含まれます (古い機能が壊れている間は新しい機能を作成できないため)。生産性に影響を与える要因の多くは、「学ぶ努力」の要因と似ています。例えばドキュメント、コミュニティ、プログラミング経験などで、その他の要因としては
  - _フレームワークの目的/原点_: ウェブフレームワークの中には、特定の種類の問題を解決するために最初に作成されたものもあり、同様の制約を持つウェブアプリケーションを作成するのに優れています。たとえば、 Django は新聞のウェブサイトの開発をサポートするために作成されたので、ブログやその他のものを公開するサイトに適しています。それとは対照的に、 Flask ははるかに軽量なフレームワークであり、組み込みデバイスで実行されるウェブアプリケーションを作成するのに最適です。
  - _考え方がある vs ない_: 考え方のあるフレームワークは、特定の問題を解決するための推奨される「最善の」方法があるものです。一般的な問題を解決する場合に、考え方のあるフレームワークはより生産的になる傾向がありますが、時々柔軟性が劣ります。
  - _電池が含まれている か 自分でそれを入手_: 一部のウェブフレームワークには、開発者が「デフォルトで」考えうるすべての問題に対処するツール/ライブラリーが含まれています。一方、より軽量なフレームワークには、ウェブ開発者が別々のライブラリーから問題の解決策を選んで解決することがあります (Django は前者の例で、 Flask は非常に軽量なフレームワークの例です)。すべてを含むフレームワークは、必要なものがすべて揃っているため、始めるのが簡単なことが多く、それがうまくまとまって文書化されている可能性があります。
    しかし、より小さなフレームワークに (これから) 必要とするものすべてがあれば、より制約の厳しい環境で実行することができ、学ぶべきことのより小さく簡単なサブセットを持つことになります。
  - _フレームワークが優れた開発プラクティスを促進するかどうか_: たとえば、[Model-View-Controller](/ja/docs/Glossary/MVC) アーキテクチャでコードを論理関数に分割することを推奨するフレームワークは、開発者に期待していないものよりも保守性の高いコードになります。同様に、フレームワーク設計は、コードをテストして再利用することがどれほど簡単かに大きな影響を与える可能性があります。

- **フレームワーク/プログラミング言語の性能:** Python のような比較的遅いランタイムでも、中規模のサイトを中程度のハードウェアで実行するには「十分」であるため、通常「スピード」が選択の最大の要因になることはありません。他の言語、たとえば C++ または JavaScript のような言語の体感速度の利点は、学習と保守のコストによって相殺される可能性があります。
- **キャッシングサポート:** ウェブサイトがより成功するにつれて、ユーザーがアクセスしたときに受信するリクエストの数に対応できなくなる可能性があります。この時点で、キャッシュのサポートを追加することを検討するかもしれません。キャッシングは、ウェブレスポンスの全部または一部を保存して、後続のリクエストで再計算する必要がないようにするための最適化です。キャッシュされたレスポンスを返すことは、そもそもレスポンスを計算するよりもはるかに高速です。キャッシングは、コード内またはサーバー内 ([リバースプロキシー](https://en.wikipedia.org/wiki/Reverse_proxy)を参照) に実装できます。ウェブフレームワークには、キャッシュ可能なコンテンツを定義するさまざまなレベルのサポートがあります。
- **スケーラビリティ:** ウェブサイトが素晴らしく成功すると、キャッシングの利益を使い果たし、さらに*垂直なスケーリング*の限界に達するでしょう (より強力なハードウェア上であなたのウェブアプリケーションを実行します)。この時点では、_水平方向にスケールする_ (サイトを多数のウェブサーバーやデータベースに分散して負荷を分散する) か、「地理的に」スケールする必要があるかもしれません。選択したウェブフレームワークによって、サイトの規模を拡大するのがいかに簡単になるかが大きく変わります。
- **ウェブセキュリティ:** 一部のウェブフレームワークは、一般的なウェブ攻撃への対処をより適切にサポートします。たとえば Django は HTML テンプレートからのすべてのユーザー入力をサニタイズするので、ユーザーが入力した JavaScript は実行できません。他のフレームワークも同様の保護を提供しますが、デフォルトで常に有効になっているわけではありません。

ライセンス、フレームワークが活発に開発されているかどうかなど、他にも多くの要因が考えられます。

プログラミングの完全な初心者であるならば、おそらく「学びやすさ」に基づいてフレームワークを選ぶでしょう。言語自体の「使いやすさ」に加えて、高品質のドキュメント/チュートリアル、および新しいユーザーを支援する活発なコミュニティが最も貴重なリソースです。コースの後半で例を書くために [Django](https://www.djangoproject.com/) (Python) と [Express](http://expressjs.com/) (Node/JavaScript) を選択しました。これは主にそれらが習得が容易で優れたサポートがあるためです。

> [!NOTE]
> [Django](https://www.djangoproject.com/) (Python) と [Express](http://expressjs.com/) (Node/JavaScript) のメインウェブサイトに行き、それらのドキュメントとコミュニティを調べてみましょう。
>
> 1. メインサイトに移動する (上記のリンク先)
>    - Documentation メニューのリンク (Documentation、Guide、API Reference、Getting Started など) をクリックします。
>    - URL ルーティング、テンプレート、データベース/モデルの設定方法を説明したトピックはありますか？
>    - ドキュメントは明確ですか？
> 2. 各サイトのメーリングリストに移動します (コミュニティリンクからアクセス可能)。
>    - 過去数日間に投稿された質問の数
>    - 回答はいくつありますか？
>    - 彼らは活発なコミュニティを持っていますか？

## いくつかの良いウェブフレームワークとは？

それでは次に、いくつかのサーバーサイドウェブフレームワークについて説明しましょう。

以下のサーバーサイドフレームワークは、執筆時点で入手可能な最も人気のあるものの一部を表しています。オープンソースで、活発に開発されており、熱心なコミュニティがドキュメントを作成し、ディスカッション掲示板でユーザーを支援しています。また、多数の有名ウェブサイトで使用されています。他にも基本的なインターネット検索を使用して見つけられる多くの素晴らしいサーバーサイドフレームワークがあります。

> [!NOTE]
> 説明は (一部) フレームワークウェブサイトから引用しています。

### Django (Python)

[Django](https://www.djangoproject.com/) は、迅速な開発とクリーンで実用的なデザインを促進する高レベルの Python ウェブフレームワークです。

経験豊富な開発者によって構築されており、ウェブ開発における面倒なことの大部分を世話します、そのため、車輪の再発明をする必要なく、アプリの作成に集中できます。無料でオープンソースです。

Django は「バッテリー同梱」という哲学に従い、ほとんどの開発者が「一般的に」実行したいと思うほとんどすべてのことを提供します。すべてが含まれているので、すべて一緒に機能し、一貫した設計原理に従い、そして広範囲かつ最新のドキュメントがあります。また、高速で安全、そして非常にスケーラブルです。Python をベースにしているので、Django のコードは読みやすく、保守も簡単です。

(Django のホームページから) Django を使っている人気のあるサイトには、Disqus、Instagram、Knight Foundation、MacArthur Foundation、Mozilla、National Geographic、Open Knowledge Foundation、Pinterest、Open Stack などがあります。

### Flask (Python)

[Flask](https://flask.palletsprojects.com) は Python 用のマイクロフレームワークです。

最小構成ですが、 Flask は一般的に真面目なウェブサイトを作成することができます。開発サーバーとデバッガーが含まれており、[Jinja2](https://github.com/pallets/jinja) テンプレート、セキュアクッキー、[ユニットテスト](https://en.wikipedia.org/wiki/Unit_testing)、および [RESTful](http://www.restapitutorial.com/lessons/restfulresourcenaming.html) リクエストのディスパッチをサポートしています。良いドキュメントと活発なコミュニティも持っています。

Flask は、特に小規模でリソースに制約のあるシステムでウェブサービスを提供する必要がある開発者 (たとえば、[Raspberry Pi](https://www.raspberrypi.org/) でウェブサーバーを実行する、[Drone コントローラー](https://www.techuseful.com/drone-definitions-learning-the-drone-lingo/)にとって非常に人気があります。

### Express (Node.js/JavaScript)

[Express](http://expressjs.com/ja/) は、[Node.js](https://nodejs.org/ja/) 用の高速で、独創的で、柔軟で最小限のウェブフレームワークです (node は JavaScript を実行するためのブラウザーなしの環境です)。ウェブおよびモバイルアプリケーションに堅牢な機能を提供し、便利な HTTP ユーティリティメソッドと[ミドルウェア](/ja/docs/Glossary/Middleware)を提供します。

Express はクライアントサイドの JavaScript ウェブプログラマーのサーバーサイド開発への移行が容易である、およびリソース効率が良い (基盤となるノード環境は、新しいウェブリクエストごとに別々のプロセスを生成するのではなく、スレッド内で軽量のマルチタスクを使用します) という部分で、非常に人気があります。

Express は最小限のウェブフレームワークであるため、使用するすべてのコンポーネントが組み込まれているわけではありません (たとえば、データベースへのアクセス、ユーザーおよびセッションのサポートは、独立したライブラリーを通じて提供されます)。多くの優れた独立したコンポーネントがありますが、特定の目的に最適なものを見つけるのが難しい場合があります。

[Feathers](https://feathersjs.com/)、[ItemsAPI](https://itemsapi.com/)、[KeystoneJS](http://keystonejs.com/)、[Kraken](https://krakenjs.com/)、[LoopBack](https://loopback.io/)、[MEAN](https://github.com/linnovate/mean)、[Sails](https://sailsjs.com/) などの、多くの一般的なサーバーサイドおよびフルスタックフレームワーク (サーバーサイドフレームワークとクライアントサイドフレームワークの両方を含む) が Express に基づいています。

Uber、Accenture、IBM などを含む多くの有名企業が Express を使用しています (リストは[こちら](http://expressjs.com/en/resources/companies-using-express.html))。

### Deno (JavaScript)

[Deno](https://deno.land/)は、シンプルで現代的での安全な [JavaScript](/ja/docs/Web/JavaScript)/TypeScript ランタイムであり、 Chrome V8 と [Rust](https://www.rust-lang.org/) の上に構築されたフレームワークです。

Deno は、 Rust ベースの非同期ランタイムである [Tokio](https://tokio.rs/) を搭載しており、ウェブページをより高速に提供することができます。また、クライアントサイドで使用するバイナリーコードのコンパイラーが利用できる WebAssembly にも内部的に対応しています。 Deno は、より優れたセキュリティを自然に維持するメカニズムを提供することで、 [Node.js](/ja/docs/Learn_web_development/Extensions/Server-side/Node_server_without_framework) のループホールの一部を埋めることを目指しています。

Deno は次のような機能を含んでいます。

- 既定でセキュリティがあります。 Deno モジュールは、明示的に許可されていない限り、**ファイル**、**ネットワーク**、**環境**へのアクセスの[権限が制限されています](https://lyty.dev/deno/deno-permission.html)。
- TypeScript 対応が**すぐに使えます**。
- 第一級の待機メカニズム。
- 組み込みのテスト機能とコード整形機能 (`deno fmt`)
- (JavaScript) ブラウザーの互換性。 `Deno` 名前空間（またはその機能テスト）を除いて完全に JavaScript で書かれた Deno プログラムは、どの現行ブラウザーでも直接動作するはずです。
- スクリプトを単一の JavaScript ファイルにバンドルします。

Deno は、クライアントサイドとサーバーサイドの両方のプログラミングに JavaScript を使用するための、簡単かつ強力な方法を提供します。

### Ruby on Rails (Ruby)

[Rails](http://rubyonrails.org/) (通常 "Ruby on Rails" と呼ばれる) は、Ruby プログラミング言語用に書かれたウェブフレームワークです。

Rails は Django と非常によく似た設計思想に従っています。 Django と同様に、URL のルーティング、データベースからのデータへのアクセス、テンプレートからの HTML の生成、および {{glossary("JSON")}} または {{glossary("XML")}} としてのデータの書式設定のための標準メカニズムを提供します。それは同様に DRY ("自分で繰り返してはいけない" — 可能であれば一度だけコードを書く)、MVC (model-view-controller) そして他の多くのようなデザインパターンの使用を奨励します。

もちろん、特定の設計上の決定と言語の性質により、多くの違いがあります。

Rails は、[Basecamp](https://basecamp.com/)、[GitHub](https://github.com/)、[Shopify](https://shopify.com/)、[Airbnb](https://airbnb.com/)、[Twitch](https://twitch.tv/)、[SoundCloud](https://soundcloud.com/)、[Hulu](https://hulu.com/)、[Zendesk](https://zendesk.com/)、[Square](https://square.com/)、[Highrise](https://highrisehq.com/) などの有名なサイトに使用されています。

### Laravel (PHP)

[Laravel](https://laravel.com/) は表現力豊かで洗練された構文を持つウェブアプリケーションフレームワークです。Laravel は、次のようなウェブプロジェクトの大部分で使用されている一般的な作業を軽減することで、開発の手間を省くことを試みています。

- [シンプルで高速なルーティングエンジン](https://laravel.com/docs/routing)
- [強力な DI コンテナー](https://laravel.com/docs/container)
- [セッション](https://laravel.com/docs/session)および[キャッシュ](https://laravel.com/docs/cache)ストレージ用の複数のバックエンド
- 表現力豊かで直感的な[データベース ORM](https://laravel.com/docs/eloquent)
- データベースにとらわれない[スキーマの移行](https://laravel.com/docs/migrations)
- [堅牢なバックグラウンドジョブ処理](https://laravel.com/docs/queues).
- [リアルタイムイベントブロードキャスティング](https://laravel.com/docs/broadcasting)

Laravel はアクセシビリティに優れながら強力であり、大規模で堅牢なアプリケーションに必要なツールを提供します。

### ASP.NET

[ASP.NET](https://dotnet.microsoft.com/en-us/apps/aspnet) は、現代のウェブアプリケーションおよびサービスを構築するために Microsoft によって開発されたオープンソースウェブフレームワークです。 ASP.NET を使用すると、HTML、CSS、および JavaScript に基づいてウェブサイトを迅速に作成し、何百万ものユーザーが使用できるように拡張し、ウェブ API、データフォーム、リアルタイム通信などのより複雑な機能を簡単に追加できます。

ASP.NET の差別化要因の 1 つは、[共通言語ランタイム](https://en.wikipedia.org/wiki/Common_Language_Runtime) (CLR) 上に構築されていることです。プログラマは、サポートされている .NET 言語 (C#、Visual Basic など) を使用して ASP.NET コードを書くことができます。多くのマイクロソフト製品と同様に、優れたツール (多くの場合無料)、活発な開発者コミュニティ、および適切に記述されたドキュメントから恩恵を受けます。

ASP.NET は、Microsoft、Xbox.com、Stack Overflow、その他多くのユーザーによって使用されています。

### Mojolicious (Perl)

[Mojolicious](http://mojolicious.org/) は、Perl プログラミング言語用の次世代ウェブフレームワークです。

ウェブの初期の頃、[CGI](https://metacpan.org/module/CGI) と呼ばれる素晴らしい Perl ライブラリーのおかげで、多くの人が Perl を学びました。それは言語についてあまり知らなくても始めるには十分に単純で、続けるには十分に強力でした。Mojolicious は、最先端のテクノロジを使ってこのアイデアを実現しています。

Mojolicious が提供する機能のいくつかは以下の通りです。

- リアルタイムウェブフレームワーク。つまり単一ファイルのプロトタイプを構造化された MVC ウェブアプリケーションに簡単に拡張できます。
- RESTful なルート、プラグイン、コマンド、Perl 風のテンプレート、コンテンツネゴシエーション、セッション管理、フォーム検証、テストフレームワーク、静的ファイルサーバー、CGI/[PSGI](http://plackperl.org) 検出、ファーストクラス Unicode に対応。
- IPv6、TLS、SNI、IDNA、HTTP/SOCKS 5 プロキシー、UNIX ドメインソケット、Comet (ロングポーリング)、キープアライブ、コネクションプーリング、タイムアウト、Cookie、マルチパートおよび gzip 圧縮サポートを備えたフルスタックの HTTP および WebSocket クライアント/サーバー実装。
- CSS セレクターをサポートする JSON および HTML/XML パーサーおよびジェネレーター。
- 隠された魔法のない、とてもきれいで、移植性があり、オブジェクト指向の純粋な Perl API。
- 長年の経験に基づく新鮮なコード、無料およびオープンソース。

### Spring Boot (Java)

[Spring Boot](https://spring.io/projects/spring-boot) は、[Spring](http://spring.io/) が提供している数多くのプロジェクトのうちの 1 つです。[Java](https://www.java.com) を使用してサーバーサイドのウェブ開発を行う良い出発点です。

[Java](https://www.java.com) をベースとした唯一のフレームワークではないことは間違いありませんが、スタンドアローンのプロダクショングレードの Spring ベースのアプリケーションを簡単に実行することができます。これは Spring プラットフォームと他社製ライブラリーの見解に基づいた見方ですが、最小限の手間と設定で始めることができます。

小さな問題にも使用できますが、その強みはクラウドアプローチを使用する大規模アプリケーションを構築することです。通常、複数のアプリケーションが互いに並行して実行され、ユーザーとのインタラクションを提供するものと、バックエンド作業を実行するもの (データベースやその他のサービスへのアクセスなど) のみがあります。ロードバランサーは、冗長性と信頼性を確保したり、ユーザーのリクエストを地理的に処理してレスポンス性を確保したりするのに役立ちます。

## まとめ

この記事では、ウェブフレームワークによって、サーバーサイドコードの開発と保守が容易になることを示しました。また、いくつかの一般的なフレームワークの概要とウェブアプリケーションフレームワークの選択基準についても説明しました。これで、少なくとも自身のサーバーサイド開発用のウェブフレームワークを選択する方法についてのアイデアが得られました。 そうでなくても心配しないでください。コースの後半で Django と Express に関する詳細なチュートリアルを提供して、ウェブフレームワークを実際に使用する経験をいくつか提供します。

このモジュールの次の記事では、方向を少し変えてウェブセキュリティについて考えます。

{{PreviousMenuNext("Learn/Server-side/First_steps/Client-Server_overview", "Learn/Server-side/First_steps/Website_security", "Learn/Server-side/First_steps")}}
