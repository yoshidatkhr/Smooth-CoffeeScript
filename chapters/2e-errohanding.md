##<a name = エラー処理>"エラー処理"</a>




全てが予定通りに（なった時に）動作するプログラムを書くのは良いことです。予期せぬ事態に遭遇した時に正しく動作するプログラムを作成する場面こそ、本当の実力が試されるでしょう。
プログラムが遭遇しうる問題のある状況は、２つのカテゴリ：プログラマのミスと正真正銘の問題に分類されます。もし関数に必要な引数を渡し忘れた場合は、第一の例にあたります。一方で、ユーザーに名前を求めて空の文字列が返ってきたような場合、それを防ぐことは出来ません。
一般的に、プログラマーエラーは見つけて修正するしかありません。正真正銘のエラーの場合、コードをチェックし問題解決に関して何らかの解決手段（たとえば再度名前を入力させるなど）を講じましょう。または、少なくともエラーを防げないとしても正しい方法で終わりましょう。

---

これらのカテゴリでどちらかの問題に陥ったかを決めることは重要です。例えば、前のpower関数で考えてみましょう。

	power = (base, exponent) ->
	  result = 1
	  for count in [0..exponent]
		result *= base
	result


何人かのギークがpower ‘Rabbit’,4 と読びだそうとすると、これは明らかにプログラマーエラーとなりますが、power 9,0.5で はどうでしょうか？この関数は小数の指数を扱うことは出来ませんが、1/2乗という表現で数学的には問題ありません。（Math.powはそれを扱うことが出来ます）。関数がどの入力を受け入れるのかはっきりしない状況では、明示的なコメントの中に許容される引数の種類を明記することをお勧めします。

---

関数がそれ自体を解決できないという問題に遭遇した場合、何をすべきでしょうか？DataStructures　で、between関数を書きました。

	between = (string , start, end) ->
	  startAt = string.indexOf start
	  startAt += start.length
	  endAt = string.indexOf end, startAt
	  string[startAt...endAt]

与えられたstartとendがstringの中に現れなければ、indexOf は-1を返し、betweenは全く意味不明な戻り値を返します。
between('Your mother!', '{-', '-}') は 'our mother'を戻します。
プログラムが実行され、関数がそのように呼び出された場合、呼び出されたコードは期待通りのStringの値を得て、めでたく処理を継続することが出来ます。しかし値は間違っており、それは更に間違った状態で終わります。また、運が悪ければ、この誤りは20の他の関数を通過した後に問題を引き起こします。そのようなケースでは、問題が発生した場所を見つけるのは非常に困難です。
時には、不正な値が与えられ関数の誤動作に気が付くまで、これらの問題に対して無関心になるかもしれません。関数がほんの数か所からしか呼び出されていなのが確かであり、呼び出し元が適切な入力を与えていると証明できる場合、一般的には、関数を肥大化させ醜くする必要はありません。
しかし、ほとんどの場合、表面化されず失敗した関数は、扱い辛く、そしてさらに厄介です。betweenの呼び出し元のコードが全てが上手くいったかどうか知りたい場合にはどのようにすれば良いでしょうか？
現時点では、betweenの全ての動作を再実行するか自分自身の結果とbetweenの結果をチェックしなければ、知ることは出来ません。それは良くないです。それが失敗した時、falseまたはundefinedのような特別な値をbetweenに返すことが一つの解決策になります。

	between = (string , start, end) ->
	  startAt = string.indexOf start
	  if startAt == -1 then return
	  startAt += start.length
	  endAt = string.indexOf end, startAt
	  if endAt == -1 then return
	  string[startAt...endAt]

エラーチェックが通常の関数よりも見にくくなることが解ります。しかし今回呼び出すコードは次のことを行うことが出来ます。

	prompt "Tell me something", "", (answer) ->
	  parenthesized = between answer , "(", ")"
	  if parenthesized?
		show "You parenthesized '#{parenthesized}'."

---

エラーを示す為に特別の値を返すことは、多くの場合、非常におススメです。しかしながらそれはマイナス面を持っています。最初に、関数が可能な限り全ての値を戻すことが出来たらどうでしょうか？例えば、配列の最後の要素を取り出すこの関数を考えてみましょう。

	lastElement = (array) ->
	  if array.length > 0
		array[array.length - 1]
	  else
		undefined
	show lastElement [1, 2, undefined]

arrayは最後の要素を持っているでしょうか？lastElement の戻り値を見ると、言うまでもありません。
特別な値を返す2つめの問題は、それが非常に多くの混乱に結びつく場合があるということです。コードが10回 between を呼び出す場合、それはundefined が返されたかどうか10回チェックする必要があります。また、between 関数が失敗から回復する手段を持たない場合、bettweenの戻り値をチェックしなければなりません、そしてそれがundefinedの場合、この関数は、 undefined または特別な値を返すことが出来ますが、呼び出し元は更にその値をチェックすることになります。
時々、奇妙なことが起こりますがその際は、今行っている処理を中断して、その問題の解決法を知っている場所へ直ちに戻ることが現実的でしょう。さて、幸運なことに、多くのプログラミング言語では、そのようなものを提供しています。たいてい、それらは例外処理と呼ばれます。

---

例外処理の支える考え方は次の通りです。コードは例外を発生（または投げる）することが出来ます。例外とは、一つの値として扱います。例外を発生されることは、関数からの凄い戻り方（super-charged return）に多少似ています。
- それはちょうど、現在の関数から抜け出すだけではなく、プログラムを実行したトップレベルの呼び出しまで戻ります。これはスタックのアンワインドと呼ばれています。
例外は、途中のコールコンテキストを全て無視して、スタックを一気に遡ってゆきます。

これらは常にスタックのベースに直ちに一気に遡ってゆくのであれあば、例外というものは利用価値はありません。それは、プログラムをぶち壊す新しい手段にすぎません。
幸運なことに、このスタックを任意の場所で止めることが可能です。
一気に遡っていく例外を「キャッチ」し、何らかの対処を行った上で、キャッチした箇所から処理を再開してゆくことができるのです。例：

	lastElement = (array) ->
	   if  array. length  >  0
	      array[array.length  -  1]
	   else
         throw ‘Can not take the last element’  +
               ‘ of  an  empty  array.’

	lastElementPlusTen  =  (array)  -  >
	   lastElement(array)  +  10


	try
	  show lastElementPlusten  []
	catch  error
	   show  ‘Something went wrong:  ‘  +  error
	   
throw は例外を発生される時に使用されるキーワードです。キーワード try は例外の妨げを設定します。その後のブロックの中にあるコードに例外が発生した時、catchブロックが実行されます。
cacth の後に括弧で指定された変数は、ブロックの中で与えられた例外の値の名前です。lastElementPlusTen関数が、lastElementが誤るかもしれない可能性を完全に無視することに注意してください。error-handlingコードはエラーが生じるポイント、およびそれが扱われるポイントで必要になる―これは例外の中で大きなアドバンテージです。関数の中では、それについて全てを忘れることがあります。まあ、ほとんど。

---

次のことを考えてみましょう。processThing　関数は、currentThingが本体の実行中に特定のことを示すトップレベルの変数に設定しています。その結果、他の関数もそれにアクセスすることが出来ます。一般に、単なる引数として渡すことができますが、暫く考えるとそれは実用的ではありません。関数が終了した時、currentThingはnullに戻すべきです。

	currentThing = null
	processThing = (thing) ->
	　　if currentThing != null
	　　　　throw 'Oh no! We are already processing a thing!'
	　　currentThing = thing
	　　# do complicated processing...
	　　currentThing = null

しかし、複雑な処理の場合、どのように例外は発生すれば良いでしょうか？
その場合にはprocessThingへの呼び出しは、例外によってスタックからスローされます。そして、
currentThingはnullにリセットされることはありません。

try 文は’no matter what happens, run this code after trying to run the code in the
try block’の後にキーわーそを続けることが出来ます。
関数で何かをクリーンアップする必要がありましたら、クリーンアップコードがginallyブロックに配置する必要があります。

	processThing = (thing) ->
	  if currentThing != null
	    throw 'Oh no! We are already processing a thing!'

	currentThing = thing
	try
	  # do complicated processing...
	finally
	  currentThing = null

---

プログラムにおける多くのエラーがCoffeeScript環境に例外を発生させます。例えば。

	try
	　　show Sasquatch
	catch error
	　show 'Caught: ' + error.message

このようなケースでは、特別なエラーオブジェクトが発生します。これらは問題の説明を含むメッセージプロパティを常に設定します。新たなキーワードとエラーコンストラクターを使用して類似オブジェクトを発生させることが可能です。

	throw new Error 'Fire!'

---

キャッチされることなく、例外がスタックの底まで行く場合、それは環境によって扱われます。
これが意味することは、異なるブラウザやエンジンによって異なります。時々何かの種類のログにエラーが記載されますし、時々ウインドウにエラーの記述をポップアップされます。CoffeeScript REPLの中の入力したコードによって発生されたエラーは、コンソールによって補足され、スタックトレースと共に表示しました。

---

ほとんどのプログラマはピュアなエラー処理機構を検討しています。本質的には、それらは、プログラムのコントロール・フローに影響を及ぼすことに最適な別のやり方があります。
例えば、それらは、帰納的関数の中の一種のbreakステートメントとして使用することができます。これは、オブジェクト、およびオブジェクトがその内部に格納されているかどうかを決定する
少なくとも7つのtrueの値が含まれている奇妙な関数です。

	FoundSeven = {}
	hasSevenTruths = (object) ->
	  counted = 0
	  count = (object) ->
	   for name of object
	      if object[name] == true
	        if (++counted) == 7
	          throw FoundSeven
	        if typeof object[name] == 'object'
	          count object[name]
	  try
	    count object
	    return false
	  catch exception
    if exception != FoundSeven
      throw exception
    return true

内部関数の数は、引数の一部であるすべてのオブジェクトのために再帰的に呼ばれます。変数のカウンターが7に到達した時、数え続ける必要はありませんが、それ以下に更に呼び出しがあるかもしれないので、数えることをやめる必要はないだろう。ですから、私達のすることは、カウントされる全ての呼び出しが正しく飛び出すことを制御し、catchブロックに到達する値をスローすることとなります。しかし、単に例外の場合にtrueを返すことは正しくありません。何か他に誤っているかもしれないので、私たちは、例外が特にこの目的のために作成されたオFoundSevenオブジェクトかどうか最初にチェックします。そうでない場合は、このcatchブロックはそれを処理する方法を知らないので、それを再度発生させます。これは、エラー状態を扱う場合にも一般的であるパターンです。catchブロックが例外のみを処理し、その処理方法を知っていることを、確認する必要があります。いくつかの例として、String値を返す為にこの章を行うことはとても良いアイディアです。何故なら例外の型を認識することは難しいからです。オブジェクト指向に述べられているように、よりよい考えは、FoundSevenオブジェクトのようなユニークな値を使用するか、新しいタイプのオブジェクトを導入することです。















	   
