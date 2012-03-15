###<a name = "ソフトウェア">ソフトウェア</a>

Smooth　CoffeeScriptはCoffeeScript言語についてですので、ツールの情報については以下のウェブサイトを参照してください。あなたをスタートさせる。。。

-	The CoffeeScript language (1.1.1 / MIT) from Jeremy Ashkenas
-	The Underscore library (1.1.0.FIX / MIT) included in CoffeeScript
-	The Coffeekup library (0.2.3 / MIT) from Maurice Machado
-	TranslatedwsWebSockets(MIT)fromJacekBecela
-	The qc testing library1 (2009 / BSD) from Darrin Thompson

必要なライブラリは標準的なCoffeeScriptに対応していて、src/preludeディレクトリに含まれています。UnderScore.js、websocket、CoffeekupはCoffeeScriptで書かれており、少しでもこの本読んで理解した読者には十分理解できます。doccoで作られたドキュメントはsrc/docsにあります。

---

開発環境を設定するには、まず最初に coffeescript.orgの手順に従います。Windowsを使用している場合、あなたは好みのブラウザをデフォルトでPrelude環境に適応させることができます。また、ブラウザが必要とするとき、WebSocketsを有効にする必要がある場合もあります。

CoffeeScriptをサポートするようにテキストエディタを設定するには、いくつかのリソースをwebで見つけることができます。cross platform Sublime Text 2 editorでTextMateを使用する例に関しては、パッケージ以下のCoffee Scriptディレクトリにハンドルしています。これを設定すると、構文の強調表示、コードスニペット、およびコード補完をに対応します。

ビルドファイルを追加すると、ボタンを押すだけでCoffeeScriptの実行を取得できます。
CoffeeScript.sublimeを構築して、OSに応じてパスを変更し、インストールファイルに名前を付けます。こんな感じに
	
	{
	  "cmd": ["/Users/username/bin/coffee", "$file"], 	  "file_regex": "^Error: In (...*?),
					  Parse error on line ([0-9]*):?", 
	  "selector": "source.coffee"

	} 

最後に、再びご使用のプラットフォーム用に調整した端末とタイプでコマンドラインを開き、次に、対話型評価環境があなたを待っています。
cd path-to-smooth-coffeescript/src coffee -r ./prelude 

CoffeeScriptコンパイラの詳細については、 usage section をお読みください。あなたはcoffee filename.coffeeでサンプルを実行することができます。

---

Smooth CoffeeScriptは、2つのエディションで提供されます。ソリューションを使用する場合と使用しない場合。srcディレクトリ内にある章のソースコードファイルで完了します。すべてのファイルのコピーがsrc-no-solutions内にあり、これらのファイルは独自のソリューションを挿入することができます。

本からさらに得るには、テキストエディタを起動して、src-no-solutionsで、あなたが呼んでいる章のソースファイルを開きます。ワイド画面のディスプレイをお持ちの場合は、本を片側に、テキストエディタをもう片側に配置。サンプルを読みながらプログラムを実行することができるので、コードを試しに書いて、演習を解いてみてください。作業ファイルのコピーを作成すれば、簡単に実験を元に戻すこともできます。実験で動けない場合は(ディスプレイが大きくなくて)、srcディレクトリ内のファイルからの私のコードをコピーして、先に進む前にそれを少し研究してください。ソースファイルは、周辺のコードに合うようにコードをインデントすることを忘れずに行ってください。

両方のエディションと付属のソースファイルは次のサイトからDownloadできます。
http://autotelicum.github.com/Smooth-CoffeeScript/
