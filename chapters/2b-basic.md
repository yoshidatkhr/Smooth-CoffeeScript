#<a name = "ベーシック CoffeeScript">ベーシック CoffeeScript</a>

##値、変数と操作方法

コンピュータ世界はデータのみで出来ています。データでないものは存在しません。事実、すべてのデータはビットの固まりから作られ、各データはそれぞれの役割を担っています。CoffeeScriptシステムにおいて、ほとんどのデータは値というモノに分割されます。値の型は6種類あり、数値型（Numbers）、文字列型（Strings）、真  偽値（Booleans）、オブジェクト型（Objects）、関数型（Functions）、（Underfined）未定義型に分けられます。

値を作るときはその名前を呼び出すだけで良いです。めっちゃべんりです。事前に値を宣言する必要はなく、それを呼び出すだけでいいんです！フー！もちろん何もないところから作り出される訳ではありません。どの値もどこかにストックされています。もし同時にものすごくたくさんの値を使う場合、メモリを使い切るかもしれません。幸運な事に、本当に同時にその値を必要とする場合だけ問題になります。値は、しばらく使われないとすぐに数ビットを残し消されます。それらのビットは次に値を作る時に再利用されます。

---
数値型の値はご想像通り、数値です。数値型はいつも通り以下のように書かれます。

<pre>144</pre>

コンソールに144と入力してください。すると同じ値が出力されるはずです。この入力は数値型として解釈され、コンソールはこの数値を取得し、再度スクリーンに出力します。こんな練習は意味がなかったかもしれないけど、これからはもっと複雑な方法で値を作って行く事になるでしょう。コンソール上でプログラムが何を出力するのかを試すのは有用でしょう。

これはビットで表現した144です。

	01000000 01100010 00000000 00000000 00000000 00000000 00000000 00000000

上記の数値は64bitで、CoffeeScriptのnumbersは常に64bitです。これには重要な影響があります。表現できるnumbersの量を制限されてしまうことです。３桁だと0から999までしか書く事が出来ません。103=異なった1000の数値。64進数だと264の異なった数値を書く事ができます。これは大きい数で、1019以上です。

すべての10の19乗より下の整数がCoffeeScriptの数値に当てはまるわけではない。たいていの負の数値がそれに当てはまります。なので、それらの数値の象徴を格納しなくてはなりません。大きな問題は、非整数を表現しなくてはいけないことです。これをするには、11ビットは小数点に格納されます。

52ビットを残します。252以上1015以下の整数は安心してCoffeeScriptで使えます。たいていの場合、普段使っている数値は使えます。どっちが良いでしょう。私は特にビットに対して何も思わないけど、あなたは何かをするときにひどい大量のビットが必要なのですか。すべてが可能なら、大きなやりとりが快適になります。

少数はドットを使って表現します。

	9.81

非常に大きいか小さい数値の場合、たいていeを加えることで’科学的’表記法を利用できます。

	2.998e8

上の数値は2.998 ·108 = 299 800 000を表します。

52ビットに当てはまるwhole numbersの計算（だいたいintegersの事を指します）は正確であると保証されています。残念ながら、分数計算は通常できません。π (pi)のようなものは少数桁により計算できず、計算ミスになります。

>***ここから(p.21-)P.43までGoogle先生による翻訳です。どなたか…***

**原文**
Which is 2.998 108 = 299 800 000.
Calculations with whole numbers (also called integers) that fit in 52 bits are guaranteed to always be precise. Unfortunately, calculations with fractional numbers are generally not. Like π(pi) can not be precisely expressed by a finite amount of decimal digits, many numbers lose some precision when only 64 bits are available to store them. This is a shame, but it only causes practical problems in very specific situations7. The important thing is to be aware of it, and treat fractional digital numbers as approximations, not as precise values.

---
The main thing to do with numbers is arithmetic. Arithmetic operations such as addition or multiplication take two number values and produce a new number from them. Here is what they look like in CoffeeScript:
	100 + 4 * 11The + and * symbols are called operators. The first stands for addition, and the second for multiplication. Putting an operator between two values will apply it to those values, and produce a new value.
Does the example mean ‘add 4 and 100, and multiply the result by 11’, or isthe multiplication done before the adding? As you might have guessed, themultiplication happens first. But, as in mathematics, this can be changedby wrapping the addition in parentheses:	(100 + 4) * 11For subtraction, there is the - operator, and division can be done with /.When operators appear together without parentheses, the order in whichthey are applied is determined by the precedence of the operators. The firstexample shows that multiplication has a higher precedence than addition.Division and multiplication always come before subtraction and addition.When multiple operators with the same precedence appear next to eachother (1 - 1 + 1) they are applied left-to-right.Try to figure out what value this produces, and then run it to see if youwere correct…
	115 * 4 - 4 + 88 / 2These rules of precedence are not something you should worry about.When in doubt, just add parentheses.
There is one more arithmetic operator which is probably less familiar toyou. The % symbol is used to represent the modulo operation. X modulo Yis the remainder of dividing X by Y. For example 314 % 100 is 14, 10 % 3is 1, and 144 % 12 is 0. Modulo has the same precedence as multiplicationand division.

---   The next data type is the string. Its use is not as evident from its nameas with numbers, but it also fulfills a very basic role. Strings are used torepresent text, the name supposedly derives from the fact that it strings togethera bunch of characters. Strings are written by enclosing their contentin quotes:
	'Patch my boat with chewing gum.'Almost anything can be put between quotes, and CoffeeScript will makea string value out of it. But a few characters are tricky. You can imaginehow putting quotes between quotes might be hard.	'The programmer pondered: "0x2b or not 0x2b"'CoffeeScript implements both single quoted and double quoted strings,which can be handy when you have only one kind of quote in a string.	"Aha! It's 43 if I'm not a bit off"Double quoted strings can contain interpolated values, small snippets ofCoffeeScript code between #{ and }. The code is evaluated and inserted into the string.	"2 + 2 gives #{2 + 2}"Newlines, the things you get when you press enter, can not be put betweenquotes in the normal form of strings. A string can span multiple lines to help avoid overly long lines in the program but the line breaks are not shown in the output.	
	'Imagine if this was a	very long line of text'

---  CoffeeScript has triple-quoted strings aka heredocs to make it easy to havestrings that span multiple lines where the line breaks are preserved in theoutput. Indentation before the quotes are ignored so the following linescan be aligned nicely.	'''First comes A	then comes B'''The triple double quoted variant allows for interpolated values.	""" 1	+ 1	\---	\#{1 + 1}"""Still to be able to have special characters in a string, the following trick is used: Whenever a backslash (‘\’) is found inside quoted text, it indicatesthat the character after it has a special meaning. A quote that is preceded by a backslash will not end the string, but be part of it. When an ‘n’ characteroccurs after a backslash, it is interpreted as a newline. Similarly, a ‘t’ after a backslash means a tab character.	'This is the first line\nAnd this is the second'There are of course situations where you want a backslash in a string to bejust a backslash, not a special code. If two backslashes follow each other,they will collapse right into each other, and only one will be left in theresulting string value:	'A newline character is written like \"\\n\".'
---
  Strings can not be divided, multiplied, or subtracted. The + operator canbe used on them. It does not add, but it concatenates, it glues two stringstogether.	'con' + 'cat' + 'e' + 'nate'There are more ways of manipulating strings, but these are discussed later.

---
  Not all operators are symbols, some are written as words. For example,the typeof operator, which produces a string value naming the type of thevalue you give it.
	typeof 4.5
The other operators we saw all operated on two values, typeof takes onlyone. Operators that use two values are called binary operators, while thosethat take one are called unary operators. The minus operator can be usedboth as a binary and a unary operator8:
	-(10 - 2)
---  Then there are values of the boolean type. There are two of these: trueand false. CoffeeScript has some aliases for them: true can be written as yes or on. false as no or off. These alternatives can in some cases make a program easier to read. Here is one way to produce a true value:
	3 > 2And false can be produced like this:	3 < 2I hope you have seen the > and < signs before. They mean, respectively, ‘isgreater than’ and ‘is less than’. They are binary operators, and the result ofapplying them is a boolean value that indicates whether they hold in thiscase. You can chain comparisons to test if something is within an interval.These comparisons give respectively true and false:	100 < 115 < 200	100 < 315 < 200Strings can be compared in the same way:	'Aardvark' < 'Zoroaster'The way strings are ordered is more or less alphabetic. More or less…Uppercase letters are always ‘less’ than lowercase ones, so 'Z' < 'a' istrue, and non-alphabetic characters (‘!’, ‘@’, etc) are also included in theordering. The actual way in which the comparison is done is based onthe Unicode standard. This standard assigns a number to virtually everycharacter one would ever need, including characters from Greek, Arabic,Japanese, Tamil, and so on. Having such numbers is practical for storingstrings inside a computer — you can represent them as a list of numbers.When comparing strings, CoffeeScript just compares the numbers of thecharacters inside the string, from left to right.8Note that there is no space between the unary minus and the value.Other similar operators are >= (‘is greater than or equal to’), <= (‘is lessthan or equal to’), == (‘is equal to’), and != (‘is not equal to’). Equal tocan also be written in text as is and not equal to as isnt.	'Itchy' isnt 'Scratchy'  ---There are also some useful operations that can be applied to boolean valuesthemselves. CoffeeScript supports three logical operators: and, or, andnot. These can be used to ‘reason’ about booleans.The logical and operator can also be written as &&. It is a binary operator,and its result is only true if both of the values given to it are true.	true and falseLogical or with alias ||, is true if either of the values given to it is true:	true or falsenot can be written as an exclamation mark, !, it is a unary operator thatflips the value given to it, !true is false, and not false is true.**Exercise 1**	((4 >= 6) || ('grass' != 'green')) &&	!(((12 * 2) == 144) && true)	Is this true? For readability, there are a lot of unnecessary parentheses in there. This simple version means the same thing:	(4 >= 6 or 'grass' isnt 'green') and	not(12 * 2 is 144 and true)**Solution**
	Yes, it is true. You can reduce it step by step like this:	(false or true) and not(false and true)	true and not false
	true	I hope you noticed that 'grass' != 'green' is true. Grass may be green, but it is not equal to green.It is not always obvious when parentheses are needed. In practice, one can usually get by with knowing that of the operators we have seen so far, or has the lowest precedence, then comes and, then the comparisonoperators (>, ==, etcetera), and then the rest. This has been chosen in sucha way that, in simple cases, as few parentheses as possible are necessary.
---
  All the examples so far have used the language like you would use a pocket calculator. Make some values and apply operators to them to get new values. Creating values like this is an essential part of every CoffeeScriptprogram, but it is only a part. A piece of code that produces a value iscalled an expression. Every value that is written directly (such as 22 or 'psychoanalysis') is an expression. An expression between parentheses is also an expression. And a binary operator applied to two expressions,or a unary operator applied to one, is also an expression.There are a few more ways of building expressions, which will be revealed when the time is ripe.
There exists a unit that is bigger than an expression. It is called a statement.A program is built as a list of statements. Most statements end with anewline, although a statement can stretch over many lines. Statements canalso end with a semicolon (;). In CoffeeScript semicolon is mostly used ifyou want to place multiple statements on the same line. The simplest kindof statement is an expression with a semicolon after it. This is a program:
	1; !false
It is a useless program. An expression can be content to just produce avalue, but a statement only amounts to something if it somehow changesthe world. It could print something to the screen — that counts as changingthe world — or it could change the internal state of the program in a waythat will affect the statements that come after it. These changes are called‘side effects’. The statements in the example above just produce the values1 and true, and then immediately throw them into the bit bucket9. Thisleaves no impression on the world at all, and is not a side effect.
---
  How does a program keep an internal state? How does it remember things?We have seen how to produce new values from old values, but this doesnot change the old values, and the new value has to be immediately usedor it will dissipate again. To catch and hold values, CoffeeScript providesa thing called a variable.
	caught = 5 * 5
A variable always has a name, and it can point at a value, holding on to it.The statement above creates a variable called caught and uses it to grabhold of the number that is produced by multiplying 5 by 5.
After running the above program, you can type the word caught into theconsole, and it will retrieve the value 25 for you. The name of a variableis used to fetch its value. caught + 1 also works. A variable name canbe used as an expression, and thus can be part of bigger expressions.
Assigning a value to a new variable name with the = operator, creates thenew variable. Variable names can be almost every word, but they may notinclude spaces. Digits can be part of variable names, catch22 is a validname, but the name must not start with one. The characters ‘$’ and ‘_’ canbe used in names as if they were letters, so $_$ is a correct variable name.When a variable points at a value, that does not mean it is tied to that valueforever. At any time, the = operator can be used on existing variables toyank them away from their current value and make them point to a newone.
	caught = 4 * 4

---  You should imagine variables as tentacles, rather than boxes. They do notcontain values, they grasp them — two variables can refer to the samevalue. Only the values that the program still has a hold on can be accessedby it. When you need to remember something, you grow a tentacle tohold on to it, or re-attach one of your existing tentacles to a new value: Toremember the amount of dollars that Luigi still owes you, you could do…
	luigiDebt = 140
Then, every time Luigi pays something back, this amount can be decrementedby giving the variable a new number:
	luigiDebt = luigiDebt - 35
The collection of variables and their values that exist at a given time iscalled the environment. When a program starts up, this environment is notempty. It always contains a number of standard variables. When you usecoffee to execute a CoffeeScript program or run the interactive environmentwith coffee -r ./prelude then the environment is called global.You can view it by typing: this. !j / ‘Tab’. When your browser loads apage, it creates a new environment called window and attaches these standardvalues to it. The variables created and modified by programs on thatpage survive until the browser goes to a new page.

---  A lot of the values provided by the standard environment have the type‘function’. A function is a piece of program wrapped in a value. Generally,this piece of program does something useful, which can be evokedusing the function value that contains it. In the development environment,the variable show holds a function that shows a message in the terminal orcommand line window. You can use it like this:	show 'Also, your hair is on fire.'Executing the code in a function is called invoking or applying it. Thenotation for doing this is the function name followed by parentheses or acomma separated list of values. Every expression that produces a functionvalue can be invoked by putting parentheses after it. The parenthesescan be left out when values are passed. The string value is given to thefunction, which uses it as the text to show in the console window. Valuesgiven to functions are called parameters or arguments. show needs onlyone of them, but other functions might need a different number.

---  Showing a message is a side effect. A lot of functions are useful becauseof the side effects they produce. It is also possible for a function to producea value, in which case it does not need to have a side effect to be useful.For example, there is a function Math.max, which takes two argumentsand gives back the biggest of the two:	show Math.max 2, 4When a function produces a value, it is said to return it. Because thingsthat produce values are always expressions in CoffeeScript, function callscan be used as a part of bigger expressions:	show 100 + Math.max 7, 4	show Math.max(7, 4) + 100	show Math.max(7, 4 + 100)	show Math.max 7, 4 + 100When parentheses are left out from a function call then CoffeeScript implicitlyinserts them stretching to the end of the line. In the example aboveit means that the first two lines gives the answer 107 and the last two 104.So depending on your intention you may have to use parentheses to getthe result you want. Functions discusses writing your own functions.
---
  As the previous examples illustrated, show can be useful for showing theresult of an expression. show is not a standard CoffeeScript function,browsers do not provide it for you, it is made available by the Smooth Coffee-Script prelude. When you are working in a web browser, you have a differentenvironment and can instead use alert to pop up a dialog with a message.We will continue in the CoffeeScript environment. show tries to displayits argument the way it would look in a program, which can give moreinformation about the type of a value. In an interactive console, startedwith coffee -r ./prelude, you can explore the environment:	show process	show console	show _	show showWhat the output means is not so important for now. show is a tool that cangive you details on the things in your programs, which can be handy later,if something does not behave the way you had expected.
---
  The environment provided by browsers contains a few more functions forpopping up windows. You can ask the user an OK/Cancel question usingconfirm. This returns a boolean, true if the user presses ‘OK’, and falseif he presses ‘Cancel’. The prelude has a similar confirm function wherethe user is asked yes or no to the question.
Since the CoffeeScript environment is optimized to run as a server, it doesnot wait for the user to reply. Instead it continues running the code followingthe function call. Eventually when the user has answered the then a function given as an argument is called with the answer. This pieceof code involves a bit of magic, that will be explained in Functions. While itis more complicated for this use, we will in later chapters see that it makesperfect sense for a web application with many users.	confirm 'Shall we, then?', (answer) -> show answerprompt can be used to ask an ‘open’ question. The first argument is thequestion, the second one is the text that the user starts with. A line oftext can be typed into the window, and the function will — in a browser— return this as a string. As with confirm the prelude offers a similarfunction, that takes a third argument which will receive the answer.	
	prompt 'Tell us everything you know.', '...',	(answer) -> show 'So you know: ' + answer
---
 It is possible to give almost every variable in the environment a new value.This can be useful, but also dangerous. If you give show the value 8, youwill not be able to show things anymore. Some functions like confirm andprompt works when you run your program from a file, but interact poorlywith the interactive environment. Fortunately, you can stop a programwith CTRL-C and pick up where you left off. 
---
 One-line programs are not very interesting. When you put more than onestatement into a program, the statements are, predictably, executed one ata time, from top to bottom.	prompt 'Pick a number', '', (answer) ->	  theNumber = Number answer	  show 'Your number is the square root of ' +		(theNumber * theNumber)The function Number converts a value to a number, which is needed in thiscase because the answer from prompt is a string value. There are similarfunctions called String and Boolean which convert values to those types.
---
  Consider a program that prints out all even numbers from 0 to 12. Oneway to write this is:	show 0	show 2	show 4	show 6	show 8	show 10	show 12That works, but the idea of writing a program is to make something lesswork, not more. If we needed all even numbers below 1000, the abovewould be unworkable. What we need is a way to automatically repeatsome code.	currentNumber = 0	while currentNumber <= 12	  show currentNumber	  currentNumber = currentNumber + 2You may have seen while in the Introduction chapter. A statement startingwith the word while creates a loop. A loop is a disturbance in the sequenceof statements, it may cause the program to repeat some statements multipletimes. In this case, the word while is followed by an expression, whichis used to determine whether the loop will loop or finish. As long as theboolean value produced by this expression is true, the code in the loopis repeated. As soon as it is false, the program goes to the bottom of theloop and continues as normal.The variable currentNumber demonstrates the way a variable can track theprogress of a program. Every time the loop repeats, it is incremented by2, and at the beginning of every repetition, it is compared with the number12 to decide whether to keep on looping.
The third part of a while statement is another statement. This is the bodyof the loop, the action or actions that must take place multiple times. Indentationis used to group statements into blocks. To the world outside theblock, a block counts as a single statement. In the example, this is usedto include in the loop both the call to show and the statement that updatescurrentNumber.
If we did not have to print the numbers, the program could have been:	counter = 0	while counter <= 12 then counter = counter + 2Here, counter = counter + 2 is the statement that forms the body of theloop. The then keyword separates the boolean from the body, so both canbe on the same line.
**Exercise 2**
	Use the techniques shown so far to write a program that calculates and shows the value of 210 (2 to the 10th power). You are, obviously, not allowed to use a cheap trick like just writing 2 * 2 * ...
	If you are having trouble with this, try to see it in terms of the evennumbers example. The program must perform an action a certain amount of times. A counter variable with a while loop can be used for that. Instead of printing the counter, the program must multiply something by 2. This something should be another variable, in which the result value is built up.
	Do not worry if you do not quite see how this would work yet. Even if you perfectly understand all the techniques this chapter covers, it can be hard to apply them to a specific problem. Reading and writing code will help develop a feeling for this, so study the solution, and try the next exercise.
**Solution**	result = 1	counter = 0	while counter < 10	  result = result * 2	  counter = counter + 1	show result	The counter could also start at 1 and check for <= 10, but, for reasons that will become apparent later on, it is a good idea to get used to counting from 0. 

	Obviously, your own solutions are not required to be precisely the same as mine. They should work. And if they are very different, make sure you also understand my solution.**Exercise 3**
	With some slight modifications, the solution to the previous exercise can be made to draw a triangle. And when I say ‘draw a triangle’ I mean ‘print out some text that almost looks like a triangle when you squint’.
	Print out ten lines. On the first line there is one ‘#’ character. On the second there are two. And so on.
	How does one get a string with X ‘#’ characters in it? One way is to build it every time it is needed with an ‘inner loop’ — a loop inside a loop. A simpler way is to reuse the string that the previous iteration of the loop used, and add one character to it.**Solution**
	line = ''	counter = 0	while counter < 10
	  line = line + '#'	  show line	  counter = counter + 1
You will have noticed the spaces I put in front of some statements. Theseare required: The level of indentation decides which block a line belongsto. The role of the indentation inside blocks is to make the structure of thecode clearer to a reader. Because new blocks can be opened inside otherblocks, it can become hard to see where one block ends and another beginsif they were not indented. When lines are indented, the visual shape of aprogram corresponds to the shape of the blocks inside it. I like to use twospaces for every open block, but tastes differ. If a line becomes too long,then you can split it between two words or place a \ at the end of the lineand continue on the next. 
---
The uses of while we have seen so far all show the same pattern. First, a‘counter’ variable is created. This variable tracks the progress of the loop.The while itself contains a check, usually to see whether the counter hasreached some boundary yet. Then, at the end of the loop body, the counteris updated.A lot of loops fall into this pattern. For this reason, CoffeeScript, andsimilar languages, also provide a slightly shorter and more comprehensiveform:
	for number in [0..12] by 2 then show number
This program is exactly equivalent to the earlier even-number-printing example.The only change is that all the statements that are related to the‘state’ of the loop are now on one line. The numbers in square bracketsare a range [4..7], a list of numbers starting from the first number andgoing up one by one to the last. A range with two dots includes the lastnumber in the list (4,5,6,7), with three dots [4...7] the last number isexcluded (4,5,6). The amount of each step can be changed with the bykeyword. So [2..6] by 2 gives the list (2,4,6). Ranges can also decrementif the first number is largest, or involve negative numbers or floatingpoint numbers.
The number in the for comprehension take on each successive value fromthe range during each turn through the loop. The number value is thenavailable in the loop body where it can be used in computations or as herein show number. In most cases this is shorter and clearer than a whileconstruction.
The for comprehension can take on other forms as well. One is that thebody of the loop can be given before the for statement.	# For with indented body	for number in [0..12] by 2	  show number
	# For with prepended body	show number for number in [0..12] by 2

---  The lines that starts with ‘#’ in the previous example might have looked abit suspicious to you. It is often useful to include extra text in a program.The most common use for this is adding some explanations in human languageto a program.	# The variable counter , which is about to be defined ,	# is going to start with a value of 0, which is zero. counter = 0	# Now, we are going to loop, hold on to your hat.	while counter < 100 # counter is less than one hundred	  ###	  Every time we loop, we INCREMENT the value of counter 	  Seriously , we just add one to it.	  ###	  counter++	# And then, we are done.
This kind of text is called a comment. The rules are like this: ‘#’ startsa comment, which goes on until the end of the line. ‘###’ starts anotherkind of comment that goes on until a ‘###’ is found so it can stretch overmultiple lines.
As you can see, even the simplest programs can be made to look big, ugly,and complicated by simply adding a lot of comments to them.

---  I have been using some rather odd capitalisation in some variable names.Because you can not have spaces in these names — the computer wouldread them as two separate variables — your choices for a name that ismade of several words are more or less limited to the following:	fuzzylittleturtle FuzzyLittleTurtle	fuzzy_little_turtle fuzzyLittleTurtleThe first one is hard to read. Personally, I like the one with the underscores,though it is a little painful to type. However, since CoffeeScript evolvedfrom JavaScript, most CoffeeScript programmers follow the JavaScriptconvention with the last one. Its the one used by the standard JavaScriptfunctions. It is not hard to get used to little things like that, so I will justfollow the crowd and capitalise the first letter of every word after the first.In a few cases, such as the Number function, the first letter of a variableis also capitalised. This was done to mark this function as a constructor.What a constructor is will become clear in Object Orientation. For now, theimportant thing is not to be bothered by this apparent lack of consistency.
---
 Note that names that have a special meaning, such as while, and for maynot be used as variable names. These are called keywords. There are alsoa number of words which are ‘reserved for use’ in future versions of Java-Script and CoffeeScript. These are also officially not allowed to be usedas variable names, though some environments do allow them. The full listin Reserved Words is rather long.Do not worry about memorising these for now, but remember that thismight be the problem when something does not work as expected. In myexperience, char (to store a one-character string) and class are the mostcommon names to accidentally use.**Exercise 4**
	Rewrite the solutions of the previous two exercises to use for instead of while.
**Solution**
	result = 1	for counter in [0...10]	  result = result * 2	show result
	Note the use of the exclusive range and that — as required by Coffee-Script — the statement in the loop is indented two spaces which make it clear that it ‘belongs’ to the line above it.
	line = ''	for counter in [0...10]	  line = line + '#'	  show line
A program often needs to ‘update’ a variable with a value that is based onits previous value. For example counter = counter + 1. CoffeeScriptprovides a shortcut for this: counter += 1. This also works for manyother operators, for example result \*= 2 to double the value of result,or counter -= 1 to count downwards. counter++ and counter-- are shorter versions of counter += 1 and counter -= 1.---  Loops are said to affect the control flow of a program. They change theorder in which statements are executed. In many cases, another kind offlow is useful: skipping statements.We want to show all numbers between 0 and 20 which are divisible bothby 3 and by 4.	for counter in [0..20]	  if counter % 3 == 0 and counter % 4 == 0		show counter
The keyword if is not too different from the keyword while: It checksthe condition it is given, and executes the statement after it based on thiscondition. But it does this only once, so that the statement is executedzero or one time.
The trick with the modulo (%) operator is an easy way to test whether anumber is divisible by another number. If it is, the remainder of theirdivision, which is what modulo gives you, is zero.If we wanted to print all of the numbers between 0 and 20, but put parenthesesaround the ones that are not divisible by 4, we can do it like this:
	for counter in [0..20]	  if counter % 4 == 0		show counter	  if counter % 4 != 0		show '(' + counter + ')'
But now the program has to determine whether counter is divisible by4 two times. The same effect can be gotten by appending an else partafter an if statement. The else statement is executed only when the if’scondition is false.	for counter in [0..20]	  if counter % 4 == 0		show counter	  else		show '(' + counter + ')'
To stretch this trivial example a bit further, we now want to print thesesame numbers, but add two stars after them when they are greater than 15,one star when they are greater than 10 (but not greater than 15), and nostars otherwise.
	for counter in [0..20]	  if counter > 15		show counter + '**'	  else if counter > 10		show counter + '*'	  else		show counter
This demonstrates that you can chain if statements together. In this case,the program first looks if counter is greater than 15. If it is, the two starsare printed and the other tests are skipped. If it is not, we continue to checkif counter is greater than 10. Only if counter is also not greater than 10does it arrive at the last show statement.**Exercise 5**	Write a program to ask yourself, using prompt, what the value of 2 + 2 is. If the answer is ‘4’, use show to say something praising. If it is ‘3’ or ‘5’, say ‘Almost!’. In other cases, say something mean. Refer back to page 30 for the little bit of magic needed with prompt.	Solution
	prompt 'You! What is the value of 2 + 2?', '',	  (answer) ->		if answer == '4'		  show 'You must be a genius or something.'		else if answer == '3' || answer == '5'		  show 'Almost!'		else		  show 'You are an embarrassment.'
The logic tests in a program can become complicated. To help write conditionsclearly CoffeeScript provides a couple of variations on the if statement:The body of an if statement can be placed before the condition.And an if not can be written as unless .	fun = on	show 'The show is on!' unless fun is off  When a loop does not always have to go all the way through to its end,the break keyword can be useful. It immediately jumps out of the currentloop, continuing after it. This program finds the first number that is greaterthan 20 and divisible by 7:	current = 20	loop	  if current % 7 == 0		break	  current++	show currentThe loop construct does not have a part that checks for the end of the loop.It is the same as while true. This means that it is dependant on the breakstatement inside it to ever stop. The same program could also have beenwritten as simply…	current = 20	current++ until current % 7 == 0	show currentIn this case, the body of the loop comes before the loop test. The untilkeyword is similar to the unless keyword, but translates into while not.The only effect of the loop is to increment the variable current to itsdesired value. But I needed an example that uses break, so pay attentionto the first version too.**Exercise 6**
Pick a lucky number from 1 to 6 then keep rolling a simulated die,until your lucky number comes up. Count the number of rolls. Use aloop and optionally a break. Casting a die can be simulated with:	roll = Math.floor Math.random() * 6 + 1Note that loop is the same as while true and both can be used to createa loop that does not end on its own account. Writing while trueis a useful trick but a bit silly, you ask the program to loop as long astrue is true, so the preferred way is to write loop.**Solution**
	luckyNumber = 5 # Choose from 1 to 6	show "Your lucky number is #{luckyNumber}"	count = 0	loop	  show roll = Math.floor Math.random() * 6 + 1	  count++	  if roll is luckyNumber then break	show "Luck took #{count} roll(s)"	Another solution, arguably nicer, without break but abusing statistics:	luckyNumber = 3 # Choose from 1 to 6	show 'Your lucky number is ' + luckyNumber	count = 0	until roll is luckyNumber	  show roll = Math.floor Math.random() * 6 + 1	  count++	show 'You are lucky ' +		Math.floor(100/count) + '% of the time'
In the second solution to the previous exercise roll has not been set to avalue the first time through the loop. It is only assigned a value in the nextstatement. What happens when you take the value of this variable?	show mysteryVariable	mysteryVariable = 'nothing'In terms of tentacles, this variable ends in thin air, it has nothing to grasp.When you ask for the value of an empty place, you get a special valuenamed undefined. Functions which do not return an interesting value,such as the built-in function console.log also return an undefined value.Most things in CoffeeScript return a value, even most statements. Theprelude function show return the value it is given, so it can be used withinexpressions.
	show console.log 'I am a side effect.'
There is also a similar value, null, whose meaning is ‘this variable isdefined, but it does not have a value’. The difference in meaning betweenundefined and null is mostly academic, and usually not very interesting.In practical programs, it is often necessary to check whether something‘has a value’. In these cases, the expression something? may be used,the ? is called the existential operator. It returns true unless somethingis null or undefined. It also comes in an existential assignment form ?=which will only assign to a variable that is either null or undefined.	show iam ? undefined	iam ?= 'I want to be'	show iam	iam ?= 'I am already'	show iam if iam?  Which brings us to another subject… If you have been exposed to Java-Script then you know that comparisons of different types can be tricky.	show false == 0	show '' == 0	show '5' == 5In JavaScript all these give the value true — not so in CoffeeScript wherethey are all false. When comparing values that have different types, youhave to convert them into compatible types first. We saw this earlier withNumber so Number('5') == 5 gives true. The behaviour of == in Coffee-Script is the same as === in JavaScript.	
	show `null === undefined `	show `false === 0`	show `'' === 0`	show `'5' === 5`
All these are false. You can embed JavaScript in CoffeeScript by surroundingthe JavaScript code with backquotes. Using JavaScript whenyou have CoffeeScript is similar to embedding assembly language in ahigh-level language. It should be something you very rarely need to do.

---  There are some other situations that cause automatic type conversions tohappen. If you add a non-string value to a string, the value is automaticallyconverted to a string before it is concatenated. If you multiply a numberand a string, CoffeeScript tries to make a number out of the string.	show 'Apollo' + 5	show null + 'ify'	show '5' * 5	show 'strawberry' * 5The last statement prints NaN, which is a special value. It stands for ‘not anumber’, and is of type number (which might sound a little contradictory).In this case, it refers to the fact that a strawberry is not a number. All arithmeticoperations on the value NaN result in NaN, which is why multiplyingit by 5, as in the example, still gives a NaN value. Also, and this can bedisorienting at times, NaN == NaN equals false, checking whether a valueis NaN can be done with the isNaN function.
These automatic conversions can be very convenient, but they are alsorather weird and error prone. Even though + and * are both arithmeticoperators, they behave completely different in the example. In my owncode, I use + on non-strings a lot, but make it a point not to use * and theother numeric operators on string values.
Converting a number to a string is always possible and straightforward,but converting a string to a number may not even work (as in the last lineof the example). We can use Number to explicitly convert the string to anumber, making it clear that we might run the risk of getting a NaN value.
	show Number('5') * 5  
---
When we discussed the boolean operators && and || earlier, I claimedthey produced boolean values. This turns out to be a bit of an oversimplification.If you apply them to boolean values, they will indeed returnbooleans. But they can also be applied to other kinds of values, in whichcase they will return one of their arguments.
What || really does is this: It looks at the value to the left of it first. Ifconverting this value to a boolean would produce true, it returns this leftvalue, and otherwise it returns the one on its right. Check for yourself thatthis does the correct thing when the arguments are booleans. Why does itwork like that? It turns out this is very practical. Consider this example:
	prompt 'What is your name?', '',	  (input) ->		show 'Well hello ' + (input || 'dear')If the user presses - / ‘Enter’ without giving a name, the variable inputwill hold the value ''. This would give false when converted to a boolean.The expression input || 'dear' can in this case be read as ‘the value ofthe variable input, or else the string 'dear'’. It is an easy way to providea ‘fallback’ value.
The && operator works similarly, but the other way around. When thevalue to its left is something that would give false when converted toa boolean, it returns that value, and otherwise it returns the value on itsright.
Another property of these two operators is that the expression to their rightis only evaluated when necessary. In the case of true || X, no matterwhat X is, the result will be true, so X is never evaluated, and if it has sideeffects they never happen. The same goes for false && X.	false || alert 'I am happening!'	true || alert 'Not me.'

**原文ここまで**


64ビットだけがそれらを格納するために利用できる精度。これは恥ずべきことですが、それだけで非常に特定のsituations7で実用的な問題を引き起こします。 IM大きな貢献の事はない、正確な値として、それを認識し、近似値として小数デジタル数字を扱うことです。

数字に関係する主なものは、算術演算です。加算や乗算などの算術演算は、2つの数値の値を取るとそこから新しい番号を生成する。ここでは、CoffeeScriptのように見えるものです。

100 +4 *11

+や*の記号は演算子と呼ばれます。最初の加算、および乗算第二の略です。二つの値の間に演算子を置くことは、それらの値に適用し、新しい値が生成されます。

---
例では、平均"4と100を追加、および11での結果を掛ける"か、または追加する前に実行乗算ですか。ご想像のとおり、乗算は最初に発生します。しかし、数学のように、これは括弧の中にラップすることによって変更することができます。

	（100+ 4）* 11

演算子、および除算は/で行うことができます- 減算の場合は、そこです。演算子が括弧なしで一緒に表示されるときは、それらが適用される順序は、演算子の優先順位によって決定されます。最初の例では、乗算が加算よりも優先順位が高いことを示しています。除算と乗算は常に減算と加算の前に来る。同じ優先順位を持つ複数の演算子が隣同士に（1 - 1 + 1）表示されるとき、それらは左から右へ適用されます。

これが生成する値を把握し、正しいであった​​かどうかを確認するためにそれを実行しようと...

	115* 4 - 4 +2分の88

優先順位のこれらのルールは、あなたが心配すべきものではありません。疑問がある場合は、単に括弧を追加します。

おそらくあなたにはあまり馴染みが1つ以上の算術演算子があります。 ％記号はモジュロ演算を表すために使用されます。 xをyで割った剰余314％100が14の例ではYでXを割った余りである、10％3は1で、144％12は0です。モジュロ乗算と除算と同じ優先順位を持ちます。
___

次のデータ型は文字列です。その使用は、数字と、その名前から明らかなようにではありませんが、それはまた非常に基本的な役割を果たす。文字列はテキストを表すために使用されている、名前は、おそらくそれは文字の集合をGETHERする文字列という事実に由来する。文字列は、引用符でその内容を囲むことによって、書かれています：

	'Patch my boat with chewing gum.'

ほとんど何でも引用符の間に置くことができる、とCoffeeScriptはそれのうち文字列値を行います。しかし、いくつかの文字はトリッキーです。あなたが引用符で囲んで引用符を置くことが困難であることか想像することができます。

	'The programmer pondered: "0x2b or not 0x2b"'

CoffeeScriptは、文字列の引用符の1種類のみがある場合に便利かもしれません両方の単一引用符と二重引用符で囲まれた文字列を、実装しています。

	"Aha! It's 43 if I'm not a bit off"

二重引用符で囲まれた文字列は値が、＃{と}の間にCoffeeScriptコードの小さな断片を補間含めることができます。コードが評価され、文字列に挿入されます。

	"2 + 2 gives #{2 + 2}"

改行は、Enterキーを押すとあなたが得るものは、文字列の正規形で引用符の間に置くことはできません。文字列は、過度に長いの行が、改行が出力に示されていないを避けるために複数行プログラムにまたがることができます。

	'Imagine if this was a very long line of text' 

	'''Firs then comes B'''

三重二重引用符で囲まれたバリアントが値を補間することができます。

それでも文字列の特殊文字を持つことができるように、次のトリックが使われます。たびにバックスラッシュ（'\'）引用符で囲まれたテキストの中に発見され、それは文字の後にそれが特別な意味を持っていることを示します。バックスラッシュが前置される引用符は文字列を終了するが、それの一部にはなりません。 'n'の文字がバックスラッシュの後に発生すると、それは改行として解釈されます。同様に、バックスラッシュの後に't'はタブ文字を意味します。

	'This is the first line\nAnd this is the second'

あなただけのバックスラッシュに文字列にバックスラッシュではなく、特別なコードをしたいコースの状況があります。二つのバックスラッシュは、お互いに従えば、彼らはお互いに右潰されて、1つのみが結果の文字列の値のままになります。

	'A newline character is written like \"\\n\".'

文字列は、分割乗算、または減算することができます。 +演算子は、それらを使用することができます。それは追加するが、それ一緒に連結し、その接着つの文字列はありません。

	'con' + 'cat' + 'e' + 'nate'


そこに文字列を操作するためのより多くの方法がありますが、これらは、後で説明します。

すべての演算子が記号であるではない、いくつかの単語として書き込まれます。たとえば、あなたがそれを与える値の型を指定する文字列値を生成するtypeof演算子、。

	typeof 4.5

我々が見た他​​の演算子はすべて二つの値で動作、typeof演算は1つだけを取ります。いずれかの処置を講ずるものが単項演算子と呼ばれる中に2つの値を使用する演算子は、二項演算子と呼ばれます。マイナス演算子は両方のバイナリと単項operator8として使用することができます。

	-(10 - 2)

その後、ブール型の値があります。 trueとfalse：これらの二つがあります。 CoffeeScriptは、彼らのためにいくつかの別名があります。trueは、yesまたは上のように書くことができます。なしまたはオフなどの偽。これらの選択肢はいくつかのケースで読み込むためのプログラムが容易になります。ここに真の値を生成する一つの方法は、次のとおりです。

	3>2

3 <2とfalseは、このように製造することができる

私はあなたの前に>と<兆候を見ている願っています。彼らは、それぞれ、意味する'より大きい'と'はより小さい"。彼らは二項演算子であり、そしてそれらを適用した結果は、彼らがこのケースに保持するかどうかを示すブール値です。あなたは何かが区間内にあるかどうかをテストするためにチェーンの比較することができます。これらの比較はそれぞれ真と偽与える。

	100 < 115 < 200 100 < 315 < 200

文字列は、同じ方法で比較することができます。

	'Aardvark' < 'Zoroaster'

文字列が順序付けされている方法は、多かれ少なかれアルファベットです。多かれ少なかれ... ）大文字は常に小文字のものよりも"小さい"ですので、'Z'<'trueになり、アルファベット以外の文字('!','@'なども順序に含まれています。比較が行われている実際の方法は、Unicode標準に基づいています。この規格は1つがこれまでギリシャ語、アラビア語、日本語、タミル語などから文字を含めて、必要となるほぼすべての文字に番号を割り当てます。そのような番号を持つことは、コンピュータ内部の文字列を格納するための実用的です - あなたは、数値のリストとして表すことができます。文字列を比較するとき、CoffeeScriptは、ちょうど左から右へ、文字列内の文字の数字を比較します。
	
他の同様の演算子は> =（'より大きいか等しい"）、<=（'より小さいか等しい"）、==（"等しいです"）であり、および！=（'に等しいではない" ）。に等しくもない限りに等しいとしないテキストで記述できま​​す。

	'Itchy' isnt 'Scratchy'

ブール値自体に適用できるいくつかの便利な操作もあります。と、または、ではなく：CoffeeScriptは、3つの論理演算子をサポートしています。これらは真偽値に関する"理由"に使用することができます。
論理と演算子も＆＆のように記述することができます。それは二項演算子であり、そしてそれに与えられた値の両方に該当する場合、その結果は、唯一の真です。

	true and false

論理またはエイリアスを持つ| |それに与えられた値のいずれかに該当する場合、真です：trueまたはfalse

、感嘆符のように記述することができるではない！、それは、それに与えられた値を反転する単項演算子です！真偽偽、およびではない真です。

**問題1**

	((4 >= 6) || ('grass' != 'green')) && 
	!(((12 * 2) == 144) && true)
	これは本当ですか？読みやすくするために、そこに不必要な括弧がたくさんあり​​ます。こ	のシンプルなバージョンでは、同じことを意味します。
	(4 >= 6 or 'grass' isnt 'green') and 
	not(12 * 2 is 144 and true)

￼￼￼￼**答え**

	はい、それは本当です。このようなステップバイステップでそれを減らすことができます。

	私は"草"が！='グリーン'がtrueであることに気づいた願っています。草は緑かもしれないが、それは緑に等しいではありません。

	(false or true) and not(false and true) true and not false true

括弧が必要な場合には、必ずしも明白ではありません。実際には、一つは通常、比較演算子（>、==、エトセトラ）、そして残りの後、我々はこれまで見てきた演算子のことを知ることでやっていける、または最も低い優先順位を持って、次に来るとができます。これは、単純なケースでは、できるだけ少数の括弧が必要か、そのような方法で選択されています。

---
あなたが電卓を使用するのと同じようにすべての例では、これまでの言語を使用している。いくつかの値を確認し、新しい値を取得するためにそれらに演算子を適用する。このような値を作成すると、すべてのCoffeeScriptプログラムの重要な部分ですが、それは一部にすぎません。値を生成するコードの断片は表現と呼ばれています。 （このような22または"精神分析"など）に直接書き込まれるすべての値は式です。括弧の間の式も式です。と二つの式、または1つに適用される単項演算子に適用される二項演算子は、また式です。

時間が熟したときは明らかにされる建物の表現、さらにいくつかの方法があります。

の式より大きいユニットが存在する。それは、ステートメントと呼ばれています。プログラムは、文のリストとして構築されています。文が多くの行に渡ってできるもののほとんどのステートメントは、改行で終了。 （;）の文もセミコロンで終了することができます。あなたが同じ行に複数のステートメントを配置する場合CoffeeScriptセミコロンで主に使用されます。文の最も単純な種類は、それの後のセミコロンを持つ式なのです。これはプログラムです。
	1; !false

それは無駄なプログラムです。式は、単に値を生成するコンテンツになることができますが、それは何らかの形で世界を変える場合、ステートメントは何かにのぼります。それは、画面に何かを印刷することができる - それが世界を変えるとしてカウントする - またはそれはそれの後に来る文に影響を与える方法で、プログラムの内部状態を変更することができます。これらの変更は、"副作用"と呼ばれています。例の文では、上記の値だけ1と真を生成し、すぐにビットbucket9にそれらを投げる。これは全く世界には印象を残していない、と副作用ではありません。

プログラムはどのように内部状態を保持していますか？それはどのように物事を覚えているのでしょうか？私たちは、古い値から新しい値を生成する方法を見てきましたが、これは古い値を変更しない、と新しい値はすぐに使用することにしているか、それが再び消費されます。キャッチして値を保持するために、CoffeeScriptは変数と呼ばれるものが用意されています。

	caught = 5 * 5

---

変数は、常に名前があり、それを保持し、値で指定することができます。上記のステートメントでは、変数捕捉と呼ばれるを作成し、5を5で乗じて生成される数値のホールドをつかむためにそれを使用しています。

上記のプログラムを実行した後、コンソールにキャッチワードを入力すると、それはあなたのために値25を取得します。変数の名前は、その値を取得するために使用されます。キャッチ+ 1も動作します。変数名を式として使用することができ、より大きな式の一部にすることができます。

=演算子を持つ新しい変数名に値を割り当てると、新しい変数を作成します。変数名は、ほとんどすべての語を使用できますが、スペースが含まれていない場合があります。数字が変数名の一部にすることができます、catch22は有効な名前ですが、名前は1つで開始してはならない。彼らは文字であるかのように文字'$'と'_'が名に使用できるので、$ _ $は正しい変数名です。

ときに、それはそれは永遠にその値に結び付けられている値で変数の点を意味するものではありません。いつでも、=演算子は、その現在の値からそれらを離れてヤンクし、新しいものにそれらを指すように既存の変数を使用することができます。

	caught = 4 * 4

---
あなたは触手のような変数ではなく、箱を想像してみてください。彼らは値が含まれていない、彼らはそれらを把握する - 二つの変数が同じ値を参照することができます。プログラムがまだ保留されていることを唯一の値は、それによってアクセスすることができます。あなたが何かを覚えておく必要があるときは、触手はそれを保持するために、または新しい値に、既存の触手の一つを再アタッチ成長：ルイージはまだあなたを負っていることはドルの量を覚えてするには、何ができる...

	luigiDebt = 140

その後、ルイージは何かを支払うたびに、この金額は、することができますデクリメント変数に新しい番号を与えることでmented：

	luigiDebt = luigiDebt - 35

所定の時間に存在する変数とその値の集合は、環境と呼ばれています。プログラムが起動すると、この環境は、空ではありません。それは、常に標準的な変数の数が含まれています。あなたは、CoffeeScriptプログラムを実行したり、その後環境がグローバルと呼ばれるコーヒーの- r。/前奏曲とインタラクティブな環境を実行するためにコーヒーを使用したとき。あなたは次のように入力して、それを表示することができます：これ。 →| /'タブ"。ブラウザがページをロードするとき、それはウィンドウと呼ばれる新しい環境を作成し、それにこれらの標準値を添付します。ブラウザが新しいページになるまで、そのページ上で作成し、プログラムによって変更された変数が生き残る。

---
標準的な環境が提供する値の多くは、型'関数'を持っている。この関数は、値に包まれたプログラムの一部です。 GENER -同盟国、プログラムのこの部分は、それを含む関数の値を使用して誘発することができる便利なものを、行います。開発環境では、変数ショーは、端末またはコマンドラインウィンドウでメッセージを表示する機能を保持しています。このように使うことができます。

	show 'Also, your hair is on fire.'

関数内のコードを実行すると、それを呼び出すか、適用することと呼ばれています。これを行うための表記法は、括弧または値のカンマ区切りのリストが後に続く関数名です。関数るの値を生成するすべての式は、それの後に括弧を置くことによって呼び出すことができます。値が渡される場合には括弧を省略することができます。文字列値は、コンソールウィンドウに表示するテキストとして、それを使用する関数、に与えられます。関数に与えられた値は、パラメータまたは引数と呼ばれます。ショーは、いずれか一方だけを必要としますが、他の関数が別の番号が必要になることがあります。

メッセージを表示すると、副作用です。関数の多くは、理由は、生成副作用が便利です。それは、それが有用であることが副作用を持っている必要がない場合、値を、生成する機能も可能です。例えば、二つの引数を取るとバック両者の最大を与える関数のMath.maxは、あります。

	show Math.max 2, 4

関数が値を生成するとき、それはそれを返すように言われています。値を生成することが常にCoffeeScriptの式であるため、関数呼び出しは、より大きな式の一部として使用することができます。

	show 100 + Math.max 7, 4 show Math.max(7, 4) + 100 show Math.max(7, 4 + 100) showMath.max 7, 4 + 100

括弧は、関数からは除外されているときには、行の最後にストレッチを挿入CoffeeScript IM - plicitlyして呼ぶ。それ上の例では最初の2行が答え107最後の二つの104を与えることを意味します。だからあなたの意図に応じてあなたが望む結果を得るために括弧を使用する必要があります。関数は、独自の関数を書くことについて説明します。

---
前の例が示すように、ショーは式の結果を表示する場合に便利です。ショーは、標準のCoffeeScript関数ではないブラウザでは、あなたのためにそれを提供しない、それがスムーズコーヒースクリプトのプレリュードで利用できるようになります。 Webブラウザで作業しているときは、別の環境があり、代わりにメッセージを含むダイアログをポップアップするように警告することができます。

我々は、CoffeeScript環境で継続されます。ショーは、値の型についての詳細な情報を与えることができる、それがプログラムで見えるような方法を、その引数を表示しようとします。インタラクティブコンソールでは、コーヒー- rで開始/前奏曲は、あなたが環境を探索することができます。

どのような出力が意味することは、今はそれほど重要ではありません。ショーはあなたに何かが予想していたように動作しない場合は、後で便利なことができるプログラムのこと、についての詳細を与えることができるツールです。

ブラウザにより提供される環境では、ウィンドウがポップアップするためのいくつかのより多くの機能が含まれています。あなたは、ユーザーが[OK]を求める/確定を使って質問をキャンセルすることができます。これは、ブール値を押下"OK"であれば真、そして彼を押すが、"キャンセル"場合はfalseを返します。プレリュードでは、ユーザーが質問にyesまたはnoを聞かれていない同様の確認機能を備えています。

CoffeeScript環境がサーバとして動作するように最適化されているので、返信にユーザーのために待機しません。その代わりに、フォローINGコードを実行する関数呼び出しを続けています。最終的にユーザーが質問に応答したときに、

	show process
	show console
	show _
	show show

どのような出力手段と、今はそれほど重要ではありません。ショーができるツールです
あなたの後に便利なことができますあなたのプログラムで物事の詳細を与える、
何かがあなたが予想していたように動作していない場合。

---
その後、引数として渡された関数がその答えと呼ばれています。コー​​ドのこの部分は関数で説明する魔法のビットを伴います。それは、この使用のためのより複雑ですが、我々は後の章では、多くのユーザーとWebアプリケーションのための完

	confirm 'Shall we, then?', (answer) -> show answer

プロンプトが"オープン"質問をするために使用することができます。最初の引数は質問で、2番目はユーザーの起動に使用されるテキストです。テキスト行がウィンドウに入力することができ、関数は予定 - ブラウザで - 文字列として返します。として確定したプレリュードは、答えを受け取る番目の引数をとる同様の機能を、提供しています。

	prompt 'Tell us everything you know.', '...',	  (answer) -> show 'So you know: ' + answer

---
環境で新たな価値をほとんどすべての変数を与える事が可能です。これは便利なだけでなく、危険なことができます。あなたが値8を表示与えれば、あなたはもはや物事を表示することができなくなります。あなたがファイルからプログラムを実行するが、インタラクティブな環境で十分に相互作用の確認およびプロンプトの作品のようないくつかの関数。幸いにも、CTRL - Cでプログラムを停止し、中断したところから拾うことができます。

---
ワンラインプログラムは、非常に面白いものではありません。あなたがプログラムに複数のステートメントを配置すると、文は、予想通り、上から下へ、一つずつ実行されます。

	prompt 'Pick a number', '', (answer) ->	  theNumber = Number answer	  show 'Your number is the square root of ' +		(theNumber * theNumber)

機能番号は、プロンプトから答えがストリング値であるため、この場合に必要とされる数値、値を変換します。これらの型に値を変換する文字列やブールと呼ばれる同様の機能があります。

---
0から12へのすべての偶数を出力するプログラムを考えてみましょう。これを記述する一つの方法は、次のとおりです。

	show 0
	show 2
	show 4
	show 6
	show 8
	show 10
	show 12

動作しますが、プログラムを書くというアイデアは、何か少ない仕事ではなく、よりにすることです。我々が1000以下のすべての偶数を必要に応じて、上記では実行不可能であろう。必要なのは、自動的にいくつかのコードを繰り返す方法です。

	currentNumber = 0	while currentNumber <= 12	  show currentNumber	  currentNumber = currentNumber + 2

はじめの章の間は、見るかもしれない。ループを作成している間の単語で始まる文。ループは、文の順序の乱れている、それはいくつかのステートメントを複数回繰り返すようにプログラムを引き起こす可能性があります。このケースでは、単語の間は、ループは、ループまたは終了するかどうかを判断するために使用されている表現が続きます。この式によって生成されるブール値がtrueである限りとして、ループ内のコードが繰り返されます。とすぐにそれが偽であるとして、プログラムはループの一番下に移動し、通常どおり継続。

T変数currentNumberは、変数がプログラムの進行状況を追跡できる方法を示しています。たびにループが繰り返される、それは2ずつインクリメントされ、各繰り返しの開始時に、それがループし続けるかどうかを決定する12番と比較されます。

while文の3番目の部分は、別のステートメントです。これは、ループ、アクションや場所を複数回行なう必要のある操作のボディです。で、歯牙状の構造は、ブロックにグループステートメントに使用されます。ブロック外の世界に、ブロックは、単一の文として数えます。例では、これはループ内で表示する呼び出しと、更新がcurrentNumberという文の両方を含むように使用されます。

我々は数字を印刷するには持っていなかった場合、プログラムはあったかもしれない。

	counter = 0	while counter <= 12 then counter = counter + 2

ここで、カウンタ=カウンタ+ 2は、ループの本体を形成するステートメントです。そしてキーワードは体内からブール値を分離し、その両方が同じ行にすることができます。

￼￼￼	**問題2**

	210の値（2 10乗まで）を計算して表示するプログラムを書くことはこれまでに示した手法を使用してください。あなたは明らかに、わずか2 * 2 *を記述するような安価なトリックを使用するために許可されていない、です...

	この問題がある場合は、偶数番号の例の面でそれを見てみてください。プログラムはアクションを何度も一定量を実行する必要があります。 whileループでカウンタ変数は、そのために使用することができます。代わりにカウンターを印刷するので、プログラムが2で何かを掛ける必要があります。この何かは、結果値が構築されている、別の変数でなければなりません。

	あなたは非常にこれはまだどのように働くか見ても心配しないでください。あなたが完全にこの章で取り上げるすべてのテクニックを理解している場合でも、それは特定の問題に適用することは困難です。コー​​ドを読み書きすることはこのための感覚を開発するのに役立つので、解決策を検討し、次の練習をしてみてください。

￼￼￼￼	**答え**

	result = 1
	counter = 0
	while counter < 10
	  result = result * 2
	  counter = counter + 1
	show result

	カウンターがまた1から開始して= 10 <をチェックすることができる、しかし、後で明らかになる理由のため、それは0からカウントするために慣れるには良いアイデアです。

	明らかに、独自のソリューションは、私とまったく同じである必要はありません。彼らは動作するはずです。そして彼らは非常に異なっている場合、あなたがまた私の解決策を理解してください。



**問題3**

	多少変更して、前の練習への解決策は、三角形を描画させることができます。そして私は"は三角形を描く"と言うとき、私は"はほぼ三角形のようないくつかのテキストをプリントアウトする際に目を細め"という意味。
	
	10行をプリントアウトする。最初の行に1つの'＃'文字がある。第二上の2つがあります。というように。

	どのようにしてそれでX'＃'文字で文字列を取得するのですか？ループ内のループ - 一つの方法はそれを、それが"内側のループ"で必要になるたびに構築することです。簡単な方法は、ループの前の反復が使用されている文字列を再利用、およびそれの1文字を追加することです。

￼￼￼￼**答え**

	line = ''
	counter = 0
	while counter < 10
	  line = line + '#'
	  show line
	  counter = counter + 1

あなたは、私はいくつかのステートメントの前に置くスペースが気づいているだろう。これらは必須です：インデントのレベルは、行が属するブロックを決定します。ブロック内のインデントの役割は、読者へのコードの明確な構造を作ることです。新しいブロックが他のブロックの内部で開かれる可能性があるため、それは一つのブロックが終了するとそれらがインデントされていない場合は、別のが始まる場所を確認するのは困難になることができます。の行がインデントされている場合、プログラムの視覚的な形状は、その内部のブロックの形状に対応しています。私は開いているすべてのブロックの2つのスペースを使用したいのですが、味は異なります。行が長くなりすぎる場合は、その行の最後に2つの単語または場所\の間に分割し、次に続けることができます。

---
我々はこれまですべて同じパターンを示して見ている間の使用しています。最初に、"カウンター"変数が作成されます。この変数は、ループの進行状況を追跡します。

自身がチェックが含まれている間、通常のカウンタはまだいくつかの境界に達したかどうかを確認する。その後、ループ本体の最後に、カウンタが更新されます。

ループの多くはこのパターンに分類されます。このため、CoffeeScript、および類似の言語については、また少し短くし、より包括的なフォームを提供します。

	for number in [0..12] by 2 then show number

このプログラムは、以前の偶数番号 - 印刷元に十分とまったく同じです。唯一の変更点は、ループの"状態"に関連するすべての文が一行になっていることになります。角括弧内の数字は、範囲[4 .. 7]、数字の最初の番号から開始し、最後に1つずつ上がっていくの一覧です。 2つのドットを持つ範囲は、3つのドット[4 ... 7]最後の数が除外されている（4,5,6）とリスト（4,5,6,7）の最後の数字が含まれています。各ステップの量は、キーワードを変更することができます。ので[2 .. 6] 2によっては、リスト（2,4,6）を与える。最初の数字が最も大きい、またはであれば範囲も減らされるが、負の数または浮動小数点数を含むことができる。

理解するための番号は、ループを介して各ターンの間に範囲から後続の各値を取る。数の値は、それが計算にまたはここにショーの数のように使用することができるループの本体で使用できるようになります。ほとんどの場合、これはしばらくの間の建設より短く、明確です。

理解は、他の形態を取ることができるため。一つは、ループの本体はfor文の前に与えることができるということです。

前の例では'＃'で始まる行はあなたに少し不審に見えたかもしれない。それは、プログラム内の余分なテキストを含めることがしばしば有用です。このための最も一般的な使用方法はプログラムする人間で言語のいくつかの説明を追加しています。

	# For with indented body
	for number in [0..12] by 2
	  show number
	
	# For with prepended body
	show number for number in [0..12] by 2

---

	# The variable counter, which is about to be defined,
	# is going to start with a value of 0, which is zero.
	counter = 0
	# Now, we are going to loop, hold on to your hat.
	while counter < 100 # counter is less than one hundred
	  ###
	  Every time we loop, we INCREMENT the value of counter
	  Seriously, we just add one to it.
	  ###
	  counter++
	# And then, we are done.

This kind of text is called a comment. The rules are like this: ‘#’ starts a comment, which goes on until the end of the line. ‘###’ starts another kind of comment that goes on until a ‘###’ is found so it can stretch over multiple lines.

As you can see, even the simplest programs can be made to look big, ugly, and complicated by simply adding a lot of comments to them.

---

テキストのこの種のコメントと呼ばれています。ルールは次のようになります：'＃'は、行の終わりまで続くコメントを開始します。 '###'は、それが複数の行に伸ばすことができるように'###'が見つかるまで、上に行くコメントの別の種類を開始します。

ご覧のように、ごく単純なプログラムは、大きな醜い、と単純にそれらに多くのコメントを追加することによって、複雑に見えるために行うことができます。

◦•◦

私はいくつかの変数名にいくつかかなり奇妙な時価総額を使用している。これらの名前にスペースを持つことができないので - コンピュータは2つの別々の変数としてそれらを読んでいました - いくつかの単語で構成されている名前については、選択肢は以下の多かれ少なかれ制限されています。

	fuzzylittleturtle		FuzzyLittleTurtle
	fuzzy_little_turtle 	fuzzyLittleTurtle

最初は読みにくいです。それは型に少し痛いですが個人的に、私は、アンダースコアのものを好き。しかし、CoffeeScriptは、JavaScriptから進化したので、ほとんどのCoffeeScriptプログラマは最後のもので、JavaScriptの規則に従います。その標準のJavaScript関数で使用されるもの。それはそのようなささいなことに慣れるのは難しいではない、私は観客に従って、最初の後の各単語の最初の文字を大文字になりますので。

そのような番号の関数として、いくつかのケースでは、変数の最初の文字も大文字になります。これはコンストラクタとしてこの関数を記念して行われました。どのようなコンストラクタがあると、オブジェクト指向で明らかになります。今のところ、重要なことは、一貫性のこの明らかな不足に悩まされないためにです。

そのような中などの特別な意味を持つ名前、、と変数名として使用されていない可能性がありますのためのことに注意してください。これらは、キーワードと呼ばれます。 JavaベースのスクリプトとCoffeeScriptの将来のバージョンで"使用するために予約"されている単語の数もあります。一部の環境では、それらを許可していないものの、これらはまた、公式に、変数名として使用することを許可されていません。予約語の完全なリストは、やや長めです。

今のところこれらを暗記する心配が、これは何かが期待通りに動作しない問題になるかもしれないことを覚えてはいけません。私の経験では、CHAR（1文字の文字列を格納する）とクラスが誤って使用するのが最も一般的な名前です。


**￼￼￼問題4**

	代わりにしばらくの間使用する前の2つの演習のソリューションを書き換える。

￼￼￼￼**答え**

	result = 1
	for counter in [0...10]
	  result = result * 2
	  show result

	排他的な範囲とその使用方法に注意してください - で必要とされるコーヒー
	スクリプト - ループ内のステートメントは、make2のスペースでインデントされてい
	それは上の行に "属して"それは明らかです。

	line = ''	for counter in [0...10]	  line = line + '#'	  show line

プログラムは、多くの場合、その前の値に基づいて値を持つ変数を"更新"する必要があります。例えばカウンタ用=カウンタ+ 1。カウンタ+ = 1：CoffeeScriptは、このためのショートカットが用意されています。これはまた、下方にカウントする結果の値、またはカウンタ-= 1を倍増させる例の結果*= 2のために、他の多くの演算子のために動作します。カウンタ+ +とカウンター - カウンター+ = 1とカウンタ-= 1の短いバージョンです。

ループは、プログラムの制御フローに影響を与えると言われています。彼らは、ステートメントが実行される順序を変更します。多くの場合、フローの別の種類のに便利です：文をスキップする。

我々は3で、4の両方によって割り切れる0〜20のすべての数字を表示したいとします。

---
キーワードifキーワードの中からあまりにも違いはありません：それは、それが与えられた条件をチェックし、それがこの条件に基づいて後にステートメントを実行します。しかし、文が0回または1回実行されるように、一度だけこれを行います。

モジュロ（％）演算子を持つトリックは数が別の数で割り切れるかどうかをテストする簡単な方法です。その場合、モジュロを与えるものであるそれらの部門、、余りは0である。

我々は0〜20の数字のすべてを印刷したいが、4の倍数ではないものの周りに括弧学位論文を配置した場合、我々はこのようにしてください：

	for counter in [0..20]	  if counter % 4 == 0		show counter	  if counter % 4 != 0		show '(' + counter + ')'

しかし、今のプログラムは、カウンタが4の2倍で割り切れるかどうかを判断する必要があります。同じ効果は、if文の後には他の部分を付加することによって得ることができます。 else文は、ifの条件が偽のときのみ実行されます。

	for counter in [0..20]	  if counter % 4 == 0		show counter	  else		show '(' + counter + ')'

少しさらに、このような簡単な例を伸ばすために、我々は今これらの同じ番号を印刷したいが、彼らが15より大きいとき、彼らが10（ただし、15より大きい）より大きいとき、それらの後で1つ星を二つの星を追加し、ない星そうでなければ。

	for counter in [0..20]	  if counter > 15		show counter + '**'	  else if counter > 10		show counter + '*'	  else		show counter

これは一緒にif文の連鎖があることを示しています。カウンタが15よりも大きい場合は、このケースでは、プログラムは最初に見える。それがある場合は、二つの星が印刷され、他のテストはスキップされます。そうでない場合、我々はカウンターが10より大きいかどうかをチェックし続けます。カウンターも10より大きいではない場合にのみそれが最後のSHOWステートメントに到達しません。

￼￼￼**問題5**

	2 + 2の値が何であるかプロンプトを、使用して、自問するプログラムを書きなさい。答えは'4'の場合は、賞賛する何かを言うには、showを使用してください。それが'3'または'5'の場合は、"ほとんど！"と言う。他のケースでは、何か意味と言う。プロンプトで必要な魔法の少しのために30ページを参照して下さい。

￼￼￼￼**答え**

	prompt 'You! What is the value of 2 + 2?', '',
	  (answer) ->
		if answer == '4'
		  show 'You must be a genius or something.'
		else if answer == '3' || answer == '5' 
		  show 'Almost!'
		else
		  show 'You are an embarrassment.'

プログラムの論理テストが複雑になることができます。条件- tions書き込みを助けるために明確にCoffeeScriptは、上のバリエーションのいくつかを提供する場合は状態- MENT：ifステートメントの本体は、条件の前に置くことができるかどうか。としない限り、のように記述することができる場合ではない。

	fun = on
	show 'The show is on!' unless fun is off

ループは、常にその終りまでの全ての道を行くことがないときは、breakキーワードが便利です。それは、その直後に続けて、現在のループの外にジャンプします。このプログラムは20を超え、7で割り切れる最初の番号を検索します。

	current = 20	loop	  if current % 7 == 0		break	  current++	show current

ループ構造は、ループの終わりをチェックする部分を持っていません。それは、真の時間と同じです。これは、今まで停止してその中にbreak文に依存していることを意味します。同プログラムはまた、単純に書かれている可能性が...

	current = 20	current++ until current % 7 == 0	show current

この場合、ループの本体は、ループテストの前に来ます。キーワードがない限り、キーワード、しかし一方ではないに変換に似てまで。ループの唯一の効果は、その目的の値に可変電流をインクリメントすることです。しかし、私は休憩を使用する例を必要なので、あまりにも最初のバージョンに注意を払う。

￼￼￼**問題6**

	その後、1から6までのラッキーナンバーを選んであなたのラッキーナンバーが表示されるまで、シミュレートされたサイコロを保つ。ロールの数をカウントします。ループと、オプションでブレークを使用してください。ダイをキャストすると、シミュレーションすることができます。

	ロール=数学。床Math.random（）* 6 + 1

	そのループが真の間と同じであり、両方が独自のアカウント上で終わっていないループをCRE -食べたにも使用できます。真の有用なトリックが、ビットばかげている間に書き込み、あなたが真の真である限りループするプログラムを尋ねる、好ましい方法は、ループを記述することですので。

**答えf**

	luckyNumber = 5 # Choose from 1 to 6	show "Your lucky number is #{luckyNumber}"	count = 0	loop	  show roll = Math.floor Math.random() * 6 + 1	  count++	  if roll is luckyNumber then break	show "Luck took #{count} roll(s)"show "Luck took #{count} roll(s)"

	ブレークが悪用統計を除くほぼ間違いなくよりよい別の解決策:

	luckyNumber = 3 # Choose from 1 to 6	show 'Your lucky number is ' + luckyNumber	count = 0	until roll is luckyNumber	  show roll = Math.floor Math.random() * 6 + 1	  count++	show 'You are lucky ' +	  	Math.floor(100/count) + '% of the time'

前の実習のロールへの2番目のソリューションではループを介して値を初めて設定されていない。それは次のステートメントで値が割り当てられます。この変数の値を取る場合はどうなりますか？

	show mysteryVariable
	mysteryVariable = 'nothing'

触手の面では、この変数は、薄い空気で終わる、それは把握するのは関係ありません。あなたが空の場所の値を求めるときは、未定義の名前の特別な値を得る。このような組み込み関数として興味深い値を、返していない関数も定義されていない値を返すCONSOLE.LOG。 CoffeeScriptのほとんどのものは、さらにほとんどの文を値を返す。プレリュードの関数は、与えられた値を返すことを示すので、式の中で使用することができます。

	show console.log 'I am a side effect.'

その意味は同様の値、nullは、この変数は'もあります

定義されていますが、値を"持っていません。間の意味の違い

未定義とnullは主に学術的、そして通常非常に興味深いものではありません。実用的なプログラムでは、それは何かが"価値を持っている"かどうかを確認する必要がしばしばあります。このような場合で、式の何か？使用されるかもしれない、？実存的な演算子と呼ばれています。何かがnullまたはundefinedでない限り、それはtrueを返します。また、実存的な割り当​​ての形で来る？のみのどちらかがnullまたは未定義の変数に代入されます=。

	show iam ? undefined	iam ?= 'I want to be'	show iam	iam ?= 'I am already'	show iam if iam?

---
それは別の話題に私たちをもたらします...もしあなたが、Java - Scriptのにさらされているなら、あなたはさまざまなタイプの比較は難しいことができることを知っている。

	show false == 0	show '' == 0	show '5' == 5

JavaScriptでは、すべてのこれらは真の値を与える - ないのでそれらがすべて偽であるCoffeeScriptに。異なる型を持つ値を比較する場合には、まず、互換性のある型に変換する必要があります。我々は、数などの数（'5'）== 5は真与えるとこの前のを見た。コー​​ヒースクリプトで==の挙動は、JavaScriptの===と同じです。

	show `null === undefined `	show `false === 0`	show `'' === 0`	show `'5' === 5`

これらはすべてfalseです。あなたは、バッククォートでシュール丸めによってCoffeeScriptでJavaScriptコードをJavaScriptを埋め込むことができます。あなたがCoffeeScriptを持っている時にJavaScriptを使用すると、高水準言語でアセンブリ言語を埋め込むに似ています。それはあなたがする必要がない非常にまれなものでなければなりません。

---
自動型変換が発生する原因となるいくつかの他の状況があります。あなたが文字列に文字列以外の値を入れても、それが連結される前に、値は自動的に文字列に変換されます。あなたが数値と文字列を掛ける場合、CoffeeScriptは、文字列の数を作ることを試みます。

	show 'Apollo' + 5	show null + 'ify'	show '5' * 5	show 'strawberry' * 5

最後の文は、特殊な値であるNaNを出力します。それは"ではない数"の略で、（少し矛盾して聞こえる可能性がある）型はNUMBERです。この場合、それはイチゴが数値ではないという事実を表しています。なぜ5を乗じているがNaNの値がNaNの結果のすべての算術 - 算術演算は、、例のように、依然としてNaN値を与えます。また、これは時には混乱させることができる、NaNは== NaNは値がNaNがisNaNは関数で実行できるかどうかをチェックし、偽等しい。

これらの自動変換は非常に便利ですが、彼らはまた、やや奇妙なエラーが発生しやすくなります。 +と\*の両方の算術演算子が表示されています、これらは例の完全に異なる動作にもかかわらず。私自身のコードでは、私は非文字列の多くの上で+を使用しますが、その文字列値に*やその他の数値演算子を使用しないようにポイントします。

数値を文字列に変換することは常に可能と簡単ですが、文字列を数値に変換するにも（例の最後の行のように）動作しない場合があります。私たちは、明示的にそれを明確に我々がNaNの値を得ることの危険性を実行される可能性があるということ、文字列を数値に変換する数値を使用することができます。

	show Number('5') * 5

---
我々は、ブール演算子について議論＆＆とするとき| |以前、私は、彼らがブール値を生成したと主張した。これはoversim - plificationのビットであることが判明した。あなたがブール値に適用した場合、彼らは確かに真偽値を返します。しかし、彼らは他のタイプの値にも適用することができます、その場合、彼らは彼らのいずれかの引数を返します。

何が| |本当にこれはない：それは最初にそれの左側の値が参照されます。 booleanにこの値を変換することが真生成するような場合、それはこの左の値を返し、それ以外の場合は、その右上の1つを返します。これは、引数がブール値である正しいことを行うことを自分自身のために確認してください。それはなぜそのように動作しますか？これは非常に実用的であるがわかりました。この例を考えてみます。

	prompt 'What is your name?', '', 
	  (input) ->
		show 'Well hello ' + (input || 'dear')

ユーザーを押す←􏰀/名前を与えることなく、'Enter'をする場合、変数入力は値''を開催します。 booleanに変換するときにこれは偽与えるだろう。式の入力| |"親愛なる"は、このケースでは'''変数inputの値、または他の文字列'として親愛なる読み取ることができます。それは、"フォールバック"の価値を提供する簡単な方法です。

＆＆演算子と同様に動作しますが、他の方法で回避。その左側の値がブール値に変換されたときにfalseを与える何かであるときは、その値を返し、それ以外の場合は、右側にある値を返します。

これら2つの演算子の別のプロパティは、必要に応じて、右側の式が唯一評価されるということです。真の場合、| | X、Xが何であるかに関係なく、結果はtrueにならないので、Xは評価されません、そして、それが副作用を持つ場合、それらが発生されることはありません。同じはfalse＆＆Xのために行く

	false || alert 'I am happening!' 
	true || alert 'Not me.' 


ここまでGoogle先生の翻訳