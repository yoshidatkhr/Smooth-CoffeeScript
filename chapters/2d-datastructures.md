##<a name = "データ構造">データ構造</a>: オブジェクトと配列

この章はいくつかの単純な問いを解くのにあてられます。その過程において、2つの新しい値の型、すなわち配列(array)とオブジェクト(object)について論じ、それに関連するいくつかのテクニックを見ていきます。

次の状況を考えてみましょう: クレイジーエイミーおばさんが——彼女には一緒に暮らしている猫が50匹以上いると噂されている(あなたはうまく数えられた試しがありません)のですが——、あなたに彼女の偉業の最新情報を報せるために定期的にe-mailを送って来ます。内容はいつもこんな感じです: 

親愛なる私の甥へ

あなたのお母さんからスカイダイビングを始めたって聞いたけど、本当なの? 

ちょっとあなた、よく考えて! わたしの夫に何が起こったか覚えてないの? 

それにあれだってたったの2Fだったのよ!

それはともかく、ここは全てが素晴らしく面白いわよ。わたしは週の全てを費やしてお隣に越してきた素敵な紳士ドレイクさんの気を引こうと試してみたけど、あの人は猫を怖がっているんじゃないかしら？それとも、猫アレルギー? 次に会ったら、太っちょイゴールをあの人の肩の上に置いてみるつもりよ。何が起きるかとても楽しみだわ。

あと、あなたに教えた例の儲け話は思いの外うまくいってるわ。もう既に5件の「支払金」が返って来ていて、申し立ては1件だけ。ちょっと悪い気がして来てはいるのだけれど。まあ、違法なんじゃないのって意見は、あなたが正しいわね。

(...中略...)

それでは

叔母エミリーより

died 27/04/2006: Black Leclère

born 05/04/2006 (mother Lady Penelope): Red Lion, Doctor Hobbles the 3rd, Little Iroquois

おばさんに調子を合わせるには、彼女の猫の血統を把握しておきたいところ。そうしたら、あなたはこんな感じに続けてもいいでしょう——「追伸、この土曜にドクターホブルズ2世が彼の誕生日を楽しんだならよいのですが。」または「大きくなったレディー・ペネロペはいかがお過ごしですか? 彼女は今5歳でしたよね?」というように——うっかり死んだ猫について尋ねないように気を付けて。あなたには叔母からの古いe-mailが大量にあります。そして幸いなことに、彼女は常に一貫して、猫の出生と死亡についての情報を、メールの終わりに正確に同じ形式で付記しています。

あなたは手動でそれらのメール全てを、進んで調べる気にはなれませんよね。幸いにも、我々はちょうど何かしらの例題を必要としていたので、我々のために動くプログラムを作ってみます。まず始めに、最後のe-mailでもまだ生きている猫のリストを与えるプログラムを書きます。

あなたが尋ねる前、通信の開始と同時に、叔母エイミーはSpot(スポット、ぶち)というたった1匹だけ独身の猫を飼っていました。(その当時、まだ彼女はわりと普通でした。)



タイプし始める前に、動こうとしているあるプログラムの何らかの手がかりを持っていることはたいてい有益である。プラン(計画、設計?)は以下の通りです: 

“Spot”だけが入っている猫の名前の集合から始める。
“born”または“died”で始まる段落を探す。
“born”で始まる段落にある名前を我々の名前の集合に加える。
“died”で始まる段落にある名前を我々の集合から取り除く。
ここで、ある段落から名前を取り出すことは以下のようになります: 

コロン(:)を段落から見つける。
このコロンの後の部分を取り出す。
カンマ(,)を探すことによって、この部分を別々の名前に分割する。
これを受け入れるには、いくつかの不信、叔母エイミーが常にこの正確な形式(体裁?)を用いているとか、彼女は決して名前を書き忘れたりスペルを間違えたりはしないとか、を一時的に止めることを求められるかもしれませんが、しかしそれこそがあなたの叔母らしいところ(叔母たらしめているところのもの、叔母たる所以?)なのです。

まず、プロパティについて話させて下さい。ほとんどのCoffeeScriptの値はそれらの値と結びついた他の値を持っています。それらの結びつきはプロパティと呼ばれています。全ての文字列はlengthと呼ばれるプロパティを持ち、そのlengthはその文字列に含まれる文字の総数である数を参照します。

text = 'purple haze'

show text['length']

show text.length

2番目の方法は1番目の省略表現であり、そのプロパティの名前が妥当な変数名であるときだけ働(動)きます—それ(その変数名)が何の空白も記号もその中に持たないとき、かつ、数字で始まらないときに。

nothing = null

show nothing.length

数値(Numbers)、真偽値(Booleans)、null値、undefined値はどんなプロパティも持ちません。そのような値からプロパティを読もうとするとエラーが生じます。このような(いくつかのブラウザに関しては、かなり不可解(暗号的?)かもしれない(ちょっと隠れているかもしれない?))場合にあなたの得るエラーメッセッージの種類についての知識(idea)を得るためにも、次のコードを試しなさい。

ある文字列のそのプロパティの値は変えられません。それらはlengthだけでなくかなりの種類がありますが、これから見ていくように、あなたは何か加えたり取り除いたりすることを許されてはいません。

これはオブジェクト型の値とは異なります。それらの主な役割は他の値を持っておく(保持する?)ことです。それらは、言わば、プロパティという形でそれら自身の触手の集合を持っていると言えるでしょう。あなたがそれらを変更すること、取り除くこと、新しいものを付け加えることは自由です。

あるオブジェクトはこのように記述されます: 

cat =

    colour: 'grey'

    name: 'Spot'

    size: 46

# Or: cat = {colour: 'grey', name: 'Spot', size: 46}

cat.size = 47

show cat.size

delete cat.size

show cat.size

show cat

変数のように、あるオブジェクトに付随する各プロパティはある文字列によって名付けられます。最初の記述がオブジェクトを作り出し、そのオブジェクトのプロパティ'colour'は文字列'grey'を保持し、そのオブジェクトのプロパティ'name'は文字列'Spot'に付随されており、そのオブジェクトのプロパティ'size'は数46を参照(指示?)しています。その次の記述はsizeと名付けられたプロパティに新しい値を与えています。変数を変更するのと同じような方法で行われています。

deleteという用語(キーワード?)はプロパティを削除します。値undefinedを与える存在しないプロパティを読んでみなさい。

まだ存在しないプロパティが = 演算子(オペレーター?)で定められたとすると、それ(そのプロパティ)はオブジェクトに加えられます。

empty = {}

empty.notReally = 1000

show empty.notReally

妥当な変数名ではない名前のプロパティは、オブジェクトを生成する際にコーテーションで囲う必要があり、呼び出すにも括弧を使う必要があります: 

thing = {'gabba gabba': 'hey', '5': 10}

show thing['5']

thing['5'] = 20

show thing[2 + 3]

delete thing['gabba gabba']

show thing

ご覧の通り、括弧の間の部分はどんな表現も可能です。それは、それを参照する(示す?)プロパティ名を決定するために文字列に変換されます。プロパティを名付けるために用いるのは変数でも大丈夫です: 

propertyName = 'length'

text = 'mainline'

show text[propertyName]

ofという演算子はオブジェクトがあるプロパティを持つかどうかをテストするのに利用できます。それは真偽値を生じます。

chineseBox = {}

chineseBox.content = chineseBox

show 'content' of chineseBox

show 'content' of chineseBox.content

show chineseBox

オブジェクトの値がコンソールに表示されているとき、プロパティの最初の何層かだけしか表示されません。もっと層を調べるために、あなたはshowにdepthという追加引数を与えることができます。

abyss = {let:1, us:go:deep:down:7}

show abyss

show abyss, 5

練習10

猫問題のための解決は名前の「集合」について言及します。集合とは複数回同じ値が現れないような値の集まりです。もし名前が文字列なら、名前の集合を表すためにオブジェクトを使う方法を考えられますか?

名前がこの集合にどのようにして加えられるか、どのようにして取り除かれるかを示し、また、どのようにしてある名前がその中に現出しているかどうか調べられるかを示しなさい。

解決

これはオブジェクトのプロパティとして集合の内容を格納することで成し得ます。

名前を追加は、ある値、すなわち任意の値、にその名前でプロパティを設定することによって成されます。名前の削除は、このプロパティを削除することで成されます。of 演算子はある特定の名前が集合の一部であるかどうかを判定するのに使えます。このアプローチに関していくつか微妙な問題がありますが、それはオブジェクト指向Object Orientationにおいて議論され解決されるでしょう。この章に関しては、これで十分です。

set = {'Spot': true}

# Add 'White Fang' to the set

set['White Fang'] = true

# Remove 'Spot'

delete set['Spot']

# See if 'Asoka' is in the set

show 'Asoka' of set

明らかに、オブジェクトの値は変えられます。Basic CoffeeScriptにおいて検討された値の型は全く不変であり、それらの型が存在するある値を変えることは不可能です。あなたはそれらを組み合わせることができ、それらから新しい値を追い出すことができます。しかし、あなたが特定の文字列の値を使うとき、その中の文字列は変えられません。一方で、オブジェクトについては、その値の内容はそのプロパティを変えることによって変更可能です。

2つの数120と120があるとき、それらは実際上は正に同じ数と考えられます。オブジェクトとしては、同じオブジェクトへの2つの参照を持つことと同じプロパティを内包する異なるオブジェクト2つを持つことの間には違いがあります。次のコードを考えなさい:

object1 = {value: 10}

object2 = object1

object3 = {value: 10}

 

show object1 == object2

show object1 == object3

 

object1.value = 15

show object2.value

show object3.value

object1とobject2は正に同じ値を保持する2つの変数です。実際のオブジェクトはたった1つだけですので、object1を変えることは、object2の値もまた変えるのです。変数object3はもう一つのオブジェクトを指し示しています。それは初めにobject1と同じプロパティを含んでいましたが、別々の道を歩みます。

CoffeeScriptの==演算子は、オブジェクト同士を比較すると、もしそれに与えられた両方の値が正に同じ値であれば、trueのみを返すでしょう。全く同一の内容を持つ異なる値を比較することはfalseを与えるでしょう。このことは何らかの場面で役立ちます。しかし、他のところでは(他人には?)非実用的です。

15underscore libraryにおいて、あなたはそれらの内容の全ての層に基づいて2つのオブジェクトを比較するisEqualという関数を見つけることができます。

オブジェクトの値は多くの異なる役割を果たすことができます。集合のように振る舞うことはそのうちのたった1個に過ぎません。我々はいくつかの他の役割をこの章の中でみていきます。そして、Object Orientationではもう一つの重要なオブジェクトの使い方を示します。

猫問題のためのプランにおいて—実際、これはプランではなく、アルゴリズムと呼びましょう、それは我々が何について話しているか我々は知っているように思わせるが—そのアルゴリズムにおいて、あるアーカイブの中の全てのe-mailを探索することについて話しています。このアーカイブは何のようにみえますか?そして、それはどこから来るのでしょうか?

Do not worry about the second question for now. Modularity talks about some ways to import data into your programs, but for now you will find that the e-mails are just magically there. Some magic is really easy, inside computers.

今は2番目の問いについては心配することはありません。いまあなたがまるで魔法のようにそこにe-mailが存在することを発見できなければ、Modularityではいくつかのあなたのプログラムへのデータの取り込み(インポート?)方法について話します。いくつかの魔法はコンピュータの中では本当に簡単です。

○•○

The way in which the archive is stored is still an interesting question. It contains a number of e-mails. An e-mail can be a string, that should be obvious. The whole archive could be put into one huge string, but that is hardly practical. What we want is a collection of separate strings.

そのアーカイブが格納されるその方法はまだ関心を引く問いです。それは多くのe-mailの数を含有しています。明らかに、一つのe-mailは文字列であり得ます。アーカイブ全体は一つの巨大な文字列にまとめられるが、あまり実用的ではありません。我々が求めているのは分離した文字列の集まりです。

Collections of things are what objects are used for. One could make an object like this:

mailArchive = {

   'the first e-mail': 'Dear nephew , ...'

   'the second e-mail': '...'

   # and so on ...

}

そして「ものごとの集まり」を表現するのは、まさにオブジェクトの使いどころです。例えばこのような形でオブジェクトを作ることができます。: 

mailArchive = {

   'the first e-mail': 'Dear nephew , ...'

   'the second e-mail': '...'

   # and so on ...

}

But that makes it hard to go over the e-mails from start to end — how does the program guess the name of these properties? This can be solved by more predictable property names:

mailArchive = {

   0: 'Dear nephew , ... (mail number 1)'

   1: '(mail number 2)'

   2: '(mail number 3)'

}

for current of mailArchive

   show 'Processing e-mail #' + current +

        ': ' + mailArchive[current] 

しかし、それは最初から最後まで電子メールを探索することを困難にします―どのようにしてプログラムがこれらのプロパティの名前を推量するのですか?これはもっとありきたりなプロパティ名によって解決することができます: 

mailArchive = {

   0: 'Dear nephew , ... (mail number 1)'

   1: '(mail number 2)'

   2: '(mail number 3)'

}

for current of mailArchive

   show 'Processing e-mail #' + current +

        ': ' + mailArchive[current]

Luck has it that there is a special kind of objects specifically for this kind of use. They are called arrays, and they provide some conveniences, such as a length property that contains the amount of values in the array, and a number of operations useful for this kind of collections.

幸運なのは(?)特にこの種の使用のための特別な種類のオブジェクトがあるということです。それらは配列と呼ばれ、配列に値の量を含んでいる"length"プロパティのようないくつかの利便なものと、この種の集まりとって便利ないくつかの演算子を備えています

(提供します、もたらします?)。

New arrays can be created using brackets ([ and ]). As with properties, the commas between elements are optional when they are placed on separate lines. Ranges and for comprehensions also create arrays.

mailArchive = ['mail one', 'mail two', 'mail three']

for current in [0...mailArchive.length]

show 'Processing e-mail #' + current +

': ' + mailArchive[current]

新しい配列は括弧("["と"]")を使って作り出すことができます。プロパティと同様、別々の行(ライン?)に置かれる場合は要素間のカンマは任意(省略可能)です。範囲も、また内包に関してもまた配列を作り出します。

mailArchive = ['mail one', 'mail two', 'mail three']

for current in [0...mailArchive.length]

show 'Processing e-mail #' + current +

': ' + mailArchive[current]

In this example, the numbers of the elements are not specified explicitly anymore. The first one automatically gets the number 0, the second the number 1, and so on.

この例において、その要素の数はもうこれ以上明確に特定されていません。最初のものは自動的に数0を得、第2番目のものは数1を得、...。

Why start at 0? People tend to start counting from 1. As unintuitive as it seems, numbering the elements in a collection from 0 is often more practical. Just go with it for now, it will grow on you.

何故0から始めるのでしょうか?人は1から数え始める傾向があります。見かけ通り非直観的として、0からの集まりの要素に番号付けすることはしばしば(多くの場合、たいてい)より実用的です。今はとにかくこのままいってみましょう、そのうち身に付くようになります。

Starting at element 0 also means that in a collection with X elements, the last element can be found at position X - 1. This is why the for loop in the example uses an exclusive range 0...mailArchive.length. There is no element at position mailArchive.length, so as soon as current has that value, we stop looping.

要素0から始めることは、要素Xで集めたものの中のものもまた意味しており、最後(最新?)の要素は場所 X - 1で見つけることができます。こういう訳で、例におけるforループは排他的な範囲 0...mailArchive.lengthを使うのです。場所mailArchive.lengthに要素はありません。したがって、"current"がその値を持つとすぐに、我々はループを止めます。

Exercise 11

Write a function range that takes one argument, a positive number, and returns an array containing all numbers from 0 up to and including the given number.

An empty array can be created by simply typing []. Also remember that adding properties to an object, and thus also to an array, can be done by assigning them a value with the = operator. The length property is automatically updated when elements are added. 

練習11

1つの引数、正の数、をとり、0から上の全ての数を含んでいて、与えられた数を含有する配列を返す関数rangeを書きなさい。空の配列は単に[]をタイプすることで作り出すことができます。また、あるオブジェクトにプロパティを追加することを思い出せば、ある配列にもまた、=演算子でそれらにある値を割り当てることによって可能になります(可能となることを思い出しなさい?)。要素が追加される場合、そのlengthプロパティは自動的に更新されます。

Solution

range = (upto) ->

  result = []

  i = 0

  while i <= upto

    result[i] = i

    i++

  result

show range 4

Instead of naming the loop variable counter or current, as I have been doing so far, it is now called simply i. Using single letters, usually i, j, or k for loop variables is a widely spread habit among programmers. It has its origin mostly in laziness: We’d rather type one character than seven, and names like counter and current do not really clarify the meaning of the variable much. 

If a program uses too many meaningless single-letter variables, it can become unbelievably confusing. In my own programs, I try to only do this in a few common cases. Small loops are one of these cases. If the loop contains another loop, and that one also uses a variable named i, the inner loop will modify the variable that the outer loop is using, and everything will break. One could use j for the inner loop, but in general, when the body of a loop is big, you should come up with a variable name that has some clear meaning. 

In CoffeeScript the solution can be written in much shorter forms using a for expression that collects the results or by using the built-in range.

range = (upto) -> i for i in [0..upto]

show range 4

range = (upto) -> [0..upto]

show range 4

解決

range = (upto) ->

  result = []

  i = 0

  while i <= upto

    result[i] = i

    i++

  result

show range 4

そのループ変数をcounterまたはcurrentと名づける代わりに、私がこれまでやってきたように、今それは単にiと呼ばれます。ループ変数に通常i、jあるいはkという単一の文字を使用することは、プログラマの間では広く普及している習慣です。それは主に怠惰から来ています: 我々は7文字より1文字をむしろタイプしたい。それに、counterとかcurrentのような名前は本当のところ、そんなに変数の意味を明確にはしていません。

もしプログラムがあまりにも多くの無意味な単一文字の変数を使うなら、それは信じられないほど混乱させるようになるでしょう。私自身のプログラムにおいては、私は少しの共通の場合にだけこれをすることにしようと試みて(努力して)います。小さなループはこれらの場合のうちの1つです。ループが別のループを含んでおり、それもまたiという名の変数を使用しているとすると、内部のループは外部のループが使用している変数を修正するでしょう。すると、すべてが壊れます(ブレイクします?)。誰もが内部のループのためにjを使用してもかまわないが、一般に、ループの本体が大きいとき、あなたは何か明瞭な意味を持つ変数名を考え出すべきです。

CoffeeScriptにおいては、解決は、結果を集めるfor表現を使用して、あるいはその内蔵の範囲を使うことによって、はるかに短い形式で書くことができます。

range = (upto) -> i for i in [0..upto]

show range 4

range = (upto) -> [0..upto]

show range 4 



In CoffeeScript most statements can also be used as expressions. That means for example that the values from a for comprehension can be collected in a variable and used later.
CoffeeScriptでは、ほとんどの命令文は式としても使えます。例えばfor節の値を変数に集めて後で使うことができる、といったことをこれは意味します。

numbers = (number for number in [0..12] by 2)
show numbers

○•○
Both string and array objects contain, in addition to the length property, a number of properties that refer to function values.
文字列も配列オブジェクトも、lengthプロパティに加えて、関数値を参照するいくつかのプロパティを含んでいます。

doh = ’Doh’
show typeof doh.toUpperCase
show doh.toUpperCase()
Every string has a toUpperCase ↓ property. When called, it will return a copy of the string, in which all letters have been converted to uppercase. There is also toLowerCase ↓. Guess what that does.
すべての文字列はtoUpperCaseプロパティを持ちます。呼ばれると、すべての文字を大文字にへ置き換えた文字列のコピーを返します。toLowerCaseもあります。何をするものか考えてみましょう。
Notice that, even though the call to toUpperCase does not pass any arguments, the function does somehow have access to the string ’Doh’ , the value of which it is a property. How this works precisely is described in Object Orientation↓.
Properties that contain functions are generally called methods↓, for example ‘toUpperCase is a method of a string object’.
toUpperCaseの呼び出しが引数を渡さないにもかかわらず、関数がどうやってかプロパティの持つ値である’Doh’文字列にアクセスしている点に、注意してください。これがどのようにして正しく動作するかは「オブジェクト指向」の章で述べられます。関数プロパティは一般的にメソッドと呼ばれ、たとえば「toUpperCaseは文字列オブジェクトのメソッド」です。

mack = []
mack.push ’Mack’
mack.push ’the’
mack.push ’Knife’
show mack.join ’ ’
show mack.pop()
show mack
The method push ↓, which is associated with arrays, can be used to add values to it. It could have been used in the last exercise, as an alternative to result[i] = i . Then there is pop ↓, the opposite of push : it takes off and returns the last value in the array. 
join ↓ builds a single big string from an array of strings. The parameter it is given is pasted between the values in the array.
配列用のpushメソッドは値を追加するのに使えます。最後に出てきた練習問題で、result[i] = iの代わりの手段としても使うことが出来たでしょう。そして、pushの逆のpopというメソッドもあります。これは、配列の最後の値を取り去って、その値を返します。joinはひとつの大きな文字列を(文字列の)配列から作成します。与えられたパラメータは配列内の値と値の間に挿入されます。
○•○
Coming back to those cats, we now know that an array would be a good way to store the archive of e-mails. In this book, the retrieveMails after the require can be used to (magically) get hold of this array. The magic will be dispelled in Modularity↓. Going over them to process them one after another is no rocket science anymore either:
猫の話に戻って、配列がEメールのアーカイブ情報を保存するのに、良い方法だということがわかります。この本では、requireの後のretrieveMailsメソッドは(魔法のように)この配列を取得できるものとします。この魔法は「モジュラリティ」と唱えられることもあります。Eメールをひとつずつ処理するのは難しいことではありません:

mailArchive = (require "./04-emails").retrieveMails() 
​
for email, i in mailArchive
  show "Processing e-mail ##{i} #{email[0..15]}..."
  # Do more things...
In a for ... in statement we can get both the value and its index in the array. The 
email[0..15] gets the first snippet of each email. We have also decided on a way to represent the set of cats that are alive. The next problem, then, is to find the paragraphs in an e-mail that start with ’born’ or ’died’ .
for...in文の中で、配列の値とそのインデックスを取ることができます。email[0..15]は、それぞれのメールの最初の断片を取り出します。私たちは、生きている猫の集合の表現方法を決めたところでした。次の問題は「born」か「died」ではじまるメールの段落を見つけ出すことです。
○•○
The first question that comes up is what exactly a paragraph is. In this case, the string value itself can not help us much: CoffeeScript’s concept of text does not go any deeper than the ‘sequence of characters’ idea, so we must define paragraphs in those terms.
Earlier, we saw that there is such a thing as a newline character. These are what most people use to split paragraphs. We consider a paragraph, then, to be a part of an e-mail that starts at a newline character or at the start of the content, and ends at the next newline character or at the end of the content.
そうなると最初の疑問は、段落とは何なのか。この場合、文字列の値そのものはあまり助けになりません。CoffeeScriptにおけるテキスト には、「文字の連なり」以上の深い意味(コンセプト)はありません。段落ラグラフとは何かを、そういった用語で定義する必要があるのです。改行文字のようなものがある、ということをこれまでのところで見て来ました。これは、ほとんどの人が段落を分けるのに使うものです。そのでは私たちは、段落をEメールの一部で、かつ、改行文字から始まる、あるいは内容の先頭から始まり、かつ、次の改行文字か内容の最後まで、と考えることにしましょう。
And we do not even have to write the algorithm for splitting a string into paragraphs ourselves. Strings already have a method named split↓, which is (almost) the opposite of the join method of arrays. It splits a string into an array, using the string given as its argument to determine in which places to cut.
そして、文字列を段落に分けるアルゴリズムを自分自身で各必要はありません。文字列にはもともとsplitメソッドがあり、(ほぼ)配列のjoinメソッドの逆になります。これは文字列を配列に分け、引数に渡された文字列をどこで区切るかの判定に使います。

words = ’Cities of the Interior’
show words.split ’ ’
Thus, cutting on newlines (’\n’ ), can be used to split an e-mail into paragraphs.
つまり、改行文字(「\n」)で切れば、Eメールを段落に分けることができるのです。

Exercise 12
split and join are not precisely each other’s inverse. string.split(x).join(x) always produces the original value, but array.join(x).split(x) does not. Can you give an example of an array where .join(’ ’).split(’ ’) produces a different value?
練習問題12
splitとjoinは正確には、それぞれの逆にはなっていません。string.split(x).join(x)は常に元々の値になりますが、array.join(x).split(x)はそうではありません。.join(‘ ‘).split(‘ ‘)が異なる値になる例を示せますか?
 Solution
array = [’a’, ’b’, ’c d’]
show array.join(’ ’).split(’ ’)

Paragraphs that do not start with either “born” or “died” can be ignored by the program. How do we test whether a string starts with a certain word? The method 
charAt ↓ can be used to get a specific character from a string. x.charAt(0) gives the first character, 1 is the second one, and so on. One way to check whether a string starts with “born” is:
「born」か「died」で始まらない段落は、プログラムで無視出来ます。どうやって、それらの文字列で始まるかをテスト出来るのでしょうか? charAtメソッドは、文字列から特定の文字を得るのに使うことができます。x.charAt(0)は最初の文字、1は2つめの文字...、というふうに。文字列が「born」で始まるかチェックするための一つの方法です。
paragraph = ’born 15-11-2003 (mother Spot): White Fang’
show paragraph.charAt(0) == ’b’ &&
     paragraph.charAt(1) == ’o’ &&
     paragraph.charAt(2) == ’r’ &&
     paragraph.charAt(3) == ’n’
But that gets a bit clumsy — imagine checking for a word of ten characters. There is something to be learned here though: when a line gets ridiculously long, it can be spread over multiple lines. The result can be made easier to read by lining up the start of the new line with the first element on the original line that plays a similar role. You can also end a line with \ to indicate that it continues on the next line.
ですが、ちょっと面倒です — 10文字の単語でチェックすることを想像して下さい。ここで、ひとつ覚えておくことがあります。もし一行があまりに長いと、複数行にまたがってしまいます。その場合は、元の行の同じような役割をする要素と次の行の始まりを揃えると、(プログラムが)読みやすくなります。また、行末に\を置くことでも、次の行に続くことを示せます。
Strings also have a method called slice . It copies out a piece of the string, starting from the character at the position given by the first argument, and ending before (not including) the character at the position given by the second one. It is the same as using a range as an index. This allows the check to be written in a shorter way.
文字列には、sliceというメソッドもあります。こちらは、最初の引数で与えられた位置から、二つ目の引数で与えられた位置の前まで、文字列の一部のコピーを返します。インデックスとして範囲を使う場合と同じです。これだと、さっきの文字列チェックが、もっと短い書き方で出来るようになります。
show paragraph.slice(0, 4) == ’born’
show paragraph[0...4] == ’born’

Exercise 13
Write a function called startsWith that takes two arguments, both strings. It returns true when the first argument starts with the characters in the second argument, and false otherwise.
練習問題13
二つの文字列を引数に取る、startsWithと呼ばれる関数を書きましょう。この関数は、第一引数が第二引数の文字列で始まる場合に、trueを返し、そうでなければfalseを返します。
 Solution
startsWith = (string, pattern) ->
  string.slice(0, pattern.length) == pattern
# or
startsWith = (string, pattern) ->
  string[0...pattern.length] == pattern
show startsWith ’rotation’, ’rot’


What happens when charAt , slice or a range are used to take a piece of a string that does not exist? Will the startsWith still work when the pattern is longer than the string it is matched against?
charAt、sliceあるいは範囲指定で、存在しない文字列を指定してしまったら何が起きるのでしょう? パターンがマッチさせる文字列より長い場合も、startsWithは動くのでしょうか?
show ’Pip’.charAt 250
show ’Nop’.slice 1, 10
show ’Pin’[1...10]
charAt will return ’’ when there is no character at the given position, and slice or the range will simply leave out the part of the new string that does not exist.
与えられた位置に文字が無い場合、charAtは「」を返します。sliceや範囲指定の場合は単純に存在する部分だけで、新しい文字列を返します。
So yes, startsWith should work. When startsWith(’Idiots’, ’Most honoured colleagues’) is called, the call to slice will, because string does not have enough characters, always return a string that is shorter than pattern . Because of that, the comparison with == will return false , which is correct.
そう、startsWithはちゃんと動くはずです。もし、startsWith(’Idiots’, ’Most honoured colleagues’)のように呼出されれば、文字列は十分な文字数がないので、sliceが呼ばれたとしても、常に(検索)パターンより短い文字列を返すでしょう。そのため、==による比較では正しい答え—falseが返されることになります。
It helps to always take a moment to consider abnormal (but valid) inputs for a program. These are usually called corner cases↓, and it is very common for programs that work perfectly on all the ‘normal’ inputs to screw up on corner cases  [P]  .
プログラムに、普通じゃない(けど、正しい)入力がある場合を、ちょっと考えてみるというのは常に有益です。それらは、よく「コーナーケース(=めったに発生しない厄介なケース)」と呼ばれ、普通の入力に対して完璧に動くプログラムが、コーナーケースで失敗するというのは極めてよくあることです。
○•○
The only part of the cat-problem that is still unsolved is the extraction of names from a paragraph. The algorithm was this:
Find the colon in the paragraph.
Take the part after this colon.
Split this part into separate names by looking for commas.

猫問題に残った未解決部分は、(猫の)名前を段落から抽出する不分です。アルゴリズムはこうです。
段落の中のコロンを見つける
コロンの後の部分を取得
カンマを探して、この部分を複数の名前に分ける

This has to happen both for paragraphs that start with ’died’ , and paragraphs that start with ’born’ . It would be a good idea to put it into a function, so that the two pieces of code that handle these different kinds of paragraphs can both use it.
これは「died」ではじまる段落、「born」で始まる段落の両方でする必要があります。異なる段落を扱う二つのコードのそれぞれから使えるように、一つの関数にまとめるのが良さそうです。

Exercise 14
Can you write a function catNames that takes a paragraph as an argument and returns an array of names?
段落を引数にとって、猫の名前を返す関数catNamesを書けますか?
Strings have an indexOf ↓ method that can be used to find the (first) position of a character or sub-string within that string. Also, when slice is given only one argument, it will return the part of the string from the given position all the way to the end. With a range either the start or end can be left out: ’shorthand’[...5]  ⇒  ’short’ and ’shorthand’[5...]  ⇒  ’hand’ .
文字列はindexOfメソッド持っています。これは文字あるいはその文字列の部分文字列(sub-string)の現れる(最初の)位置を見つけるのに使うことができます。また、sliceに引数がひとつだけ与えられた場合、与えられた位置から最後までの部分を返します。範囲指定では、始めか終わりを書かないでおくことができます。’shorthand’[...5]  なら  ’short’ に。そして、 ’shorthand’[5...]  なら  ’hand’となります。
It can be helpful to use CoffeeScript interactively to ‘explore’ functions. Try ’foo: bar’.indexOf(’:’) and see what you get.
CoffeeScriptをインタラクティブに使って関数を「探検」すると良いですよ。’foo: bar’.indexOf(’:’)を試して、何が得られるか見てみましょう。
Solution
catNames = (paragraph) ->
  colon = paragraph.indexOf ’:’
  paragraph[colon+2...].split ’, ’
​
show catNames ’born 20/09/2004 (mother Yellow Bess): ’ +
              ’Doctor Hobbles the 2nd, Noog’
The tricky part, which the original description of the algorithm ignored, is dealing with spaces after the colon and the commas. The + 2 used when slicing the string is needed to leave out the colon itself and the space after it. The argument to split contains both a comma and a space, because that is what the names are really separated by, rather than just a comma.
This function does not do any checking for problems. We assume, in this case, that the input is always correct.



All that remains now is putting the pieces together. One way to do that looks like this:
今残っているのは、ここまでのピースをまとめあげることだけです。ひとつのやり方としては、こんな感じになるでしょう:

mailArchive = (require ’./04-emails’).retrieveMails()
livingCats = ’Spot’: true
​
for email, i in mailArchive
  paragraphs = email.split ’\n’
  for paragraph in paragraphs
    if startsWith paragraph, ’born’
      names = catNames paragraph
      for name in names
        livingCats[name] = true
    else if startsWith paragraph, ’died’
      names = catNames paragraph
      for name in names
        delete livingCats[name]
​
show livingCats
That is quite a big dense chunk of code. We will look into making it a bit lighter in a moment. But first let us look at our results. We know how to check whether a specific cat survives:
だいぶぎゅむっとした感じのコードですね。この後、これをもう少し軽くする方法を見ていきます。が、ひとまずはその結果を見てみましょう。ある猫が生きているかどうかを確認するやり方は分かっています:
if ’Spot’ in livingCats
  show ’Spot lives!’
else
  show ’Good old Spot, may she rest in peace.’
But how do we list all the cats that are alive? The of ↓ keyword is somewhat similar to the in keyword when it is used together with for :
しかし、どうやったら生きている全ての猫を一覧に出来るのでしょうか? 「of」キーワードは「for」と一緒に使うときは、「in」キーワードにいくらか似ています:

for cat of livingCats
  show cat
A loop like that will go over the names of the properties in an object, which allows us to enumerate all the names in our set.
このような繰返しはオブジェクトのプロパティの名前を調べて行って、集合にある全ての名前を列挙することができます。
○•○
Some pieces of code look like an impenetrable jungle. The example solution to the cat problem suffers from this. One way to make some light shine through it is to just add some strategic blank lines. This makes it look better, but does not really solve the problem.
コードが、足の踏み込めないジャングルのように見えることもあります。猫の問題の解決例は、そうなってしまっています。一定のルールで空行を追加するだけで、その状況から少し見通しを良くすることができます。これは、若干よくなったように見えますが、本当に問題を解決した訳ではありません。
What is needed here is to break the code up. We already wrote two helper functions, startsWith and catNames , which both take care of a small, understandable part of the problem. Let us continue doing this.
ここで必要なのは、コードをバラバラにすることです。すでに、二つのヘルパー関数startsWithとcatNamesを書きましたが、どちらも小さな理解可能な部分を扱うものでした。このやり方を続けてみましょう。

addToSet = (set, values) ->
  for i in [0..values.length]
    set[values[i]] = true
​
removeFromSet = (set, values) ->
  for i in [0..values.length]
    delete set[values[i]]
These two functions take care of the adding and removing of names from the set. That already cuts out the two most inner loops from the solution:
これらの二つの関数は、集合からの名前の追加と削除を扱います。これで、すでに二つの内部ループのほとんどを、解法から取り去ります。

livingCats = ’Spot’: true
​
for email in mailArchive
  paragraphs = email.split ’\n’
  for paragraph in paragraphs
    if startsWith paragraph, ’born’
      addToSet livingCats, catNames paragraph
    else if startsWith paragraph, ’died’
      removeFromSet livingCats, catNames paragraph
​
show livingCats
Quite an improvement, if I may say so myself.
かなりの改善です、我ながら。
Why do addToSet and removeFromSet take the set as an argument? They could use the variable livingCats directly, if they wanted to. The reason is that this way they are not completely tied to our current problem. If addToSet directly changed livingCats , it would have to be called addCatsToCatSet , or something similar. The way it is now, it is a more generally useful tool.
addToSetとremoveFromSetはなぜ、集合を引数にとるのでしょうか? これらの関数は、必要があればlivingCats変数を直接使えるはずです。その理由は、今の問題に完全に特化したものにしていないからです。もし、addToSetが直接livingCatsを変更してしまったら、それはadCatsToCatSetとでも呼ぶべきものです。ここでは、もう少し汎用的で便利なツールにしています。
Even if we are never going to use these functions for anything else, which is quite probable, it is useful to write them like this. Because they are ‘self sufficient’, they can be read and understood on their own, without needing to know about some external variable called livingCats .
もし、他の用途にこの関数をまったく使わないつもりなら、あまり意味はありませんが、こんな風に書いておくとこと便利です。外部の変数であるlivingCatsのことを知らなくても、これらは「自己完結」しているため、読みやすく分かり易いのです。
The functions are not pure: They change the object passed as their set argument. This makes them slightly trickier than real pure functions, but still a lot less confusing than functions that run amok and change any value or variable they please.
この関数はset引数として渡したオブジェクトを変更してしまうため、純関数ではありません。このことが、ちゃんとした純関数と比べると若干トリッキーなものにしてしまってはいますが、自制心を失って所構わず変数や値を変更してしまうような関数などに比べたら、全然ややこしくありません。
○•○
We continue breaking the algorithm into pieces:
アルゴリズムを部分に分けて行く作業を続けましょう:

findLivingCats = ->
  mailArchive = (require ’./04-emails’).retrieveMails()
  livingCats = ’Spot’: true
​
  handleParagraph = (paragraph) ->
    if startsWith paragraph, ’born’
      addToSet livingCats, catNames paragraph
    else if startsWith paragraph, ’died’
      removeFromSet livingCats, catNames paragraph
​
  for email in mailArchive
    paragraphs = email.split ’\n’
    for paragraph in paragraphs
      handleParagraph paragraph
​
  livingCats
​
howMany = 0
for cat of findLivingCats()
  howMany++
show ’There are ’ + howMany + ’ cats.’
The whole algorithm is now encapsulated by a function. This means that it does not leave a mess after it runs: livingCats is now a local variable in the function, instead of a top-level one, so it only exists while the function runs. The code that needs this set can call findLivingCats and use the value it returns.
全てのあるゴリズが、関数によってカプセル化されました。これは、処理が終わった後に余計なものを残さないことを意味します: livingCatsはトップレベルではなく、関数内のローカル変数となったので、関数が実行される間だけ存在します。この集合を必要とするコードは、findLivingCatsを呼んで、そこで返される値を使うことができます。
It seemed to me that making handleParagraph a separate function also cleared things up. But this one is so closely tied to the cat-algorithm that it is meaningless in any other situation. On top of that, it needs access to the livingCats variable. Thus, it is a perfect candidate to be a function-inside-a-function. When it lives inside findLivingCats , it is clear that it is only relevant there, and it has access to the variables of its parent function.
handleParagraphに処理を分けて関数にすると、分かり易くなるように思います。ただ、この関数は猫アルゴリズムに非常に強く結びついているので、他のシチュエーションで使ってもあまり意味がありません。加えて、livingCsats変数にアクセスする必要がああります。そのため、関数内関数にしてしまうのが最適な候補となります。findLivingCatsの中であれば、その場所だけで有効なことが明らかで、親関数の変数にもアクセスすることができる訳です。
This solution is actually bigger than the previous one. Still, it is tidier and I hope you will agree that it is easier to read.
この解決法は、実際のところ前のものより大きいです。ですが、整然としていますし、こちらの方が読みやすいということに、あなたも賛成してくれると期待します。
○•○
The program still ignores a lot of the information that is contained in the e-mails. There are birth-dates, dates of death, and the names of mothers in there.
このプログラムは、まだEメールに含まれるいろいろな情報を無視しています。誕生日や、亡くなった日、そこにある母親たちの名前などがあります。.

To start with the dates: What would be a good way to store a date? We could make an object with three properties, year , month , and day , and store numbers in them.
日付情報から始めましょう : 日付を記録しておくのに良い方法はなんでしょうか? year、month、dayの三つのプロパティを持つオブジェクトを作って、そこに数字を保存しておくことは可能です。

whenWasIt = year: 1980, month: 2, day: 1
But CoffeeScript already provides a kind of object for this purpose. Such an object can be created by using the keyword new ↓:
ですが、CoffeeScriptはすでにこの目的で使うためのオブジェクトが用意されています。newキーワードを使うと、そんなオブジェクトを作成できます。

whenWasIt = new Date 1980, 1, 1
show whenWasIt
Just like the notation with colons and optional braces we have already seen, new is a way to create object values. Instead of specifying all the property names and values, a function is used to build up the object. This makes it possible to define a kind of standard procedure for creating objects. Functions like this are called constructors↓, and in Object Orientation↓ we will see how to write them.
既に見てきたコロンと括弧(あっても無くてもOK)の表記と同じように、newはオブジェクト値を生成するための方法です。全てのプロパティ名と値を指定する代わりに、関数がオブジェクトを作り上げてくれます。これによって、一種の標準的なオブジェクト生成の手順を決めておくことが出来るようになります。こういった関数はコンストラクタと呼ばれ、「オブジェクト指向」の章でどのように書くかを見ることになります。
The Date ↓ constructor can be used in different ways.

show new Date
show new Date 1980, 1, 1
show new Date 2007, 2, 30, 8, 20, 30
As you can see, these objects can store a time of day as well as a date. When not given any arguments, an object representing the current time and date is created. Arguments can be given to ask for a specific date and time. The order of the arguments is year, month, day, hour, minute, second, milliseconds. These last four are optional, they become 0 when not given.
見たままですが、これらのオブジェクトは、日付と同様に、一日の中の時間を保存することができます。もし、引数が何も与えられなければ、現在の時刻と日付を表現するオブジェクトが生成されます。特定の日付や時間にするように、引数を与えることも可能です。引数の順番は、年、月、日、時、分、秒、ミリ秒です。最後の4つの引数はオプションで、指定しなかった場合はそれぞれ0がセットされます。
The month numbers these objects use go from 0 to 11, which can be confusing. Especially since day numbers do start from 1.
これらのオブジェクトで使う「月」番号は、紛らわしいことに0から11です。とくに「日」番号は1から始まるので。
○•○
The content of a Date object can be inspected with a number of get... methods.
Dateオブジェクトの中身は、get...メソッドで調べることができます。

today = new Date();
show "Year: #{today.getFullYear()}
 month: #{today.getMonth()}
 day: #{today.getDate()}"
show "Hour: #{today.getHours()}

 minutes: #{today.getMinutes()}
 seconds: #{today.getSeconds()}"
show "Day of week: #{today.getDay()}"
All of these, except for getDay , also have a set... variant that can be used to change the value of the date object.
getDay以外は、日付オブジェクトの値を変更するために使うset...関数もあります。
Inside the object, a date is represented by the amount of milliseconds it is away from January 1st 1970. You can imagine this is quite a large number.
オブジェクトの中で、日付は1970年1月1日からミリ秒でどれだけ経っているかで表現されています。かなり大きな数になることは想像がつくと思います。

today = new Date()
show today.getTime()
A very useful thing to do with dates is comparing them.
日付オブジェクトで非常に便利なのは、これらの比較です。

wallFall = new Date 1989, 10, 9
gulfWarOne = new Date 1990, 6, 2
show wallFall < gulfWarOne
show wallFall == wallFall
# but
show wallFall == new Date 1989, 10, 9
Comparing dates with < , >, <= , and >= does exactly what you would expect. When a date object is compared to itself with == the result is true , which is also good. But when == ↓ is used to compare a date object to a different, equal date object, we get false . Huh?
「<」と「>」、「<=」と「>=」で日付を比較すると、想像通りのことができます。そのオブジェクト自身と「==」で比較すると、trueが返るのも良いですね。しかし、「==」が異なる日付オブジェクトで、同じ日時を表すオブジェクトの比較に使われた場合、falseか返ってきてしまいます。あれっ?
As mentioned earlier, == will return false when comparing two different objects, even if they contain the same properties. This is a bit clumsy and error-prone here, since one would expect >= and == to behave in a more or less similar way. Testing whether two dates are equal can be done like this:
「==」について前に述べたように、2つのことなるオブジェクトについて比較をすると、「==」はfalseを返します。「>=」と「==」は同じような振る舞いをすると思うでしょうから、ここではちょっと気が利かないというか、間違いのもとですね。二つの日付が同じかどうかをテストするには、次のようにします:

wallFall1 = new Date 1989, 10, 9
wallFall2 = new Date 1989, 10, 9
show wallFall1.getTime() == wallFall2.getTime()
○•○
In addition to a date and time, Date objects also contain information about a timezone↓. When it is one o’clock in Amsterdam, it can, depending on the time of year, be noon in London, and seven in the morning in New York. Such times can only be compared when you take their time zones into account. The getTimezoneOffset ↓ function of a Date can be used to find out how many minutes it differs from GMT (Greenwich Mean Time).
日付と時刻に加えて、Dateオブジェクトはタイムゾーンについての情報を含んでいます。アムステルダムで1時なら、時季によりますが、ロンドンでは正午、ニューヨークでは朝の7時のはずです。こうした時間は、タイムゾーンを考慮して初めて比較することができます。DateオブジェクトのgetTimezoneOffset関数は何分GMT(グリニッジ標準時)からずれているかを調べるのに使うことができます。

now = new Date()
show now.getTimezoneOffset()
Exercise 15
’died 27/04/2006: Black Leclère’ The date part is always in the exact same place of a paragraph. How convenient. Write a function extractDate that takes such a paragraph as its argument, extracts the date, and returns it as a date object.
日付部分は、いつも段落の全く同じ場所にあります。何て便利。このような段落を引数にとって、日付を取り出し、日付オブジェクトとして返すextractDate関数を書きなさい。
 
Solution
extractDate = (paragraph) ->
  numberAt = (start, length) ->
    Number paragraph[start...start + length]
  new Date numberAt(11, 4),     # Year
           numberAt( 8, 2) - 1, # Month
           numberAt( 5, 2)      # Day
​
show extractDate ’died 27-04-2006: Black Leclère’
It would work without the calls to Number , but as mentioned earlier, I prefer not to use strings as if they are numbers. The inner function was introduced to prevent having to repeat the Number and slice part three times.
Note the -1 for the month number. Like most people, Aunt Emily counts her months from 1, so we have to adjust the value before giving it to the Date constructor. (The day number does not have this problem, since Date objects count days in the usual human way.)
In Regular Expressions↓ we will see a more practical and robust way of extracting pieces from strings that have a fixed structure.


Storing cats will work differently from now on. Instead of just putting the value true into the set, we store an object with information about the cat. When a cat dies, we do not remove it from the set, we just add a property death to the object to store the date on which the creature died.
これから、猫情報の保存は違った方法をとります。ただ、trueを集合に入れておくのではなくて、猫に関する情報と一緒に保存します。猫がもし死んでいたら、それを削除するのではなくて、創造物が死んだ日をオブジェクトに記録するため、deathプロパティを追加します。

This means our addToSet and removeFromSet functions have become useless. Something similar is needed, but it must also store birth-dates and, later, the mother’s name.
これは、addToSetとremoveFromSet関数が用済みになることを意味します。同様のものが改めて必要になりますが、それは、産まれた日と母猫の名前も保存出来るものでなくてはなりません。
catRecord = (name, birthdate, mother) ->
  name:   name
  birth:  birthdate
  mother: mother
​
addCats = (set, names, birthdate, mother) ->
  for name in names
    set[name] = catRecord name, birthdate, mother
​
deadCats = (set, names, deathdate) ->
  for name in names
    set[name].death = deathdate
catRecord is a separate function for creating these storage objects. It might be useful in other situations, such as creating the object for Spot. ‘Record’ is a term often used for objects like this, which are used to group a limited number of values.
catRecordは
○•○
So let us try to extract the names of the mother cats from the paragraphs.

’born 15/11/2003 (mother Spot): White Fang’
One way to do this would be…

extractMother = (paragraph) ->
  start = paragraph.indexOf ’(mother ’
  start += ’(mother ’.length
  end = paragraph.indexOf ’)’
  paragraph[start...end]
​
show extractMother \
  ’born 15/11/2003 (mother Spot): White Fang’
Notice how the start position has to be adjusted for the length of the string ’(mother ’ , because indexOf returns the position of the start of the pattern, not its end.

Exercise 16
The thing that extractMother does can be expressed in a more general way. Write a function between that takes three arguments, all of which are strings. It will return the part of the first argument that occurs between the patterns given by the second and the third arguments. That is:
between ’born 15/11/2003 (mother Spot): White Fang’,
         ’(mother ’, ’)’  ⇒  ’Spot’
between ’bu ] boo [ bah ] gzz’, ’[ ’, ’ ]’  ⇒  ’bah’

To make that second test work, it can be useful to know that indexOf can be given a second, optional parameter that specifies at which point it should start searching.
 Solution
between = (string, start, end) ->
  startAt = string.indexOf start
  startAt += start.length
  endAt = string.indexOf end, startAt
  string[startAt...endAt]
show between ’bu ] boo [ bah ] gzz’, ’[ ’, ’ ]’



Having between makes it possible to express extractMother in a simpler way:
extractMother = (paragraph) ->  between paragraph, ’(mother ’, ’)’

○•○
The new, improved cat-algorithm looks like this:

findCats = ->
  mailArchive = (require ’./04-emails’).retrieveMails()
  cats = {’Spot’: catRecord ’Spot’,
    new Date(1997, 2, 5), ’unknown’}
​
  handleParagraph = (paragraph) ->
    if startsWith paragraph, ’born’
      addCats cats, catNames(paragraph),
              extractDate(paragraph),
              extractMother(paragraph)
    else if startsWith paragraph, ’died’
      deadCats cats, catNames(paragraph),
               extractDate(paragraph)
​
  for email in mailArchive
    paragraphs = email.split ’\n’
    for paragraph in paragraphs
      handleParagraph paragraph
  cats
​
catData = findCats()
show catData
Having that extra data allows us to finally have a clue about the cats aunt Emily talks about. A function like this could be useful:

formatDate = (date) -> "#{date.getDate()}/" +
                       "#{date.getMonth() + 1}/" +
                       "#{date.getFullYear()}"
catInfo = (data, name) ->
  unless name of data
    return "No cat by the name of #{name} is known."
  cat = data[name]
  message = "#{name}," +
            " born #{formatDate cat.birth}" +
            " from mother #{cat.mother}"
  if "death" of cat
    message += ", died #{formatDate cat.death}"
  "#{message}."
​
show catInfo catData, "Fat Igor"
The return statement in catInfo is used as an escape hatch. If there is no data about the given cat, the rest of the function is meaningless, so we immediately return a value, which prevents the rest of the code from running.

In the past, certain groups of programmers considered functions that contain multiple return statements sinful. The idea was that this made it hard to see which code was executed and which code was not. Other techniques, which will be discussed in Error Handling↓, have made the reasons behind this idea more or less obsolete, but you might still occasionally come across someone who will criticise the use of ‘shortcut’ return statements.

Exercise 17
The formatDate function used by catInfo does not add a zero before the month and the day part when these are only one digit long. Write a new version that does this.
Solution
formatDate = (date) ->
  pad = (number) ->
    if number < 10
      "0" + number
    else
      number
  "#{pad date.getDate()}/" +
  "#{pad date.getMonth() + 1}/" +
  "#{date.getFullYear()}"
​
show formatDate new Date 2000, 0, 1



↓↓The property ‘dot’ accessor that we have been using comes in a handy form combined with the existential operator. Instead of object.element we can write object?.element if object is defined then we get the value as before. But if it is null then we get undefined instead of an error.

Exercise 18
Write a function oldestCat which, given an object containing cats as its argument, returns the name of the oldest living cat.

 Solution
oldestCat = (data) ->
  oldest = null
  for name of data
    cat = data[name]
    unless ’death’ of cat
      if oldest is null or oldest.birth > cat.birth
        oldest = cat
  oldest?.name
show oldestCat catData
The conditions in the unless/if statements might seem a little intimidating. It can be read as ‘only store the current cat in the variable oldest if it is not dead, and oldest is either null or a cat that was born after the current cat’.

for cat, info of catData # Test with dead cats
  delete catData[cat] unless ’death’ of info
show oldestCat catData
Note that this function returns undefined when there are no living cats in data . What does your solution do in that case?



Now that we are familiar with arrays, I can show you something related. Whenever a function is called, a special variable named arguments ↓ is added to the environment in which the function body runs. This variable refers to an object that resembles an array. It has a property 0 for the first argument, 1 for the second, and so on for every argument the function was given. It also has a length ↓ property.
This object is not a real array though, it does not have methods like push , and it does not automatically update its length property when you add something to it. Why not, I never really found out, but this is something one needs to be aware of.

argumentCounter = ->
  show "You gave me #{arguments.length} arguments."
​
argumentCounter "Death", "Famine", "Pestilence"
 
Some functions can take any number of arguments. These typically loop over the values in the arguments object to do something with them. We can create a print function that uses show to print each of its arguments.

print = -> show arg for arg in arguments
​
print ’From here to’, 1/0
Others can take optional arguments which, when not given by the caller, get some sensible default value.

add = (number, howmuch) ->
  if  arguments.length < 2
    howmuch = 1
  number + howmuch
​
show add 6
show add 6, 4
Exercise 19
Extend the range function from the exercise on page 1↑ to take a second, optional argument. If only one argument is given, it behaves as earlier and produces a range from 0 to the given number. If two arguments are given, the first indicates the start of the range, the second the end.
Solution
range = (start, end) ->
  if arguments.length < 2
    end = start
    start = 0
  result = []
  for i in [start..end]
    result.push i
  result
​
show range 4
show range 2, 4
 
The optional argument does not work precisely like the one in the add example above. When it is not given, the first argument takes the role of end , and start becomes 0 .



CoffeeScript has a few of features that can make it simpler to work with arguments. You can set default values directly in the argument list. The showfunction is defined like:

show = (obj, depth = 2, showHidden = false,
             colors = useColors) ->
  # body
When the arguments starting from depth are not present in a call, they get the value after the = . No checks are needed in the body where the arguments are used.
For variable arguments you can use ... commonly called splats. The ellipsis can indicate extra arguments in a function definition or a call. Do you remember the testPure function? It was used with both absolute which takes one argument and power which takes two. In its definition (c, a...) says that a... is a variable argument list. The variable arguments are used two times, in the call to func and in the call to property .

prelude.qc.testPure = (func, types, name, property) ->
  prelude.qc.declare name, types, (c, a...) ->
    c.assert property c, a..., c.note func a...
Finally the or= operator can be used in options or= defaults as shorthand for options || (options = defaults) .

Exercise 20
You may remember this line of code from the introduction:
show sum [1..10] All we need to make this line work is a sum function. This function takes an array of numbers, and returns their sum. Write it, it should be easy. Check that it also works with range .
 
Solution
sum = (numbers) ->
  total = 0
  for num in numbers
    total += num
  total
​
show sum [1..10]
show sum range 1, 10


The previous chapter showed the functions Math.max and Math.min . With what you know now, you will notice that these are really the properties max and min of the object stored under the name Math ↓. This is another role that objects can play: A warehouse holding a number of related values.
There are quite a lot of values inside Math , if they would all have been placed directly into the global environment they would, as it is called, pollute it. The more names have been taken, the more likely one is to accidentally overwrite the value of some variable. For example, it is not a far shot to want to name something max .
Most languages will stop you, or at least warn you, when you are defining a variable with a name that is already taken. Not JavaScript.
In any case, one can find a whole outfit of mathematical functions and constants inside Math . All the trigonometric functions are there — cos , sin , tan , acos , asin , atan . π and e, which are written with all capital letters (PI and E ), which was, at one time, a fashionable way to indicate something is a constant. pow is a good replacement for the power functions we have been writing, it also accepts negative and fractional exponents. sqrt takes square roots. max and min can give the maximum or minimum of two values. round ↓, floor ↓, and ceil ↓ will round numbers to the closest whole number, the whole number below it, and the whole number above it respectively.
There are a number of other values in Math , but this text is an introduction, not a reference↓. References are what you look at when you suspect something exists in the language, but need to find out what it is called or how it worked exactly. A useful reference for predefined global objects like the Math object exist at the Mozilla Developer Network.
 
An interesting object is Array when you look through its reference notice that many definitions for example forEach are marked
Requires JavaScript 1.6
or another version number. JavaScript 1.5 corresponds to ECMA-262 3rd Edition from December 1999.
More than a decade later this is still the standard that most JavaScript engines implement — including V8, the engine that via JavaScript compiles CoffeeScript to native machine code. It is fair to say that JavaScript is evolving at a glacial pace. Fortunately CoffeeScript and Underscore leapfrogs the JavaScript process and gives you language and library advances that you can use without waiting for existing browsers and engines to be upgraded.
○•○
Maybe you already thought of a way to find out what is available in the Math object:

for name of Math
  show name
But alas, nothing appears. Similarly, when you do this:

for name of [’Huey’, ’Dewey’, ’Loui’]
  show name
You only see 0 , 1 , and 2 , not length , or push , or join , which are definitely also in there. Apparently, some properties of objects are hidden↓. There is a good reason for this: All objects have a few methods, for example toString ↓, which converts the object into some kind of relevant string, and you do not want to see those when you are, for example, looking for the cats that you stored in the object.
Why the properties of Math are hidden is unclear to me. Someone probably wanted it to be a mysterious kind of object. But you can peek under the hood with show — see the prelude for details:

show Math, 2, true
show [’Huey’, ’Dewey’, ’Loui’], 2, true
All properties your programs add to objects are visible. There is no way to make them hidden, which is unfortunate because, as we will see in Object Orientation↓, it would be nice to be able to add methods to objects without having them show up in our for / of loops.
○•○
↓Some properties are read-only, you can get their value but not change it. For example, the properties of a string value are all read-only.
↓Other properties can be ‘watched’. Changing them causes things to happen. For example, lowering the length of an array causes excess elements to be discarded:

array = [’Heaven’, ’Earth’, ’Man’]
array.length = 2
show array