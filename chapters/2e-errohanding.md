##<a name = エラー処理>"エラー処理"</a>

Kazuki Suda  ■main translater
Takashi Tsuda ■main translater

Takaichi Qubo
Takahiro Yoshida

Writing programs that work when everything goes as expected is a good
start. Making your programs behave properly when encountering unexpected
conditions is where it really gets challenging.
The problematic situations that a program can encounter fall into two categories:
Programmer mistakes and genuine problems. If someone forgets
to pass a required argument to a function, that is an example of the first
kind of problem. On the other hand, if a program asks the user to enter a
name and it gets back an empty string, that is something the programmer
can not prevent.
In general, one deals with programmer errors by finding and fixing them,
and with genuine errors by having the code check for them and perform
some suitable action to remedy them (for example, asking for the name
again), or at least fail in a well-defined and clean way.

全てが予定通りに（なった時に）動作するプログラムを書くのは良いことです。予期せぬ事態に遭遇した時に正しく動作するプログラムを作成する場面こそ、本当の実力が試されるでしょう。
プログラムが遭遇しうる問題のある状況は、２つのカテゴリ：プログラマのミスと正真正銘の問題に分類されます。もし関数に必要な引数を渡し忘れた場合は、第一の例にあたります。一方で、ユーザーに名前を求めて空の文字列が返ってきたような場合、それを防ぐことは出来ません。
一般的に、プログラマーエラーは見つけて修正するしかありません。正真正銘のエラーの場合、コードをチェックし問題解決に関して何らかの解決手段（たとえば再度名前を入力させるなど）を講じましょう。または、少なくともエラーを防げないとしても正しい方法で終わりましょう。

　　 ○●○

It is important to decide into which of these categories a certain problem falls. 
For example, consider our old power function:

power = (base, exponent) ->
result = 1
for count in [0..exponent]
result *= base
result

これらのカテゴリでどちらかの問題に陥ったかを決めることは重要です。例えば、前のpower関数で考えてみましょう。

When some geek tries to call power 'Rabbit', 4, that is quite obviously a programmer error, but how about power 9, 0.5? The function can not handle fractional exponents, but, mathematically speaking, raising a number to the ½ power is perfectly reasonable (Math.pow can handle it). In
situations where it is not entirely clear what kind of input a function accepts,it is often a good idea to explicitly state the kind of arguments that are acceptable in a comment.

何人かのギークがpower ‘Rabbit’,4 と読びだそうとすると、これは明らかにプログラマーエラーとなりますが、power 9,0.5で はどうでしょうか？この関数は小数の指数を扱うことは出来ませんが、1/2乗という表現で数学的には問題ありません。（Math.powはそれを扱うことが出来ます）。関数がどの入力を受け入れるのかはっきりしない状況では、明示的なコメントの中に許容される引数の種類を明記することをお勧めします。

　　 ○●○

If a function encounters a problem that it can not solve itself, what should it do? In Data Structures we wrote the function between:

between = (string , start, end) ->
startAt = string.indexOf start
startAt += start.length
endAt = string.indexOf end, startAt
string[startAt...endAt]

関数がそれ自体を解決できないという問題に遭遇した場合、何をすべきでしょうか？DataStructures　で、between関数を書きました。

If the given start and end do not occur in the string, indexOf will return -1 and this version of between will return a lot of nonsense:
between('Your mother!', '{-', '-}') returns 'our mother'. 
When the program is running, and the function is called like that, the code
that called it will get a string value, as it expected, and happily continue doing something with it. But the value is wrong, so whatever it ends up doing with it will also be wrong. And if you are unlucky, this wrongness only causes a problem after having passed through twenty other functions.
In cases like that, it is extremely hard to find out where the problem started.
In some cases, you will be so unconcerned about these problems that you do not mind the function misbehaving when given incorrect input. For example, if you know for sure the function will only be called from a few places, and you can prove that these places give it decent input, it is generally not worth the trouble to make the function bigger and uglier so that it can handle problematic cases.
But most of the time, functions that fail ‘silently’ are hard to use, and even dangerous. What if the code calling between wants to know whether everything went well? At the moment, it can not tell, except by re-doing all the work that between did and checking the result of between with its own result. That is bad. One solution is to make between return a special value, such as false or undefined, when it fails.

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

You can see that error checking does not generally make functions prettier.
But now code that calls between can do something like:

エラーチェックが通常の関数よりも見にくくなることが解ります。しかし今回呼び出すコードは次のことを行うことが出来ます。

prompt "Tell me something", "", (answer) ->
parenthesized = between answer , "(", ")"
if parenthesized?
show "You parenthesized '#{parenthesized}'."

　 ○●○

In many cases returning a special value is a perfectly fine way to indicate an error. It does, however, have its downsides. Firstly, what if the function can already return every possible kind of value? For example, consider this function that gets the last element from an array:

エラーを示す為に特別の値を返すことは、多くの場合、非常におススメです。しかしながらそれはマイナス面を持っています。最初に、関数が可能な限り全ての値を戻すことが出来たらどうでしょうか？例えば、配列の最後の要素を取り出すこの関数を考えてみましょう。

lastElement = (array) ->
if array.length > 0
array[array.length - 1]
else
undefined
show lastElement [1, 2, undefined]

So did the array have a last element? Looking at the value lastElement returns, it is impossible to say.
The second issue with returning special values is that it can sometimes lead to a whole lot of clutter. If a piece of code calls between ten times, it has to check ten times whether undefined was returned. Also, if a function calls between but does not have a strategy to recover from a failure, it will have to check the return value of between, and if it is undefined, this function can then return undefined or some other special value to its caller, who in turn also checks for this value.
Sometimes, when something strange occurs, it would be practical to just stop doing what we are doing and immediately jump back to a place that knows how to handle the problem.
Well, we are in luck, a lot of programming languages provide such a thing. Usually, it is called exception handling.

arrayは最後の要素を持っているでしょうか？lastElement の戻り値を見ると、言うまでもありません。
特別な値を返す2つめの問題は、それが非常に多くの混乱に結びつく場合があるということです。コードが10回 between を呼び出す場合、それはundefined が返されたかどうか10回チェックする必要があります。また、between 関数が失敗から回復する手段を持たない場合、bettweenの戻り値をチェックしなければなりません、そしてそれがundefinedの場合、この関数は、 undefined または特別な値を返すことが出来ますが、呼び出し元は更にその値をチェックすることになります。
時々、奇妙なことが起こりますがその際は、今行っている処理を中断して、その問題の解決法を知っている場所へ直ちに戻ることが現実的でしょう。さて、幸運なことに、多くのプログラミング言語では、そのようなものを提供しています。たいてい、それらは例外処理と呼ばれます。

　 ○●○

The theory behind exception handling goes like this: It is possible for code to raise (or throw) an exception, which is a value. Raising an exception somewhat resembles a super-charged return from a function — it does not just jump out of the current function, but also out of its callers, all the way up to the top-level call that started the current execution. This is called unwinding the stack. You may remember the stack of function calls that was mentioned in Functions. An exception zooms down this stack, throwing away all the call contexts it encounters.

If they always zoomed right down to the base of the stack, exceptions would not be of much use, they would just provide a novel way to blow up your program. Fortunately, it is possible to set obstacles for exceptions along the stack. These ‘catch’ the exception as it is zooming down, and can do something with it, after which the program continues running at the point where the exception was caught. An example:

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
                  ‘   of  an  empty  array  .’

lastElementPlusTen  =  (array)  -  >
   lastElement(array)  +  10


try
  show lastElementPlusten  []
catch  error
   show  ‘Something went wrong:  ‘  +  error

- 98 -