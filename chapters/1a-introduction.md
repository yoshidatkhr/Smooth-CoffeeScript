#<a name="パート1.序章">パート1.序章</a>

##<a name = "導入">導入</a>


CoffeeScriptは、Jeremy Ashkenasによって作られた、JavaScriptの輝かしい革命です。この本はMarijn Haverbekeの著書『雄弁なるJavaScript』(”Eloquent JavaScript”)を発展させることを試みています。JavaScriptの代わりとしてのCoffeeScriptは、その大きな変化はともかく、それ以外にも数えきれない程多くの変更が加えられたので説明する過程で加筆修正を行いました。

従って、この本で表現されている全てのものの文責は、ひとえに編集者にあります。OSSと同様の意味合いで、この本はフォークです。オリジナルの著者によって意図された素晴らしい作品を読みたければ、Marijn　Haverbekeの著書『雄弁なるJavaScript』(”Eloquent JavaScript”)を参照してください。

JavaScriptを知る必要はないですが、Smooth CoffeeScriptを読んだ後に、Simon Willisonの著書『JavaScript再入門』(“A re-introduction to JavaScript”)を読めば、デバッグのときや、JavaScriptライブラリを使用する際に役立ち得る概要が分かります。

---

この本で出てくるプログラムの例は、CoffeeScript環境に加えてPreludeファイルを使用します。Preludeファイルには、Underscore.jsの関数ライブラリ、CoffeekupによるHTMLのマークアップ、サーバーサイドWebSockets、QuickCheckテストライブラリが含まれます。これらのライブラリはCoffeeScriptを便利な抽象性とテストツールによって拡張して、気の散るような定型コードを排除し、目の前のタスクへの集中を助けます。

原始的な言語のとても小さな一式でプログラムを表現することは可能ですが、それはすぐに冗長になるし、エラーがでやすい傾向にあります。ここで採用されるアプローチは、まるでプログラミング言語のネイティブの一部であるかのように機能的な積み木の一式をより広く含むことです。これらのより高いレベルの構成の観点で考えることによって、より複雑な問題を、より少ない労力で処理することができます。

正確さを保証するためにテストすることが必要です。これは、特にダイナミック言語や型なし言語で再利用可能なアルゴリズムを開発する際は当てはまります。機能が導入されるやいなや、QuickCheckスタイルのテストケースが積み重なっていくことによって、ライティングテストと前提の宣言が一つの途切れないライティングソフトの一部分になることを意味しています。

CoffeeScriptは、JavaScriptが使用可能なブラウザや環境で使用可能です。下のスクリーンショットはMac OS X、Windows、iOS環境で、同じWebサーバー、クライアントアプリケーションを実行したCoffeeScriptを示しています。


![Alt text](../img/TadaOnMacOSX.png)
![Alt text](../img/TadaOnWin7.png)
![Alt text](../img/TadaOniOS.png)


以下のCoffeeScriptで書かれたプログラムのスクリーンショットは自己完結型アプリケーションの簡潔さを示しています。ここではCoffeekupでマークアップした独自のHTTP Webサーバで、HTML5のWebページが含まれています。ページには『生命の種子』(“Seed of Life”)の描画をCanvas要素で行なっています。Coffeekupは140行未満のCoffeeScriptで、フレームワークもJavaScriptも使われていない、純粋で快適なものです。

	'require './prelude'

	  webpage = kup.render -> doctype 5
	  html ->
	    head ->
		  meta charset: 'utf-8'
		  title 'My drawing | My awesome website' 
		  style '''
			body {font-family: sans-serif}
			header, nav, section, footer {display: block} 
		  '''
		coffeescript ->
	  	  draw = (ctx, x, y) ->
			circle = (ctx, x, y) ->
		  	  ctx.beginPath()
		  	  ctx.arc x, y, 100, 0, 2*Math.PI, false
		  	  ctx.stroke()
	      ctx.strokeStyle = 'rgba(255,40,20,0.7)' 
	      circle ctx, x, y
		  for angle in [0...2*Math.PI] by 1/3*Math.PI
	        circle ctx, x+100*Math.cos(angle), 
	       			    y+100*Math.sin(angle)
	 	  window.onload = ->
	  	    canvas = document.getElementById 'drawCanvas' 
	  	    context = canvas.getContext '2d'
	        draw context, 300, 200	
	  body ->
	    header -> h1 'Seed of Life'
	    canvas id: 'drawCanvas', width: 600, height: 400

	http = require 'http'		
	server = http.createServer (req, res) ->
	  show "#{req.client.remoteAddress} #{req.method}#{req.url}}" 
	  res.writeHead 200, 'Content-T	  y	pe': 'text/html'
	  res.write webpage
	  res.end()

	server.listen 3389
	show 'Server running at' show server.address() `

