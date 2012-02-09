#<a name = "パラダイム">パラダイム</a>

Functional Programming
 
##<a name = "関数型プログラミング">関数型プログラミング</a>
 
As programs get bigger, they also become more complex and harder to understand. We all think ourselves pretty clever, of course, but we are mere human beings, and even a moderate amount of chaos tends to baffle us. And then it all goes downhill. Working on something you do not really understand is a bit like cutting random wires on those time-activated bombs they always have in movies. If you are lucky, you might get the right one - especially if you are the hero of the movie and strike a suitably dramatic pose - but there is always the possibility of blowing everything up.
 
コードの量が増えるにつれ、プログラムはより複雑に、分かりにくくなってゆきます。いくら自分で賢いと思っていても、私たちは所詮、人間というちっぽけな生き物に過ぎません。わずかな矛盾に直面しただけで頭を抱え、事態は一層複雑さを増してゆくのみでしょう。十分な理解無く物事に取り組むのは、映画でよくあるように時限爆弾のコードを当てずっぽうに切断するのと大差ありません。映画の主人公であればクールに時限爆弾を解除できるかもしれませんが、物事はそううまくは運びません。下手したら大爆発を引き起こすケースもありますからね。
 
Admittedly, in most cases, breaking a program does not cause any large explosions. But when a program, by someone’s ignorant tinkering, has degenerated into a ramshackle mass of errors, reshaping it into something sensible is a terrible labour - sometimes you might just as well start over.
 
もちろん、プログラムを破壊して大爆発が起こるようなことは「まず」ありません。しかし誰かが考えなしにプログラムをいじって、エラーだらけのハチャメチャな状態にしてしまった場合、それをまともな状態に復旧させるのは至難の業です。あるいは最初から作り直したほうがまだましかも知れません。
 
Thus, the programmer is always looking for ways to keep the complexity of his programs as low as possible. An important way to do this is to try and make code more abstract. When writing a program, it is easy to get sidetracked into small details at every point. You come across some little issue, and you deal with it, and then proceed to the next little problem, and so on. This makes the code read like a grandmother’s tale.
 
それゆえプログラマは、コードを可能な限りシンプルに保つ方法を常に模索しているのです。重要なプラクティスとしては、より抽象的なコーディングを目指し、実践することです。プログラムを書く際、その都度些細なディテールにとらわれ、本質から逸脱してしまうことはよくあります。小さな問題にぶつかり、それを処理した後に別の小さな問題にぶつかる。これの繰り返しです。そのおかげで、年寄りの長話のようなコードになってしまうのです。
 
Yes, dear, to make pea soup you will need split peas, the dry kind. And you have to soak them at least for a night, or you will have to cook them for hours and hours. I remember one time, when my dull son tried to make pea soup. Would you be- lieve he hadn’t soaked the peas? We almost broke our teeth, all of us. Anyway, when you have soaked the peas, and you’ll want about a cup of them per person, and pay attention be- cause they will expand a bit while they are soaking, so if you aren’t careful they will spill out of whatever you use to hold them, so also use plenty water to soak in, but as I said, about a cup of them, when they are dry, and after they are soaked you cook them in four cups of water per cup of dry peas.
 
いいこと？エンドウ豆のスープを作るときは、まずスプリットピーを用意しなさい。乾燥したエンドウ豆のことよ。それを必ず一晩は水に浸しておくこと。じゃないと調理するのに何時間かかるか分かったものじゃないわ。そうそう！昔、おっちょこちょいの息子がエンドウ豆スープを作ろうとしたことがあってね、あの子ったらエンドウ豆を水に浸しておかなかったの、信じられる？私たちみんな、歯が折れちゃうかと思ったくらいよ。あら、こんな話をしてる場合じゃなかったわね。それでエンドウ豆を水に浸すんだけど、一人前でカップ一杯分必要よ。水に漬けるとエンドウ豆は少し膨れるから分量には気を付けなさい。うっかりしてると、容器からこぼれちゃうわよ。たっぷりの水で浸しておきなさい。どれだけのエンドウ豆を浸すかって言うと、さっき言ったとおり、カップ一杯分よ。乾燥状態のエンドウ豆をね。それで水に浸してから、カップ一杯分の分量につき4カップの水で調理するの。
 
- 99 -
 
you cook them in four cups of water per cup of dry peas. Let it simmer for two hours, which means you cover it and keep it barely cooking, and then add some diced onions, sliced celery stalk, and maybe a carrot or two and some ham. Let it all cook for a few minutes more, and it is ready to eat.
 
２時間くらいコトコト煮込こみなさい。フタをしてそのまま放っておくだけ。その後角切りにした玉ねぎ、スライスしたセロリを入れるの。あと１～２本のニンジンとかハムとかを入れるのもいいわね。さああと何分か煮込んだら、もう出来上がりよ！
 
Another way to describe this recipe:
 
さて、このレシピを次のように言い換えてみましょう。
 
Per person: one cup dried split peas, half a chopped onion, half a carrot, a celery stalk, and optionally ham.
 
一人前：乾燥スプリットピー1カップ、玉ねぎのみじん切り（１／２個）、ニンジン（１／２本）、セロリのスライス、お好みでハムなど。
 
Soak peas overnight, simmer them for two hours in four cups of water (per person), add vegetables and ham, and cook for ten more minutes.
 
一晩水に浸したエンドウ豆を、一人前につき４カップの水で２時間煮込みます。それから野菜やハムを加え、さらに１０分間調理します。
 
This is shorter, but if you do not know how to soak peas you will surely screw up and put them in too little water. But how to soak peas can be looked up, and that is the trick. If you assume a certain basic knowledge in the audience, you can talk in a language that deals with bigger concepts, and express things in a much shorter and clearer way.
 
このレシピはより簡潔になっていますが、もし作り手がエンドウ豆の浸し方を知らない場合、浸しておく水が少なすぎて失敗するのは目に見えています。しかしエンドウ豆の浸し方は別に調べれば済みますし、そこがミソとなるのです。聞き手がある予備知識を共有している場合、話し手はより大きな文脈で会話ができ、また物事をより簡潔にかつ明確に表現することができます。
 
This, more or less, is what abstraction is.
 
これはまさに、抽象化のプロセスとも言えるのではないでしょうか。
 
How is this far-fetched recipe story relevant to programming? Well, obviously, the recipe is the program. Furthermore, the basic knowledge that the cook is supposed to have corresponds to the functions and other constructs that are available to the programmer. If you remember the introduction of this book, things like while make it easier to build loops, and in Data Structures we wrote some simple functions in order to make other functions shorter and more straightforward. Such tools, some of them made available by the language itself, others built by the programmer, are used to reduce the amount of uninteresting details in the rest of the program, and thus make that program easier to work with.
 
しかしこのやや強引とも言えるレシピのエピソードは、プログラミングと何の関係があるのでしょう？すでにお分かりのことと思いますが、レシピとはプログラムのことです。もっと言えば、料理が前提とする基礎知識は、プログラマが利用できる関数やその他の構成要素に相当します。本書の導入部分で紹介したwhileなどを使えばループ処理が簡単になりますし、データ構造では簡単な関数を用いて、他の関数をコンパクトに、より分かりやすいものにしています。これらの機能は、言語そのものが提供しているものもあれば、プログラマ自身が実装することもあります。プログラムから非本質的な細部を削り、扱いやすくするために利用します。
 
○●○
 
Functional programming, which is the subject of this chapter, produces abstraction through clever ways of combining functions. A programmer armed with a repertoire of fundamental functions and, more importantly, the knowledge on how to use them, is much more effective than one who starts from scratch. Unfortunately, a standard CoffeeScript environment comes with deplorably few essential functions, so we have to write them ourselves or, which is often preferable, make use of somebody else’s code (more on that in Modularity).
 
本章のテーマである関数型プログラミングは、関数を効果的に組み合わせることにより抽象化を実現します。プログラマは、幾つかの基本的な関数、さらにはそれらを利用するためのノウハウを身に付けていれば、何の知識もない状態から始める場合に比べて、圧倒的に効率的なプログラミングが可能になります。しかし残念なことに、標準的なCoffeeScript環境には、必須とも言える関数はほとんど実装されていません。それらは自分たちで用意するか、あるいはもう少しまともな選択肢として、誰か他の開発者のコードを利用することをお勧めします。詳しくはモジュール性をご参照下さい。
 
- 100 -
 
In this chapter we write a set of useful functions to understand how they work and solve problems with them to understand how to use them. In later chapters we will use the larger set of functions in the Underscore library that comes with CoffeeScript.
 
この章では便利な関数を幾つか書いてゆき、それらがどのように作用してどのように問題を解決するのかを通して、利用法を理解してゆきます。本章以降は、ＣｏｆｆｅｅＳｃｒｉｐｔに付属のＵｎｄｅｒｓｃｏｒｅライブラリに収められている、より多くの関数群を扱ってゆきます。
 
There are other popular approaches to abstraction, most notably object-oriented programming, the subject of Object Orientation.
 
抽象化の方法としては、他にも有力な候補があります。最も特筆すべきはオブジェクト指向プログラミングです。詳しくはオブジェクト指向で述べられています。
 
○●○
 
In programming a fundamental operation is performing an action on every element of an array. Many programming languages have borrowed their way of doing this from the C programming language:
 
プログラミングで、配列内の各要素に対して、基本的な操作を行いたい場合があります。多くのプログラミング言語は、Ｃ言語のやり方を真似てこれを実現しています。
 
size_t i;
size_t N = sizeof(thing) / sizeof(thing[0]);
for (i = 0; i < N; ++i) {
do_something(thing[i]);
}
 
That is very ugly, an eyesore if you have any good taste at all. It has been improved somewhat in derived languages like C++ and JavaScript. Other programming languages can have very different approaches17. In CoffeeScript it becomes the reasonably pleasant:
 
まともな感覚を持っている者であれば、これは非常に醜い代物に見えることでしょう。C++やJavaScriptなどのCから派生した言語においては、もう少しましな書き方になります。他のプログラミング言語では、かなり異なった手法を採用しています17。例えばCoffeeScriptでは、このくらい分かりやすくなっています。
 
for i in [0...thing.length] then doSomething thing[i]
# or
# あるいは
for element in thing then doSomething element
 
Still do we have to do this over and over or can it be abstracted? The problem is that, whereas most functions just take some values, com- bine them, and return something, such a loop contains a piece of code that it must execute. It is easy to write a function that goes over an array and prints out every element:
 
しかし、この表現にしても面倒な繰り返し表記は残っています。このプロセスを抽象化することは可能でしょうか？これを考える上で厄介な問題があります。それは、ほとんどの関数が「簡単な引数を取り、それらを組み合わせて、何かを返す」というシンプルな形を取っているのに対して、今述べたようなループには「実行すべきコードそのもの」が含まれているということです。配列を受け取って、各要素を出力する関数を書くのは簡単です。
 
printArray = (array) ->
for element in array
show element
return
 
 
 
17 In Mathematica a function can be set as listable - eliminating the need for a loop:
 
17 Mathematicaでは関数はリスタブルとして定義でき、繰り返し処理の記述を省ことができます。
 
f[x_] := If[x > 0, Sqrt[x], Sqrt[-x]]; SetAttributes[f, Listable];
 
- 101 -
 
But what if we want to do something else than print? Since ‘doing something’ can be represented as a function, and functions are also values, we can pass our action as a function value:
 
ここで、出力以外のことをしたくなった場合はどうすればいいでしょうか？実は「何かを行う」ということは関数として表現可能であり、かつ関数そのものも値として扱えるため、その「何かを行う」関数自身を別の関数に引数として渡すことができるのです。
 
forEach = (array, action) ->
for element in array
action element
#return
forEach ['Wampeter', 'Foma', 'Granfalloon'], show
 
In CoffeeScript most statements are expressions that return a value, that is also the case with the for statement. A return statement at the end of forEach will make it return undefined. Here forEach is allowed to return its value, when we get to the map function you will see why.
 
CoffeeScriptでは、ほとんどの命令文の正体は値を返す式ですが、それはfor構文にも当てはまります。最後にreturn文があれば、forEachはundefinedを返します。ここではforEachはその値を返しています。何故そうするのかは、map関数を使う際に明らかになります。
 
By making use of an anonymous function, something just like a for loop can be written as:
 
匿名関数を利用すれば、forループのようなものは次のように書くことができます。
 
sum = (numbers) ->
total = 0
forEach numbers, (number) -> total += number
total
show sum [1, 10, 100]
 
Note that the variable total is visible inside the anonymous function because of the scoping rules. Also note that this version is hardly shorter than the for loop.
 
スコープ規則により、変数totalは匿名関数内でアクセス可能です。また、このバージョンは、forループと比べてもコードの長さはほとんど変わりません。
 
You do get a variable bound to the current element in the array, number, so there is no need to use numbers[i] anymore, and when this array is created by evaluating some expression, there is no need to store it in a variable, because it can be passed to forEach directly.
 
配列内の要素が変数numberに格納されているため、numbers[i]などのような表記は不要です。また何かの処理の結果として配列が生成さされる場合でも、forEachにそれを直接渡すことで、わざわざ変数に代入する手間を省くことができます。
 
The cat-code in Data Structures contains a piece like this:               	
 
データ構造のcat-codeには、このようなコードがありました。
 
paragraphs = email.split '\n'
for paragraph in paragraphs
handleParagraph paragraph
 
This can now be written as…
 
これをこのように書き換えることができます。
 
forEach email.split('\n'), handleParagraph
 
On the whole, using more abstract (or ‘higher level’) constructs results in more information and less noise: The code in sum reads ‘for each number in numbers add that number to the total’, instead of… ‘there is this
 
一般的に言えば、抽象的な、あるいは「高次な」構造を利用すれば、より密な情報量でノイズの少ないコードを書くことができます。sum関数のコードは、「配列numbers内の個々の要素をnumberとして取り出し、その値をtotalに加えてゆく」と読むことができます。元々のコードの
 
- 102 -
 
‘there is this variable that starts at zero, and it counts upward to the length of the array called numbers, and for every value of this variable we look up the corresponding element in the array and add this to the total’
 
「ある変数があります。この変数を、0から配列numbersの長さまで数えてゆくわけですが、カウントアップの際に配列内の対応する位置にある要素を参照して、その値をtotalに加えてゆく」と比べてみてください。
 
○●○
 
What forEach does is take an algorithm, in this case ‘going over an array’, and abstract it. The ‘gaps’ in the algorithm, in this case, what to do for each of these elements, are filled by functions which are passed to the algorithm function.
 
forEachの真髄は、「配列を走査する」というアルゴリズムを抽象化することにあります。「配列内の各要素に対して何を行うか」という肝心のアルゴリズムの「中身」は、forEach関数に引数として渡される関数が実現してくれます。
 
Functions that operate on other functions are called higher-order functions. By operating on functions, they can talk about actions on a whole new level. The makeAddFunction function from Functions is also a higherorder function. Instead of taking a function value as an argument, it produces a new function. Higher-order functions can be used to generalise many algorithms that regular functions can not easily describe. When you have a repertoire of these functions at your disposal, it can help you think about your code in a clearer way: Instead of a messy set of variables and loops, you can decompose algorithms into a combination of a few fundamental algorithms, which are invoked by name, and do not have to be typed out again and again.
 
他の関数上で作用する関数のことを、高階関数と呼びます。関数が関数を処理するという視点は、物事の処理に関して全く新しい地平を切り開いてくれます。関数で紹介されていたmakeAddFunctionも、高階関数の一つです。この場合関数を引数に取る代わりに、関数を戻り値として返します。高階関数なら、通常の関数で実現の難しい多くのアルゴリズムを記述することが可能です。これらの関数を身につけ自在に操ることができれば、より分かりやすいコーディングを行う手助けとなるでしょう。ごちゃごちゃした変数やループを使うのではなく、問題のアルゴリズムを幾つかの本質的なアルゴリズムの組み合わせに分割し、各々を必要に応じて呼び出すことによって、同じコードを何度も打ち込む手間が省けます。
 
Being able to write what we want to do instead of how we do it means we are working at a higher level of abstraction. In practice, this means shorter, clearer, and more pleasant code.
 
「どのように実行するか」ではなく「何を実行するか」を書くことは、作業をより高度な抽象度にまで高めてくれます。それはより短く明確で、かつ快適なコーディングを保証します。
 
○●○
 
Another useful type of higher-order function modifies the function value it is given:
 
また別の使い方として、高階関数は、引数として与えられた関数をカスタマイズすることもできます。
 
negate = (func) ->
(x) -> not func x
isNotNaN = negate isNaN
show isNotNaN NaN
 
The function returned by negate feeds the argument it is given to the original function func, and then negates the result. But what if the function you want to negate takes more than one argument? You can get access to any arguments passed to a function with the arguments array, but how
 
negateが返す関数は、元々のfunc関数に引数を与えて、その結果に対して否定演算を行います。ここで、否定演算を適用したい関数が、二つ以上の引数をとる場合はどうしたらいいでしょうか？
 
- 103 -
 
You can get access to any arguments passed to a function with the arguments array, but how do you call a function when you do not know how many arguments you have?
 
関数に渡した引数はargumentsという配列から取得することはできますが、引数が幾つ必要であるか分からない場合、どのようにして関数を呼び出せばよいでしょうか？
 
Functions18 have a method called apply, which is used for situations like this. It takes two arguments. The role of the first argument will be discussed in Object Orientation, for now we just use null there. The second argument is an array containing the arguments that the function must be applied to. Now you know the underlying arguments mechanism remember that you can also use splats…
 
関数オブジェクト18はapplyと呼ばれる関数を持っており、これは次のような場合に用います。まずapply関数は二つの引数を取ります。1番目の引数に関しては、オブジェクト指向の説明をご覧下さい。ここではシンプルにnullを使います。2番目の引数には、対象の関数が必要とする引数を配列として入れます。ここでunderlying argumentsを使うこともできますし、スプラット（…）を使うこともできます。
 
show Math.min.apply null, [5, 6]
negate = (func) ->
-> not func.apply null, arguments
negate = (func) ->
(args...) -> not func args...
 
○●○
 
Let us look at a few more basic algorithms related to arrays. The sum function is really a variant of an algorithm which is usually called reduce or foldl:
 
配列に関して、基本的なアルゴリズムをもう少し紹介したいと思います。実はsum関数は、一般的にreduceやfoldLと呼ばれるものの一例に過ぎません。
 
reduce = (array, combine, base) ->
forEach array, (element) ->
base = combine base, element
base
add = (a, b) -> a + b
sum = (numbers) -> reduce numbers, add, 0
show sum [1, 10, 100]
 
reduce combines an array into a single value by repeatedly using a function that combines an element of the array with a base value. This is exactly what sum did, so it can be made shorter by using reduce… except that addition is an operator and not a function in CoffeeScript, so we first had to put it into a function.
 
reduceは、ベースとなる値を用意し、それに対して配列内の個々の要素を結合することによって、配列を一つの値へと集約します。これはsumの働きと全く同じです。従ってreduce…を用いてsumをコンパクトに改良することができます。ただCoffeeScriptでは加算は関数ではなく演算子ですから、まず加算を関数で定義する必要があります。
 
 
 
18 Unfortunately, on at least older versions of the Internet Explorer browser a lot of built-in functions, such as alert, are not really functions… or something. They report their type as 'object' when given to the typeof operator, and they do not have an apply method. Your own functions do not suffer from this, they are always real functions.
 
18残念ながら、少なくとも古いバージョンのInternet Explorerにおいては、alertなどの多くのビルトイン関数は、実際には関数としては実装されていません。typeof演算子を使った場合、これらの「関数」は”object”を返します。またこれらはapply関数を持ちません。一方、自分で作成した関数は問題ありません。それらは本当の意味での関数となります。
 
- 104 -
 
Exercise 21
練習問題21
 
Write a function countZeroes, which takes an array of numbers as its argument and returns the amount of zeroes that occur in it. Use reduce.
 
number型の配列を引数に取り、その中に出現する0の数を数える、countZeros関数を作ってください。ただし、その際reduceを使ってください。
 
Then, write the higher-order function count, which takes an array and a test function as arguments, and returns the amount of elements in the array for which the test function returned true. Re-implement countZeroes using this function.
 
そして、配列とテスト関数を引数に取り、配列の要素のうちテスト関数がtrueを返すものの数を数える高階関数countを作ってください。また、この関数を用いてcountZerosを再実装してください。
 
Solution
解答
 
countZeroes = (array) ->
counter = (total, element) ->
total++ if element is 0
total
reduce array, counter, 0
bits = [1, 0, 1, 0, 0, 1, 1, 1, 0]
show countZeroes bits
 
Here is the solution that uses a count function, with a function that produces equality-testers included to make the final countZeroes function even shorter:
 
こちらはcount関数を使った解になります。等価性の評価関数を返す関数を利用することで、最終的なcountZeroes関数をさらに短いものにしています。
 
count = (test, array) ->
reduce array, ((total, element) ->
total + if test element then 1 else 0), 0
equals = (x) ->
(element) -> x == element
countZeroes = (array) ->
count equals(0), array
show countZeroes bits
 
One other generally useful ‘fundamental algorithm’ related to arrays is called map.
 
配列を扱う際に様々な用途に役立つ「基本的アルゴリズム」をもう一つ紹介しましょう。それはmapです。
 
- 105 -
 
called map. It goes over an array, applying a function to every element, just like forEach. But instead of discarding the values returned by function, it builds up a new array from these values.
 
mapはforEachと同様に、配列内の各要素に対して関数を適用します。しかし関数の戻り値を破棄するのではなく、その戻り値から新たな配列を作り出すのです。
 
map = (array, func) ->
result = []
forEach array, (element) ->
result.push func element
result
show map [0.01, 2, 9.89, Math.PI], Math.round
 
Note that the last argument is called func, not function, this is because function is a keyword and thus not a valid variable name. And then:
 
ちなみにfunctionは予約語ですので、変数名としては使えません。従って最後の引数はfuncとしています。さらに続けて、
 
# Leave out result since forEach already returns it
# forEach自体が戻り値を返しているので、resultを省略します
map = (array, func) ->
forEach array, (element) ->
func element
# Leave out func arguments
# 引数のfuncを省略します
map = (array, func) ->
forEach array, func
# Leave out forEach arguments
# forEachの引数を省略します
map = forEach
 
The reduction shows how nicely functions and expressions can be used to shorten a function. If we were concerned with the performance of forEach then inserting a return at the end of its definition would prevent it from collecting the results of the for comprehension and we would have to provide an implementation in map.
 
この一連のプロセスから分かるとおり、複数の関数や表現式をうまく使うことで、一つの関数をコンパクトにまとめることができます。forEachのパフォーマンスが気になるようであれば、定義の最後にreturnを挿入してみましょう。そうすればfor内包表記の計算結果は保存されません。ただしその場合、mapの実装を別に行わなければいけません。
 
○●○
 
There once was, living in the deep mountain forests of Transylvania, a recluse. Most of the time, he just wandered around his mountain, talking to trees and laughing with birds. But now and then, when the pouring rain trapped him in his little hut, and the howling wind made him feel unbearably small, the recluse felt an urge to write something, wanted to pour some thoughts out onto paper, where they could maybe grow bigger than he himself was.
 
むかしむかし、トランシルバニアの山林の奥深く、一人の世捨て人がいました。いつも山中を気ままに歩き、木々に語りかけ、鳥たちとともに笑いあう、そんな生活を送っていました。ある日のことでした。大雨のせいで小さな掘っ立て小屋から出ることができず、おまけにビュービュー吹きすさぶ風の音のせいで、彼は自分がひどくちっぽけな存在になってしまったような気がしました。彼はとにかく何か物を書きたい、取り留めない考え事を紙に綴ってゆけば、こんな惨めな思いから抜け出せるのでは、と思いました。
 
- 106 -
 
After failing miserably at poetry, fiction, and philosophy, the recluse finally decided to write a technical book. In his youth, he had done some computer programming, and he figured that if he could just write a good book about that, fame and recognition would surely follow.
 
詩を書いたり、小説や哲学にも手を出しましたがどれもうまくいきません。世捨て人はついに、一冊の技術書を書くことを決意しました。彼は若い頃にプログラミングの経験があったのです。その時のことをうまく本にできれば、きっと人から評価され、名声を得られることでしょう。
 
So he wrote. At first he used fragments of tree bark, but that turned out not to be very practical. He went down to the nearest village and bought himself a laptop computer. After a few chapters, he realised he wanted to put the book in HTML format, in order to put it on his web-page…
 
そうして彼は書き始めました。最初は木の皮に書いていたのですが、これはあまり現実的ではないことに気づいたようです。それで近くの村に下り、一台のノートパソコンを買ったのです。何章か書き進めた後に、彼は本をHTMLフォーマットにして、ウェブサイトに公開したいと考えるようになりました。
 
Are you familiar with HTML? It is the method used to add mark-up to pages on the web, and we will be using it a few times in this book, so it would be nice if you know how it works, at least generally. If you are a good student, you could go search the web for a good introduction to HTML now, and come back here when you have read it. Most of you probably are lousy students, so I will just give a short explanation and hope it is enough.
 
話は中断しますが、HTMLはご存知でしょうか？HTMLとはウェブページにマークアップを記述する言語のことです。この本にもHTMLは使われていますし、HTMLがどのようなものなのかは、知っておいて損は無いはずです。優秀な生徒であれば、すぐにでもHTMLについて分かりやすく説明したウェブサイトをインターネットでHTMLについて調べ、理解してくれることでしょう。しかしながら大半の優秀ではない学生たちのために、さしあたってHTMLについて簡単な説明をしてゆきます。
 
HTML stands for ‘HyperText Mark-up Language’. An HTML document is all text. Because it must be able to express the structure of this text, information about which text is a heading, which text is purple, and so on, a few characters have a special meaning, somewhat like backslashes in CoffeeScript strings. The ‘less than’ and ‘greater than’ characters are used to create ‘tags’. A tag gives extra information about the text in the document. It can stand on its own, for example to mark the place where a
 
HTMLとは、ハイパーテキストマークアップ ランゲージの略です。HTMLドキュメントは、テキストで書かれています。どのテキストが見出しでどのテキストが紫色かなどの情報―すなわちテキストの構造―を記述するため、幾つかの文字は特別な意味を持っています。CoffeeScriptの文字列におけるバックスラッシュのようなものです。「大なり」と「小なり」の記号が、「タグ」を形成します。タグとは、ドキュメント内のテキストに対して追加の情報を賦与します。
 
- 107 -
 
It can stand on its own, for example to mark the place where a picture should appear in the page, or it can contain text and other tags, for example when it marks the start and end of a paragraph.
 
タグは、ページに表示する画像の位置を指定する時のようにそれ自体完結した要素として扱えますし、あるいは段落の始まりと終わりを示す時のように、テキストや他のタグを内部に含むこともできます。
 
Some tags are compulsory, a whole HTML document must always be contained in between html tags. The HTML version is specified on the first line with the document type, DOCTYPE, so browsers can parse and render it correctly. Here is an example of an HTML5 document:
 
また、幾つかのタグは必須タグです。HTMLドキュメントは、htmlタグの中に書かなければいけません。HTMLのバージョンは、最初の一行目にドキュメントタイプ、すなわちDOCTYPEに指定します。ブラウザはこれを見て、正しくドキュメントを解析しレンダリングを行うわけです。以下はHTML5ドキュメントの例になります。
 
<!DOCTYPE HTML>
<html>
<head>
<meta charset="utf-8"/>
<title>A quote</title>
<title>引用</title>
</head>
<body>
<h1>A quote</h1>
<h1>引用</h1>
<blockquote>
<p>The connection between the language in which we
think/program and the problems and solutions we can
imagine is very close. For this reason restricting
language features with the intent of eliminating
programmer errors is at best dangerous.</p>
 
<p>我々がプログラミングを行う時に用いる言語と、我々が考えうる問題及びその解法との間は、非常に密接な関係がある。この理由によって、プログラマからエラーを取り除くために言語機能に制限を設けることは、ひいき目に見ても危険であると言える。</p>
 
<p>-- Bjarne Stroustrup</p>
<p>-- ビャーネ・ストロヴストルップ</p>
</blockquote>
<p>Mr. Stroustrup is the inventor of the C++
programming language, but quite an insightful
person nevertheless.</p>
 
<p>ストロヴストルップ氏はC++プログラミング言語の開発者はでありますが、それにもかかわらず深い洞察力を持った方です。</p>
 
<p>Also, here is a picture of an ostrich:</p>
 
<p>そしてこちらがダチョウの写真になります：</p>
 
<img src="../img/ostrich.jpg"/>
</body>
</html>
 
Elements that contain text or other tags are first opened with <tagname>, and afterwards finished with </tagname>. The html element always contains two children: head and body. The first contains information about the document, the second contains the actual document.
 
テキストや他のタグを内部に含んだタグは、<タグ名>で始まり、</タグ名>で終わります。HTML要素は、必ず二つの子要素を持ちます。それはheadとbodyです。headにはドキュメントの情報が含まれており、bodyには実際のドキュメントが含まれています。
 
Most tag names are cryptic abbreviations. h1 stands for ‘heading 1’, the biggest kind of heading. There are also h2 to h6 for successively smaller headings. p means ‘paragraph’, and img stands for ‘image’. The img element does not contain any text or other tags, but it does have some extra information, src="../img/ostrich.png", which is called an ‘attribute’. In this case, it contains information about the image file that should be shown here.
 
ほとんどのタグ名は、やや分かりにくい省略形となっています。h1は「見出し１(=heading 1)」を意味します。これは一番大きな見出しです。見出しは他にもh2からh6まで揃っており、数値が大きいほど小さな見出しになります。pは「段落(=paragraph)」を意味し、imgは「画像(=image)」を意味します。img要素は内部にテキストや他のタグを含むことはありませんが、src=”…/img/ostrich.png”のような追加情報を持っています。これは「属性」と呼びます。ここには、表示すべき画像ファイルの情報が書かれています。
 
Because < and > have a special meaning in HTML documents, they can not be written directly in the text of the document.
 
「<」と「>」はHTMLドキュメントにおいて特別な意味を持っているため、ドキュメント内のテキストに直接書くことはできません。
 
- 108 -
 
not be written directly in the text of the document. If you want to say ‘5 < 10’ in an HTML document, you have to write ‘5 &lt; 10’, where ‘lt’ stands for ‘less than’. ‘&gt;’ is used for ‘>’, and because these codes also give the ampersand character a special meaning, a plain ‘&’ is written as ‘&amp;’.
 
例えばドキュメント内で「5 < 10」と書きたい場合、「5 &lt; 10」と書く必要があります。ここでltは「小なり(=less than)」を意味します。そして「&gt;」は「>(=greater than)」を意味します。ここでアンド記号（&）に特別な意味が与えられているため、リテラルの「&」は、「&amp;」と書きます。
 
Now, those are only the bare basics of HTML, but they should be enough to make it through this chapter, and later chapters that deal with HTML documents, without getting entirely confused.
 
今まで述べてきたことは、必要最低限のHTML入門編でしかありません。しかしHTMLドキュメントを扱う本章および次章以降を読み進めてゆく上では、これで十分だと思われます。
 
○●○
 
The prelude has a function viewURL that can be used to look at HTML docu- ments. The example document above is stored in the file '06-Quote.html', so you can view it by executing the following code:
 
preludeには、HTMLドキュメントを表示するための関数viewURLが用意されています。上に挙げたサンプルドキュメントは、「06-Quote.html」に保存されていますので、以下のコードを実行してその内容を表示させてみて下さい。
 
viewURL '06-Quote.html'
 
You can also run a tiny server from your program or the interactive CoffeeScript environment (REPL). It can serve a webpage either from a string variable or from a file. If you have created a web page in a string variable, say stroustrupQuote then you can start the server with:
 
また、プログラムで小さなサーバーを立てたり、インタラクティブなCoffeeScript環境（REPL）を使うことも可能です。それで文字列あるいはファイルからウェブページを表示させることができます。作成したウェブページを、例えばstroustrupQuoteといった変数に格納した場合、次のようにしてサーバーを立ち上げることができます。
 
viewServer stroustrupQuote
 
Or you could give it a filename as its argument. When you are done with the server then you can either type stopServer() or CTRL-C.
 
あるいは、ファイル名を引数として与えても構いません。サーバーを閉じる時は、stopServer()とタイプするか、Ctrl＋Cを押してください。
 
○●○
 
So, picking up the story again, the recluse wanted to have his book in HTML format. At first he just wrote all the tags directly into his manuscript, but typing all those less-than and greater-than signs made his fingers hurt, and he constantly forgot to write &amp; when he needed an &. This gave him a headache. Next, he tried to write the book in Microsoft Word, and then save it as HTML. But the HTML that came out of that was fifteen times bigger and more complicated than it had to be. And besides, Microsoft Word gave him a headache.
 
さて物語を再開しましょう。我らが世捨て人は、自分の本をHTMLフォーマットにしたいと考えています。彼はまず、全てのタグを原稿に直接書いていました。しかし大なり記号小なり記号をいちいちタイピングしてゆくのは、大変な骨折りです。おまけに彼は、アンド記号の必要な箇所に&amp;と書くことをしょっちゅう忘れてしまいます。どうしたらいいものか、彼は頭を抱えて悩み始めました。そこで、次に彼はMicrosoft Wordを使い、原稿をHTMLとして保存してみました。しかし出力されたHTMLは、本来あるべきファイルよりも15倍ほど大きく、複雑なものになってしまいます。さらに悪いことに、Microsoft Wordそのものが使い辛く頭痛の種となってしまいます。
 
The solution that he eventually came up with was this: He would write the book as plain text, following some simple rules about the way paragraphs were separated and the way headings looked. Then, he would write a program to convert this text into precisely the HTML that he wanted.
 
最終的に思いついたソリューションは次の通りです。まず本を飾り気の無い単純なテキストとして書き始めます。しかしそこに、段落の分け方と見出しの付け方に関してシンプルな規則を適用することにしたのです。次に彼は、このテキストを正確にHTMLに変換してくれるプログラムを書きました。
 
The rules are this:
 
規則は、次の通りです。
 
- 109 -
 
1. Paragraphs are separated by blank lines.
1. 各段落は、空行で分けられている
 
2. A paragraph that starts with a ‘%’ symbol is a header. The more ‘%’ symbols, the smaller the header.
2. 「%」記号で始まる段落は、見出しである。「%」記号が多ければ多いほど、見出しは小さくなる。
 
3. Inside paragraphs, pieces of text can be emphasised by putting them between asterisks.
3. 段落中で、アスタリスクに囲まれたテキストは強調表示される
 
4. Footnotes are written between braces.
4. 脚注は、大括弧の間に書く
 
○●○
 
After he had struggled painfully with his book for six months, the recluse had still only finished a few paragraphs. At this point, his hut was struck by lightning, killing him, and forever putting his writing ambitions to rest.
 
6ヶ月にもわたる艱難辛苦に満ちた執筆作業にもかかわらず、世捨て人は、ほんのわずかの段落しか完成させることができていません。掘っ立て小屋は雷に打たれ、彼は大いなる野望を抱えたまま、帰らぬ人となってしまいました。
 
From the charred remains of his laptop, I could recover the following file:
 
こうして黒焦げになったノートパソコンから、私は以下のファイルを復旧させることができました。
 
% The Book of Programming
% プログラミングの本
 
%% The Two Aspects
%%　陰と陽
 
Below the surface of the machine, the program moves.
 
マシンの奥深い場所で、プログラムが動いている。
 
Without effort, it expands and contracts. In great harmony, electrons scatter and regroup. The forms on the monitor are but ripples on the water. The essence stays invisibly below.
 
それはいとも容易く拡大と縮小を繰り広げる。偉大なる調和の元に、電子は離れそして再び集うのだ。モニター上のイメージは、水上のさざなみに如かず。真理は我々の見えないところに存在する。
 
When the creators built the machine, they put in the processor and the memory. From these arise the two aspects of the program.
 
天はPCに、CPUとメモリを与えた。ここからプログラムの陰陽が浮き彫りにされる。
 
The aspect of the processor is the active substance. It is called Control. The aspect of the memory is the passive substance. It is called Data.
 
まずCPUとは、能動的な存在である。これはコントロールと呼ばれる。一方でメモリは、受動的な存在である。これはデータと呼ばれる。
 
Data is made of merely bits, yet it takes complex forms. Control consists only of simple instructions, yet it performs difficult tasks. From the small and trivial, the large and complex arise.
 
データは単純なビットからできているが、複雑な情報の担い手となる。コントロールはシンプルな命令から成り立っているが、それでも難しいタスクを実行することができる。矮小でちっぽけなものから、偉大で複雑なものが生まれるのだ。
 
The program source is Data. Control arises from it. The Control proceeds to create new Data. The one is born from the other, the other is useless without the one. This is the harmonious cycle of Data and Control.
 
プログラムのソースはデータである。コントロールはそこから生じる。コントロールは新しいデータを生成する。一方がもう一方から生まれ、もう一方は一方が存在しないと意味を成さない。これこそがデータとコントロールの調和的な循環である。
 
Of themselves, Data and Control are without structure. The programmers of old moulded their programs out of this raw substance. Over time, the amorphous Data has crystallised
 
データもコントロールも、それ自身は何の構造も持っていない。いにしえのプログラマは、これらの原料を型に流し込むようにプログラムを作り上げていた。
 
- 110 -
 
Over time, the amorphous Data has crystallized into data types, and the chaotic Control was restricted into control structures and functions.
 
時は流れ、無定形のデータはデータ型へと結晶化され、混沌たるコントロールはコントロール構造及び関数へと集約されてゆく。
 
%% Short Sayings
%% 対話
 
When a student asked Fu-Tzu about the nature of the cycle of Data and Control, Fu-Tzu replied 'Think of a compiler, compiling itself.'
 
門人が孔子に、データとコントロールの循環的な性質について問う。孔子これに応えて曰く「コンパイラはどうだい、自分自身をコンパイルしているじゃないか」
 
A student asked 'The programmers of old used only simple machines and no programming languages, yet they made beautiful programs. Why do we use complicated machines and programming languages?'. Fu-Tzu replied 'The builders of old used only sticks and clay, yet they made beautiful huts.'
 
門人が問いて曰く「いにしえのプログラマは、シンプルなマシンしか使わず、プログラミング言語なんてありませんでした。それでも美しいプログラムを書くことができたそうです。ならばどうして私たちに複雑なマシンと複雑なプログラミング言語が必要なのでしょうか？」孔子、これに応えて曰く「そうだね。いにしえの建築家たちは棒切れと粘土しか使わなかったが、それでも美しい掘っ立て小屋を作ることができたがね。」
 
A hermit spent ten years writing a program. 'My program can compute the motion of the stars on a 286-computer running MS DOS', he proudly announced. 'Nobody owns a 286-computer or uses MS DOS anymore.', Fu-Tzu responded.
 
ある隠者が10年かけてプログラムを書き終えた。自らを誇りて曰く「私のプログラムは、MS DOSの動く286マシンで、天体の動きを計算することができる。」孔子、これに応えて曰く「誰も286マシンなんて持っちゃいないし、MS DOSなんて使っちゃいないよ。」
 
Fu-Tzu had written a small program that was full of global state and dubious shortcuts. Reading it, a student asked 'You warned us against these techniques, yet I find them in your program. How can this be?' Fu-Tzu said 'There is no need to fetch a water hose when the house is not on fire.' {This is not to be read as an encouragement of sloppy programming, but rather as a warning against neurotic adherence to rules of thumb.}
 
孔子がグローバル変数や怪しげなショートカットだらけの、小さなプログラムを書き上げた。それを見た門人が問いて曰く「先生は使ってはいけない手法について教えてくれましたよね。それなのに先生のプログラムにはそれらがばっちり使われているじゃないですか。どういうことですか？」孔子、これに応えて曰く「家が燃えていないならば、わざわざ水道ホースを引っ張り出す必要は無いのだよ。」{これは杜撰なプログラミングを勧めるものではない。むしろ原則に固執することの危険性を指摘しているのである。}
 
%% Wisdom
%% 叡智
 
A student was complaining about digital numbers. 'When I take the root of two and then square it again, the result is already inaccurate!'. Overhearing him, Fu-Tzu laughed. 'Here is a sheet of paper. Write down the precise value of the square root of two for me.'
 
門人が、数値に関して愚痴りて曰く「２の平方根を二乗しただけなのに、計算結果が狂っている！」これを聞き孔子、莞爾として笑いて曰く「ここに一枚の紙がある。どうか２の平方根の正確な値を書いてくれないかね。」
 
Fu-Tzu said 'When you cut against the grain of the wood, much strength is needed. When you program against the grain of a problem, much code is needed.'
 
孔子曰く「木理を切る時は、大変な力が必要だ。小さな問題をプログラムで解く時でも、大変な量のコードが必要なのだよ。」
 
Tzu-li and Tzu-ssu were boasting about the size of their latest programs. 'Two-hundred thousand lines', said Tzu-li, 'not counting comments!'. 'Psah', said Tzu-ssu, 'mine is almost a *million* lines already.' Fu-Tzu said 'My best
 
子路と子索が、最近書いたプログラムのサイズで競い合っている。
「俺は20万行書いたぞ！」子路曰く「コメント抜きでだ！」
「ほう」子索曰く「私のは*100万*行を超えたがね。」
 
- 111 -
 
Fu-Tzu said 'My best program has five hundred lines.' Hearing this, Tzu-li and Tzu-ssu were enlightened.
 
孔子曰く「私のベストプログラムは500行だよ。」これを聞き、子路と子索は啓かれる。
 
A student had been sitting motionless behind his computer for hours, frowning darkly. He was trying to write a beautiful solution to a difficult problem, but could not find the right approach. Fu-Tzu hit him on the back of his head and shouted '*Type something!*' The student started writing an ugly solution. After he had finished, he suddenly understood the beautiful solution.
 
門人、眉をしかめてPCの前に座ったまま、数刻微動だにせず。難しい問題を解くために美しいコードを書こうとするも、どうしてもそれを見出せずにいた。孔子が彼の後頭部をたたき、叱り付ける「*とっととコーディングしたまえ！*」門人は汚いコードを書き始める。それを書き上げた時、彼は突如として美しいコードに思い至った。
 
%% Progression
%% 前進
 
A beginning programmer writes his programs like an ant builds her hill, one piece at a time, without thought for the bigger structure. His programs will be like loose sand. They may stand for a while, but growing too big they fall apart{Referring to the danger of internal inconsistency and duplicated structure in unorganised code.}.
 
プログラミング初心者は、まるでアリが塚を築くがごとく、大きな構造を考えずに一気にプログラムを書き始める。そのコードはまるでサラサラの砂のようだ。小さなものならともかく、少し大きなプログラムを組み立てようとすると、たちまち崩れてしまう。{コード内部の一貫性の無さや、重複コードによって生じる危険性を指している}
 
Realising this problem, the programmer will start to spend a lot of time thinking about structure. His programs will be rigidly structured, like rock sculptures. They are solid, but when they must change, violence must be done to them {Referring to the fact that structure tends to put restrictions on the evolution of a program.}.
 
プログラマはこの問題に直面し、構造について多大な時間を費やして考えるようになる。やがてプログラムは、岩彫刻のようにがっしりしたものになってゆく。堅牢なプログラムはしかし、ひとたび変更の必要に迫られたとき、暴力に訴えなければそれを変えることはできない。 {構造そのものが、プログラムの発展を妨げてしまうという傾向を示している}
 
The master programmer knows when to apply structure and when to leave things in their simple form. His programs are like clay, solid yet malleable.
 
真のプログラマは、構造を用いることと単純なコーディングを行うこととのバランス感覚を心得ている。そのプログラムは粘土のように、堅牢かつ柔軟であるのである。
 
%% Language
%% 言語
 
When a programming language is created, it is given syntax and semantics. The syntax describes the form of the program, the semantics describe the function. When the syntax is beautiful and the semantics are clear, the program will be like a stately tree. When the syntax is clumsy and the semantics confusing, the program will be like a bramble bush.
 
プログラミング言語は、シンタクスとセマンティクスを備えたものとして作られた。シンタクスはプログラムの形式を、セマンティクスはその機能をつかさどる。シンタクスが美しくセマンティクスが明確であるならば、プログラムは堂々たる樹木の容をなす。シンタクスが拙く、セマンティクスが混乱していると、プログラムは茨の茂みとなる。
 
Tzu-ssu was asked to write a program in the language called Java, which takes a very primitive approach to functions. Every morning, as he sat down in front of his computer, he started complaining. All day he cursed, blaming the language for all that went wrong. Fu-Tzu
 
子索はJavaと呼ばれる言語でプログラムを書くよう命じられた。Javaは、非常に原始的な関数の使い方を要請する言語である。彼は毎朝PCの前に座っては、文句を言い始める。こいつは全てを滅茶苦茶にしてしまうどうしようもない言語であると、彼は一日中口汚く罵っていた。 
 
- 112 -
 
listened for a while, and then reproached him, saying 'Every language has its own way. Follow its form, do not try to program as if you were using another language.'
 
孔子、これをしばらく聞き、そして彼に近づいて曰く
「どんな言語にもやり方というものがあるのだよ。その形式に従いなさい。決して別の言語を扱うかのごとくプログラムを行ってはいけないよ。」
 
○●○
 
To honour the memory of our good recluse, I would like to finish his HTML-generating program for him. A good approach to this problem goes like this:
 
われらが世捨て人の想いを無駄にしないためにも、ぜひHTML生成プログラムを作ってみましょう。まずこの問題に関して、次のようなアプローチが考えられます。
 
1. Split the file into paragraphs by cutting it at every empty line.
2. Remove the ‘%’ characters from header paragraphs and mark them as headers.
3. Process the text of the paragraphs themselves, splitting them into normal parts, emphasised parts, and footnotes.
4. Move all the footnotes to the bottom of the document, leaving numbers19 in their place.
5. Wrap each piece into the correct HTML tags.
6. Combine everything into a single HTML document.
 
1. ファイルを、空の行で区切って幾つかの段落に分ける
2. ヘッダ行から%記号を取り除き、ヘッダとしてマーキングする
3. 段落内のテキストを処理する。通常部分、強調部分、そして脚注部分へと分割する。
4. 全ての脚注をドキュメントの一番下に移動し、脚注のあった箇所に数字19を入れておく。
5. 各分割部分を正しくHTMLタグでマークアップする
6. 全体を一つのHTMLドキュメントとしてまとめる
 
This approach does not allow footnotes inside emphasised text, or vice versa. This is kind of arbitrary, but helps keep the example code simple.
If, at the end of the chapter, you feel like an extra challenge, you can try to revise the program to support ‘nested’ mark-up.
The whole manuscript is in '06-RecluseFile.text'. You can get it as a string value by calling the readTextFile function in the prelude.
 
ただこの手法では、強調されたテキスト内に脚注を入れることはできませんし、逆もまた無理です。これはやや恣意的なルールですが、代わりにサンプルコードをシンプルにできます。
この章を終えて物足りないと感じるようであれば、ネスト可能なマークアップをサポートするようにプログラムを改良してみてはいかがでしょうか。
原文は「06-RecluseFile.text」に収められています。preludeにあるreadTextFile関数を使って、中身を文字列として取り出してみましょう。
 
recluseFile = readTextFile '06-RecluseFile.text'
 
○●○
 
Step 1 of the algorithm is trivial. A blank line is what you get when you have two newlines in a row, and if you remember the split method that strings have, which we saw in Data Structures, you will realise that this will do the trick:
 
アルゴリズムのステップ１は至極簡単です。空の行は、2つの改行が連続して続いた場合に発生します。ところで、以前データ構造でsplitを使ったのを覚えているでしょうか。この関数を使えばステップ１は簡単に実現できます。
 
paragraphs = recluseFile.split "\n\n"
show "Found #{paragraphs.length} paragraphs."
 
 
 
19 Like this…
19 こんな感じです
 
- 113 -
 
Exercise 22
練習問題22
 
Write a function processParagraph that, when given a paragraph string as its argument, checks whether this paragraph is a header. If it is, it strips of the ‘%’ characters and counts their number. Then, it returns an object with two properties, content, which contains the text inside the paragraph, and type, which contains the tag that this paragraph must be wrapped in, 'p' for regular paragraphs, 'h1' for headers with one ‘%’, and 'hX' for headers with X ‘%’ characters.
 
段落文字列を引数として受け取り、その段落がヘッダかどうかをチェックする関数、processParagraphを作ってみてください。ヘッダの場合、%記号を切り分け、その数を数えてください。それから段落内のテキストを含んだcontentというプロパティ、及び段落をラップするタグを含んだtypeというプロパティ、この2つのプロパティを持ったオブジェクトを返します。ここでtypeには、通常の段落の場合は「p」が入り、%記号が1つの場合は「h1」が入ります。%記号がX個あるのに対して、typeの値は「hX」となります。
 
Solution
解答
 
processParagraph = (paragraph) ->
header = 0
while paragraph[0] == '%'
paragraph = paragraph.slice 1
header++
type: if header == 0 then 'p' else 'h' + header,
content: paragraph
 
show processParagraph paragraphs[0]
 
This is where we can try out the map function we saw earlier.
 
ここで、先ほど紹介したmap関数を試すときが来ました。
 
paragraphs = map recluseFile.split('\n\n'),
processParagraph
show paragraphs[0..2]
 
And bang, we have an array of nicely categorised paragraph objects. We are getting ahead of ourselves though, we forgot step 3 of the algorithm:
 
さあ、これで綺麗に分類された段落オブジェクトのできあがりです。この調子でアルゴリズムその3に進んでゆきましょう。
 
Process the text of the paragraphs themselves, splitting them into normal parts, emphasised parts, and footnotes.
段落内のテキストを処理する。通常部分、強調部分、そして脚注部分へと分割する
 
Which can be decomposed into:
 
この処理は、次のように分解可能です：
 
1. If the paragraph starts with an asterisk, take off the emphasised part and store it.
2. If the paragraph starts with an opening brace, take off the footnote and store it.
 
1. 段落がアスタリスクで始まっている場合、強調部分を取り出し、保存します。
2. 段落が開き中括弧で始まっている場合、脚注を取り出し、保存します。
 
- 114 -
 
3. Otherwise, take off the part until the first emphasised part or footnote, or until the end of the string, and store it as normal text.
4. If there is anything left in the paragraph, start at 1 again.
 
3. それ以外の場合、強調部分もしくは脚注に出会うまで、あるいは文字列の最後までを抜き出し、通常テキストとして保存します。
4. 段落内に文字列が残っている限り、1から処理を繰り返します。
 
Exercise 23
練習問題23
 
Build a function splitParagraph which, given a paragraph string, returns an array of paragraph fragments. Think of a good way to represent the fragments, they need type and content properties.
 
段落文字列を受け取り、段落パーツの配列を返す、splitParagraph関数を作ってみましょう。パーツを表現するための工夫が必要です。パーツはtypeとcontentというプロパティを持っています。
 
The method indexOf, which searches for a character or sub-string in a string and returns its position, or -1 if not found, will probably be useful in some way here.
 
ここではindexOf関数が役に立つでしょう。この関数は、文字列中から文字あるいは部分文字列を検索し、見つかった場合はその位置を、見つからなかった場合は-1を返します。
 
This is a tricky algorithm, and there are many not-quite-correct or way-too-long ways to describe it. If you run into problems, just think about it for a minute. Try to write inner functions that perform the smaller actions that make up the algorithm.
 
アルゴリズムはトリッキーですので、全く正しくない、あるいはあまりに長すぎるものになってしまうかもしれません。困難に直面したときは、立ち止まってちょっとだけ考えてみてください。アルゴリズムを補助する小さな処理を行ってくれる、内部関数を書いてみてみましょう。
 
Solution
解答
 
Here is one possible solution:
 
一つの例として参考にしてみてください。
 
splitParagraph = (text) ->
# Find character position or end of text
# 文字の位置、あるいはテキストの最後を返します
indexOrEnd = (character) ->
index = text.indexOf character
if index == -1 then text.length else index
 
# Return and remove text upto next special
# character or end of text
# 次の特殊文字あるいはテキストの最後までの文字列を返し、それを除きます
takeNormal = ->
end = reduce map(['*', '{'], indexOrEnd),
Math.min, text.length
part = text.slice 0, end
text = text.slice end
part
 
# Return and remove text upto character
# 引数の文字までを返し、取り除きます
takeUpTo = (character) ->
 
- 115 -
 
end = text.indexOf character, 1
if end == -1
throw new Error 'Missing closing ' +
'"' + character + '"'
part = text.slice 1, end
text = text.slice end + 1
part
 
fragments = [];
 
while text != ''
if text[0] == '*'
fragments.push
type: 'emphasised',
content: takeUpTo '*'
else if text[0] == '{'
fragments.push
type: 'footnote',
content: takeUpTo '}'
else
fragments.push
type: 'normal',
content: takeNormal()
fragments
 
Note the over-eager use of map and reduce in the takeNormal function This is a chapter about functional programming, so program functionally we will! Can you see how this works? The map produces an array of positions where the given characters were found, or the end of the string if they were not found, and the reduce takes the minimum of them, which is the next point in the string that we have to look at. If you’d write that out without mapping and reducing you’d get something like this: takeNormalAlternative = ->
 
takeNormal関数内で、mapとreduceが頻繁に使われていることに注目してください。この章は関数プログラミングの章であり、従って関数的なプログラミングを目指しましょう！これがどのように動くか分かりますか？　mapは与えられた文字が見つかった位置、あるいは見つからなかった場合は文字列の最終位置、これらの配列を返します。そしてreduceはそれらの中での最小値を取ります。この値が、文字列内で次に処理を開始する地点になります。mapとreduceを使わなかった場合、関数は例えば次のようになります。 takeNormalAlternative = ->
 
nextAsterisk = text.indexOf '*'
nextBrace = text.indexOf '{'
end = text.length
if nextAsterisk != -1
 
- 116 -
 
end = nextAsterisk
if nextBrace != -1 and nextBrace < end
end = nextBrace
part = text.slice 0, end
text = text.slice end
part
 
Which is even more hideous. Most of the time, when a decision has to be made based on a series of things, even if there are only two of them, writing it as array operations is nicer than handling every value in a separate if statement. (Fortunately, Regular Expressions describes an easier way to ask for the first occurrence of ‘this or that character’ in a string.)
 
このやり方だと、大変恐ろしいことになっていますね。大概の場合、複数の物事に関して決断を下す必要がある時には、たとえそれが2つだけだとしても、配列操作として扱うほうが、それぞれの値を個別のif節で扱うよりも良いコードになります。(幸いなことに正規表現では、文字列中に最初に出てくる「この文字か、あの文字」を簡単に探す方法が説明しています)
 
If you wrote a splitParagraph that stored fragments in a different way than the solution above, you might want to adjust it, because the functions in the rest of the chapter assume that fragments are objects with type and content properties.
 
もし上に挙げた解答以外の方法でパーツを保存するsplitParagraph関数を書いたのであれば、修正することをお勧めします。なぜなら、本章の残りで出てくる関数は、パーツ配列がtypeとcontentの2つのプロパティを持ったオブジェクトの配列であることを前提としているからです。
 
We can now wire processParagraph to also split the text inside the paragraphs, my version can be modified like this:
 
ここからprocessParagraphを連携させて、段落内のテキストを分割します。私の場合、このように修正しました。
 
processParagraph = (paragraph) ->
header = 0
while paragraph[0] == '%'
paragraph = paragraph.slice 1
header++
type: if header == 0 then 'p' else 'h' + header,
content: splitParagraph paragraph
# Adhoc test
# 追加テスト
recluseFile = readTextFile '06-RecluseFile.text'
paragraphs = map recluseFile.split('\n\n'),
processParagraph
show paragraphs, 3
 
Mapping that over the array of paragraphs gives us an array of paragraph objects, which in turn contain arrays of fragment objects. The next thing to do is to take out the footnotes, and put references to them in their place.
 
段落の配列に対してmap処理を行い、段落オブジェクトの配列を取得します。このオブジェクトは、内部にパーツオブジェクトの配列を持っています。次は脚注を取り出し、元の場所に参照点を追加しましょう。
 
Something like this:
 
大体このようになります。
 
extractFootnotes = (paragraphs) ->
 
- 117 -
 
footnotes = []
currentNote = 0
replaceFootnote = (fragment) ->
if fragment.type == 'footnote'
++currentNote
footnotes.push fragment
fragment.number = currentNote
type: 'reference', number: currentNote
else
fragment
forEach paragraphs, (paragraph) ->
paragraph.content = map paragraph.content,
replaceFootnote
footnotes
 
The replaceFootnote function is called on every fragment. When it gets a fragment that should stay where it is, it just returns it, but when it gets a footnote, it stores this footnote in the footnotes array, and returns a reference to it instead. In the process, every footnote and reference is also numbered.
 
全てのパーツに対してreplaceFootnote関数を適用します。移動すべきではないパーツの場合は、関数はそのままその値を返します。脚注だった場合は、その脚注を配列に保存し、脚注への参照を返します。この過程で、全ての脚注とその参照の両方に数字が割り振られることになります。
 
○●○
 
That gives us enough tools to extract the information we need from the file. All that is left now is generating the correct HTML. A lot of people think that concatenating strings is a great way to produce HTML. When they need a link to, for example, a site where you can play the game of Go, they will do:
 
これで、ファイルから必要な情報を抽出するための道具立てがそろいました。残った作業は、正しいHTMLを生成することだけです。多くの人々は、HTMLを作るには文字列の連結が最良であると考えています。例えば、囲碁をプレイできるサイトへのリンクが必要な場合は、このようにすることでしょう。
 
url = "http://www.gokgs.com/"
text = "Play Go!"
linkText = "<a href=\"#{url}\">#{text}</a>"
show linkText
 
(Where a is the tag used to create links in HTML documents.) … Not only is this clumsy, but when the string text happens to include an angular bracket or an ampersand, it is also wrong. Weird things will happen on your website, and you will look embarrassingly amateurish. We would not want that to happen. A few simple HTML-generating functions are easy to write. So let us write them.
 
(ここでaは、HTMLドキュメント内にリンクを作るためのタグを意味します)しかしこれはやり方が拙いだけでなく、文字列が山括弧やアンド記号を含んでいた場合、このタグは間違っていることになります。そうなるとウェブサイトの挙動がおかしくなるでしょうし、「このサイトの作り手はとんでもない素人だ」と判断されてしまうでしょう。そんなことは避けなければいけません。ここでシンプルなHTML生成関数をいくつか書いてみることにします。簡単な作業ですので、早速やってみましょう。
 
○●○
 
- 118 -
 
The secret to successful HTML generation is to treat your HTML document as a data structure instead of a flat piece of text. CoffeeScript’s objects provide a very easy way to model this:
 
HTML生成を成功させるための秘訣は、HTMLをフラットなテキストとしてではなく、データ構造として扱うことです。CoffeeScriptのオブジェクトを使うと、簡単にモデリングを行うことができます。
 
linkObject =
name: 'a'
attributes:
href: 'http://www.gokgs.com/'
content: ['Play Go!']
content:['囲碁をプレイ！']
 
Each HTML element contains a name property, giving the name of the tag it represents. When it has attributes, it also contains an attributes property, which contains an object in which the attributes are stored. When it has content, there is a content property, containing an array of other elements contained in this element. Strings play the role of pieces of text in our HTML document, so the array ['Play Go!'] means that this link has only one element inside it, which is a simple piece of text.
 
各々のHTML要素は、タグ名に相当するnameプロパティを持っています。タグが属性を持つ場合、HTML要素はattributesプロパティを持ち、そこには様々な属性が保存されているオブジェクトが入ります。タグに中身がある場合、要素内に含まれる他のHTML要素の配列を収めたcontentプロパティを持つことになります。String型は、HTMLドキュメント内のテキストの役割を果たします。従って配列[‘囲碁をプレイ！’]は、リンク内にはただ一つの要素、すなわちシンプルなテキストしか含まれていないことを意味します。
 
Typing in these objects directly is clumsy, but we do not have to do that. We provide a shortcut function to do this for us:
 
これらのオブジェクトを直接タイピングするのは面倒です。わざわざそうする必要はありません。ここで手間を省いてくれる関数を作りましょう：
 
tag = (name, content, attributes) ->
name: name
attributes: attributes
content: content
 
Note that, since we allow the attributes and content of an element to be undefined if they are not applicable, the second and third argument to this function can be left off when they are not needed.
 
ここで、attributes や要素のcontent などを適用しない場合、それらにundefinedをセットするものとしましょう。ですので関数の2つ目と3つ目の引数は、必要なければ空にしておけます。
 
tag is still rather primitive, so we write shortcuts for common types of elements, such as links, or the outer structure of a simple document:
 
tag関数はまだ初歩の段階です。リンクやシンプルなドキュメントの外部構造など、HTML要素の基本的な型を作るためのショートカットを用意します。
 
link = (target, text) ->
tag "a", [text], href: target
show link "http://www.gokgs.com/", "Play Go!"
show link "http://www.gokgs.com/", "囲碁をプレイ！"
htmlDoc = (title, bodyContent) ->
tag "html", [tag("head", [tag "title", [title]]),
tag "body", bodyContent]
show htmlDoc "Quote", "In his house at R'lyeh " +
"dead Cthulu waits dreaming."
show htmlDoc “引用”, “ルルイエの館にて” +
          	"死せるクトゥルフ夢見るままに待ちいたり”
 
- 119 -
 
Exercise 24
練習問題24
 
Looking back at the example HTML document if necessary, write an image function which, when given the location of an image file, will create an img HTML element.
必要であればサンプルのHTMLドキュメントの参考にし、画像ファイルの場所を与えるとimg要素を生成するimage関数を作ってください。
 
Solution
解答
 
image = (src) ->
tag 'img', [], src: src
 
When we have created a document, it will have to be reduced to a string. But building this string from the data structures we have been producing is very straightforward. The important thing is to remember to transform the special characters in the text of our document…
 
ドキュメントが完成したら、それを文字列にまで落とし込まなければいけません。これまで作ってきたデータ構造から文字列を組み立てるのは、非常にシンプルなやり方でできます。ここで重要なのは、ドキュメントのテキスト部分の特殊文字を変形処理することです。
 
escapeHTML = (text) ->
replacements = [[/&/g, '&amp;']
[/"/g, '&quot;']
[/</g, '&lt;']
[/>/g, '&gt;']]
forEach replacements, (replace) ->
text = text.replace replace[0], replace[1]
text
 
The replace method of strings creates a new string in which all occurrences of the pattern in the first argument are replaced by the second argument, so 'Borobudur'.replace(/r/g, 'k') gives 'Bokobuduk'. Do not worry about the pattern syntax here - we will get to that in Regular Expressions.
 
文字列が持つreplace関数は、1番目の引数で与えられた正規表現パターンを全て2番目の引数で置換し、新しい文字列として返します。つまり‘Borobudur’.replace(/r/g, ‘k’)は'Bokobuduk’を返します。パターンのシンタクスについては正規表現で説明しますので、今は気にしないで下さい。
 
The escapeHTML function puts the different replacements that have to be made into an array, so that it can loop over them and apply them to the argument one by one.
 
escapeHTMLでは複数の置換を行いますので、それらを配列として用意し、引数に対して一つ一つループで適用してゆくことになります。
 
Double quotes are also replaced, because we will also be using this function for the text inside the attributes of HTML tags. Those will be surrounded by double quotes, and thus must not have any double quotes inside of them.
 
ダブルクォーテーションも置換します。なぜならHTMLタグの属性部分のテキストにもこの関数を使うからです。属性はダブルクォーテーションで囲みます。従ってその中にダブルクォーテーションを含んではいけないのです。
 
Calling replace four times means the computer has to go over the whole string four times to check and replace its content. This is not very efficient.
 
replace関数を4回呼ぶことは、コンピュータが文字列全体を4回チェックし、その内容を置換しなければいけないことを意味します。これはあまり効率的ではありませんよね。
 
- 120 -
 
cient. If we cared enough, we could write a more complex version of this function, something that resembles the splitParagraph function we saw earlier, to go over it only once. For now, we are too lazy for this. Again, Regular Expressions shows a much better way to do this.
 
注意してみると、この関数をもっと複雑にしたものを作ることができそうです。先ほどsplitParagraph 関数で見たように、一度だけの実行で済ませてしまおうというわけです。ただ、面倒ですので今はこの作業は行いません。ここで再び正規表現を使って、さらにベターな方法を実現してみましょう。
 
○●○
 
To turn an HTML element object into a string, we can use a recursive function like this:
 
HTML要素を文字列に変換するには、このように再帰関数を使うことができます。
 
renderHTML = (element) ->
pieces = []
renderAttributes = (attributes) ->
result = []
if attributes
for name of attributes
result.push ' ' + name + '="' +
escapeHTML(attributes[name]) + '"'
result.join ''
 
render = (element) ->
# Text node
# テキストノード
if typeof element is 'string'
pieces.push escapeHTML element
# Empty tag
# 空のタグ
else if not element.content or
element.content.length == 0
pieces.push '<' + element.name +
renderAttributes(element.attributes) + '/>'
# Tag with content
# 内容のあるタグ
else
pieces.push '<' + element.name +
renderAttributes(element.attributes) + '>'
forEach element.content, render
pieces.push '</' + element.name + '>'
 
render element
pieces.join ''
 
Note the of loop that extracts the properties from a CoffeeScript object in order to make HTML tag attributes out of them. Also note that in two
 
CoffeeScriptオブジェクトからプロパティを抽出しているofループに注目してください。ここでHTMLタグに属性を追加しています。
 
- 121 -
 
Also note that in two places, arrays are being used to accumulate strings, which are then joined into a single result string. Why did I not just start with an empty string and then add the content to it with the += operator?
 
また、文字列を貯めるのに使われている配列が2箇所あります。
それぞれ配列の中身が結合され、一つの文字列になるのです。空の文字列に、内容を順次+=演算子で追加してゆくというシンプルな方法を採らないのは何故でしょうか？
 
It turns out that creating new strings, especially big strings, is quite a lot of work. Remember that CoffeeScript string values never change. If you concatenate something to them, a new string is created, the old ones stay intact. If we build up a big string by concatenating lots of little strings, new strings have to be created at every step, only to be thrown away when the next piece is concatenated to them. If, on the other hand, we store all the little strings in an array and then join them, only one big string has to be created.
 
それは新しい文字列－特に大きな文字列－を生成するのは、とてもコストのかかる作業だからです。CoffeeScriptでは、文字列が決して変化しないということを思い出してください。文字列に何かを連結させる際、そこでは新しい文字列が生成され、元の文字列はそっくりそのまま残っているのです。小さな文字列を沢山連結して大きな文字列を作ろうとすれば、その連結過程で、次の文字列を連結するためだけにその都度新しい文字列が生成されてしまいます。逆に小さな文字列を全て配列の中に収めて、それらをjoinするという方法であれば、一つの大きな文字列を生成するだけで済むのです。
 
○●○
 
So, let us try out this HTML generating system…
 
さあ、HTML生成システムを実際に動かしてみましょう。
 
show renderHTML link 'http://www.nedroid.com',
'Drawings!'
'お絵描き！'
 
That seems to work.
 
これは問題なく動くでしょう。
 
body = [tag('h1', ['The Test']),
tag('p', ['Here is a paragraph ' +
'and an image...']),
tag('p', [‘ここに段落と’ +
‘画像が来ます…’]),
image('../img/ostrich.jpg')]
doc = htmlDoc 'The Test', body
doc = htmlDoc 'テスト', body
show renderHTML doc
# Type `stopServer()` or Ctrl-C when done.
# `stopServer()` とタイプするかCtrl-Cを押して終了します。
viewServer renderHTML doc
 
Now, I should probably warn you that this approach is not perfect. What it actually renders is XML, which is similar to HTML, but more structured. In simple cases, such as the above, this does not cause any problems. However, there are some things, which are correct XML, but not proper HTML, and these might confuse a browser that is trying to show the documents we create. For example, if you have an empty script tag (used to put JavaScript into a page) in your document, browsers will not realise that it is empty and think that everything after it is JavaScript. (In this case, the problem can be fixed by putting a single space inside of the tag, so that it is no longer empty, and gets a proper closing tag.)
 
ここで、この方法が不完全なものであるということを指摘しておかなければいけません。この方法では、HTMLに似ていますがもう少し構造的なXMLというものがレンダリングされます。上で見たようなシンプルなケースでは、問題にはなりません。しかし幾つかの要素の中で、XMLとしては正しいものの適切なHTMLではないものがあり、それらが入ったドキュメントを表示させようとすると、ブラウザが正常に動作しないこともあります。例えば空のscriptタグ（ページ内にJavaScriptを入れるためのタグ）がドキュメント内にある場合、ブラウザはそれが空であると理解できず、そのタグ以降のテキストを全てJavaScriptであると判断してしまいます。（この場合、タグの中にスペースを一つ挿入すれば、それは空タグでなくなり閉じタグも正しく解釈されることで、問題は解決します。）
 
- 122 -
 
Exercise 25
練習問題25
 
Write a function renderFragment, and use that to implement another function renderParagraph, which takes a paragraph object (with the footnotes already filtered out), and produces the correct HTML element (which might be a paragraph or a header, depending on the type property of the paragraph object).
 
まずrenderFragment関数を書き、それを利用してrenderParagraph関数を実装してください。renderParagraph関数は、脚注がすでに取り除かれた段落オブジェクトを引数に取り、その段落オブジェクトのtypeプロパティに基づいて、段落やヘッダなどの正しいHTML要素を作ります。
 
This function might come in useful for rendering the footnote references:
 
脚注の参照をレンダリングする際は、この関数を使ってみてください。
 
footnote = (number) ->
tag 'sup',
[link '#footnote' + number, String number]
 
A sup tag will show its content as ‘superscript’, which means it will be smaller and a little higher than other text. The target of the link will be something like '#footnote1'. Links that contain a ‘#’ character refer to ‘anchors’ within a page, and in this case we will use them to make it so that clicking on the footnote link will take the reader to the bottom of the page, where the footnotes live.
 
supタグはその内容を「上付き(=superscript)」として表示します。つまり他のテキストよりも小さく、文字位置が少し上の部分に表示されます。リンクの参照先は「#footnote1」のようになります。「#」を含んだリンクはページ内の「アンカー」を参照し、今回の場合脚注リンクをクリックすればページの下の脚注内容が書かれている部分に飛ぶことになります。
 
The tag to render emphasised fragments with is em, and normal text can be rendered without any extra tags.
 
強調パーツにはemタグが使われ、通常のテキストは余計なタグなしでレンダリングされます。
 
Solution
解答
 
renderFragment = (fragment) ->
if fragment.type == 'reference'
footnote fragment.number
else if fragment.type == 'emphasised'
tag 'em', [fragment.content]
else if fragment.type == 'normal'
fragment.content
 
renderParagraph = (paragraph) ->
tag paragraph.type,
map paragraph.content, renderFragment
 
show renderParagraph paragraphs[7]
 
-123 -
 
We are almost finished. The only thing that we do not have a rendering function for yet are the footnotes. To make the '#footnote1' links work, an anchor must be included with every footnote. In HTML, an anchor is specified with an a element, which is also used for links. In this case, it needs a name attribute, instead of an href.
 
さあゴールはもう目の前です。レンダリング関数が必要な要素は、脚注を残すだけとなりました。「#footnote1」リンクを機能させるために、全ての脚注にアンカーを付ける必要があります。HTMLでは、アンカーはa要素で指定します。これはリンクにも使えます。アンカーにはhref要素ではなく、name要素が必要です。
 
renderFootnote = (footnote) ->
anchor = tag "a", [],
name: "footnote" + footnote.number
number = "[#{footnote.number}] "
tag "p", [tag("small",
[anchor, number, footnote.content])]
 
Here, then, is the function which, when given a file in the correct format and a document title, returns an HTML document:
 
そして次の関数は、正しくフォーマットされたファイルとドキュメントのタイトルを与えると、HTMLドキュメントを返します。
 
renderFile = (file, title) ->
paragraphs = map file.split('\n\n'),
processParagraph
footnotes = map extractFootnotes(paragraphs),
renderFootnote
body = map paragraphs,
renderParagraph
body = body.concat footnotes
renderHTML htmlDoc title, body
 
page = renderFile recluseFile, 'The Book of Programming'
show page
# Type `stopServer()` or Ctrl-C when done.
# `stopServer()` とタイプするかCtrl-Cを押して終了します。
viewServer page
 
The concat method of an array can be used to concatenate another array to it, similar to what the + operator does with strings.
 
配列はconcatメソッドで、他の配列をつなげることができます。文字列に対して＋演算を行うのと同じですね。
 
○●○
 
In the chapters after this one, elementary higher-order functions like map and reduce will always be available from the Underscore library and will be used by code examples. Now and then, a new useful tool is explained and added to this. In Modularity, we develop a more structured approach to this set of ‘basic’ functions.
 
以降の章では、基礎的な高階関数として、Underscoreライブラリに収められているmapおよびreduce関数をコードサンプルで頻繁に使うことになります。この他にも、便利なツールを適宜紹介し説明・使用してゆくことになります。モジュール性では、これらの「ベーシックな」関数に対して、より構造的なアプローチで迫ってゆきます。
 
○●○
 
 
- 124 -
 
In some functional programming languages operators are functions, for example in Pure you can write foldl (+) 0 (1..10); the same in CoffeeScript is reduce [1..10], ((a, b) -> a + b), 0.
 
Pureなどの幾つかの関数型プログラミング言語では、foldl (+) 0 (1..10)のように書くことができます。CoffeeScriptでは同じ処理をreduce [1..10], ((a, b) -> a + b), 0と書きます。
 
A way to shorten this is by defining an object that is indexed by an operator in a string:
 
これをコンパクトに書くには、演算子を文字列で表現し、それをインデックスとしたオブジェクトを定義するというやり方があります。
 
op = {
'+': (a, b) -> a + b
'==': (a, b) -> a == b
'!': (a) -> !a
# and so on
}
show reduce [1..10], op['+'], 0
 
The list of operators is quite long, so it is questionable whether such a data structure improves readability compared to:
 
しかしこれでは演算子のリストは膨大な量になります。このようなデータ構造が、果たして可読性の向上につながるかどうかは疑問です。逆に次のように書いてみるのはどうでしょうか。
 
add = (a, b) -> a + b
show reduce [1..10], add, 0
 
And what if we need something like equals or makeAddFunction, in which one of the arguments already has a value? In that case we are back to writing a new function again.
 
更に、引数の一方がすでに値を持っているようなequalsやmakdAddFunctionのような関数を作りたい場合はどうでしょう？このような場合には、改めて新しい関数を作ってみましょう。
 
For cases like that, something called ‘partial application’ is useful. You want to create a new function that already knows some of its arguments, and treats any additional arguments it is passed as coming after these fixed arguments. A simple version of this could be:
 
ここで「部分適用」という概念が役に立ちます。引数の幾つかの値がすでに分かっており、それらの固定引数に続けて他の引数を渡す、そういった関数を新しく作ってみましょう。単純に書いてしまえば次のようになるはずです。
 
partial = (func, a...) ->
(b...) -> func a..., b...
 
f = (a,b,c,d) -> show "#{a} #{b} #{c} #{d}"
g = partial f, 1, 2
g 3, 4
 
The return value of partial is a function where the a... arguments have been applied. When the returned function is called the b... arguments are appended to the arguments of func.
 
partialの戻り値は、引数「a…」が適用済みの関数となります。こうして得られた関数は「b…」を引数に与えると実行できますが、この引数は実際にはfuncの引数リストに追加されることになります。
 
equals10 = partial op['=='], 10
show map [1, 10, 100], equals10
 
Unlike traditional functional definitions, Underscore defines the order of its arguments as array before action. That means we can not simply say:
 
伝統的な関数定義と異なり、Underscoreでは関数の実行前に引数の順序を配列として定義します。従って次のように単純に書くことはできません。
 
- 125 -
 
square = (x) -> x * x
show map [[10, 100], [12, 16], [0, 1]],
partial map, square # Incorrect

partial map, square # 正しくありません
 
Since the square function needs to be the second argument of the inner map. But we can define another partial function that reverses its arguments:
 
何故ならsquare関数は、内側にあるmapの2番目の引数である必要があるからです。ですので、ここで引数の順序を逆にするpartial関数をもう一つ作ってみましょう。
 
partialReverse = (func, a) -> (b) -> func b, a
 
mapSquared = partialReverse map, square
show map [[10, 100], [12, 16], [0, 1]], mapSquared
 
However it is again worthwhile to consider whether the intent of the program is clearer when the functions are defined directly:
 
しかしここでも、プログラムの意図が、関数を直接定義した時よりも明瞭になっているのかどうかを十分に考慮する必要があります。
 
show map [[10, 100], [12, 16], [0, 1]],
(sublist) -> map sublist, (x) -> x * x
 
○●○
 
A trick that can be useful when you want to combine functions is function composition. At the start of this chapter I showed a function negate, which applies the boolean not operator to the result of calling a function:
 
関数を繋げたいときは、関数合成を行うことをお勧めします。この章の始めに、negate関数を紹介しました。これはboolean型のnot演算子を関数の呼び出し結果に適用するものです。
 
negate = (func) ->
(args...) -> not func args...
 
This is a special case of a general pattern: call function A, and then apply function B to the result. Composition is a common concept in mathematics. It can be caught in a higher-order function like this:
 
関数Aを呼び出し、その結果に関数Bを適用するという、一般的なパターンの特殊例となります。合成は数学上の共通概念です。高階関数において、合成は次のように実現できます。
 
compose = (func1, func2) ->
(args...) -> func1 func2 args...
 
isUndefined = (value) -> value is undefined
isDefined = compose ((v) -> not v), isUndefined
show 'isDefined Math.PI = ' + isDefined Math.PI
show 'isDefined Math.PIE = ' + isDefined Math.PIE
 
In isDefined we are defining a new function without naming it. This can be useful when you need to create a simple function to give to, for example, map or reduce. However, when a function becomes more complex than this example, it is usually shorter and clearer to define it by itself and name it.
 
isDefined関数では、名前を付けることなく新しい関数を定義しています。これは、mapやreduceなどに渡す簡単な関数を作りたい時に使う手法です。ただし、関数がこの例よりも複雑になってきた場合には、関数にきちんと定義して名前を付けてやったほうが、コードはより短くそして簡潔になります。
