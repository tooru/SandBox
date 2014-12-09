# JSHint Options

* This is a complete list of all configuration options accepted by JSHint. If you see something missing, you should either file a bug or email me.

## Enforcing options

* When set to true, these options will make JSHint produce more warnings about your code.

### bitwise

* This option prohibits the use of bitwise operators such as ^ (XOR), | (OR) and others. Bitwise operators are very rare in JavaScript programs and quite often & is simply a mistyped &&.
* `^` (XOR) や `|` (OR) 等のビット演算子を禁止します。ビット演算子はJavaScriptで使うことは稀で、よく`&&`の間違いとして`&`を使用することがあります。

### camelcase
* This option allows you to force all variable names to use either camelCase style or UPPER_CASE with underscores.
* すべての変数名は、キャメルケースか大文字+アンダースコアでなくてはなりません。

### curly
* This option requires you to always put curly braces around blocks in loops and conditionals. JavaScript allows you to omit curly braces when the block consists of only one statement, for example:
* ループや条件文で必ず`{}`を付けなければなりません。JavaScriptはブロックが1つのステートメントの場合、`{}`を省略できます。
```
while (day)
  shuffle();
```
* However, in some circumstances, it can lead to bugs (you'd think that sleep() is a part of the loop while in reality it is not):
* しかし、状況によっては、これが不具合を引き起こします。`sleep()`がwhileループの一部に見えますが、そうではありません。

```
while (day)
  shuffle();
  sleep();
```

### eqeqeq
* This options prohibits the use of == and != in favor of === and !==. The former try to coerce values before comparing them which can lead to some unexpected results. The latter don't do any coercion so they are generally safer. If you would like to learn more about type coercion in JavaScript, we recommend Truth, Equality and JavaScript by Angus Croll.
* このオプションは`==`と`!+`よりも`===`と`!==`を使用する事を禁止します。前者は比較の前に値を変換させるため予期せぬ結果を引き起こしかねません。後者はそのような変換が行われないので一般的に安全です。JavaScriptの変換のもっと詳しい情報は、[Equality and Javascript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/)がおすすめです。


### es3
* This option tells JSHint that your code needs to adhere to ECMAScript 3 specification. Use this option if you need your program to be executable in older browsers—such as Internet Explorer 6/7/8/9—and other legacy JavaScript environments.
* このオプションは、ECMAScript 3 に準拠しているか調べます。IE6/7/8/9のような古いJavaScript実行環境で動作させたいときに使います。


### forin
* This option requires all for in loops to filter object's items. The for in statement allows for looping through the names of all of the properties of an object including those inherited throught the prototype chain. This behavior can lead to unexpected items in your object so it is generally safer to always filter inherited properties out as shown in the example:
* このオプションは`for in`ループで、オプジェクトのアイテムかどうか調べることを矯正します。`for in` はプロトタイプチェーンで継承されたものを含む全てのプロパティでループされます。望まない要素がオブジェクトに含まれているかもしれないので、普通は次のように継承されたプロパティをフィルタします。

```
for (key in obj) {
  if (obj.hasOwnProperty(key)) {
    // We are sure that obj[key] belongs to the object and was not inherited.
  }
}
```
* For more in-depth understanding of for in loops in JavaScript, read Exploring JavaScript for-in loops by Angus Croll.
* JavaScriptの`for in`ループのもっと詳しい情報は、Angus Crollの[Exploring JavaScript for-in loops](http://javascriptweblog.wordpress.com/2011/01/04/exploring-javascript-for-in-loops/)を参考にしてください。

### freeze
* This options prohibits overwriting prototypes of native objects such as Array, Date and so on.
* このオプションは、`Array`や`Date`などのNativeオブジェクトのプロトタイプを上書きするとを禁止します。

```
/* jshint freeze:true */
Array.prototype.count = function (value) { return 4; };
// -> Warning: Extending prototype of native object: 'Array'.
```

### immed
* This option prohibits the use of immediate function invocations without wrapping them in parentheses. Wrapping parentheses assists readers of your code in understanding that the expression is the result of a function, and not the function itself.
* このオプションは、`()`を伴わない即時関数呼び出しの使用を禁止します。`()`をつけると、評価結果が関数の戻り値であることが分かりやすくなります。

### indent
* This option sets a specific tab width for your code.
* このオプションはタブ幅を指定します。
* 2.5.0以降では無効です。https://github.com/jshint/jshint/releases/tag/2.5.0

### latedef
* This option prohibits the use of a variable before it was defined. JavaScript has function scope only and, in addition to that, all variables are always moved—or hoisted— to the top of the function. This behavior can lead to some very nasty bugs and that's why it is safer to always use variable only after they have been explicitly defined.
* このオプションでは変数を宣言の前に使用することを禁止します。JavaScriptは関数スコープしか持たないため、全ての変数は関数の先頭に移動します。この振る舞いは不具合につながりますので、変数は常に宣言の後に使用したほうが安全です。

* Setting this option to "nofunc" will allow function declarations to be ignored.
* このオプションに`"nofunc"`を指定すれば、関数の宣言については無視できます。

* For more in-depth understanding of scoping and hoisting in JavaScript, read JavaScript Scoping and Hoisting by Ben Cherry.
* JavaScriptのスコープや巻き上げ(hoisting)について詳しく知りたい場合は、Ben Cherryの[JavaScript Scoping and Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting)を参考にしてください。

* 指定可能な値
 * `false`   : 警告を出しません
 * `true`    : 宣言の前に使用している全ての変数で警告を出します
 * `"nofunc"`: 関数宣言を除く全ての変数で警告を出します

### newcap
* This option requires you to capitalize names of constructor functions. Capitalizing functions that are intended to be used with new operator is just a convention that helps programmers to visually distinguish constructor functions from other types of functions to help spot mistakes when using this.
* このオプションはコンストラクタ関数の名前を大文字始まりにすることを要求します。大文字始まりの関数は`new`演算子と共に使われることを意図しますので、コンストラクタ関数とそれ以外の関数を区別するための命名規則となります。

* Not doing so won't break your code in any browsers or environments but it will be a bit harder to figure out—by reading the code—if the function was supposed to be used with or without new. And this is important because when the function that was intended to be used with new is used without it, this will point to the global object instead of a new object.
* TODO

### noarg
* This option prohibits the use of arguments.caller and arguments.callee. Both .caller and .callee make quite a few optimizations impossible so they were deprecated in future versions of JavaScript. In fact, ECMAScript 5 forbids the use of arguments.callee in strict mode.
* このオプションは、`arguments.caller`と`arguments.callee`の使用を禁止します。`.caller`と`.callee`は共に僅かながら最適化をできなくしていますし、これらは将来JavaScriptのバージョンで非推奨なる予定です。実際、ECMAScript5では、strictモードでは、`arguments.callee`の使用を禁止しています。

### noempty
* This option warns when you have an empty block in your code. JSLint was originally warning for all empty blocks and we simply made it optional. There were no studies reporting that empty blocks in JavaScript break your code in any way.
* このオプションはからブロックに対して警告を出します。JSLintはすべての空ブロックに警告を出しますが、JSHintではオプションです。いかなる時もからブロックがコードを破壊するというstudies reportingはありません。


### nonbsp
* This option warns about "non-breaking whitespace" characters. These characters can be entered with option-space on Mac computers and have a potential of breaking non-UTF8 web pages.
* このオプションは、"non-breaking whitespace"に警告を出します。この文字はMacでoption+spaceで入力できてしまい、UTF-8でないWeb Pageを破壊する恐れがあります。


### nonew
* This option prohibits the use of constructor functions for side-effects. Some people like to call constructor functions without assigning its result to any variable:
* このオプションは副作用のためのコンストラクタ関数の使用を禁止します。コンストラクタ関数の結果を変数に代入することなく呼び出します。

```
new MyConstructor();
```

* There is no advantage in this approach over simply calling MyConstructor since the object that the operator new creates isn't used anywhere so you should generally avoid constructors like this one.
* これは単に`MyConstructor`を呼び出すこと以上に利点がありません。`new`演算子で生成されたオブジェクトは使われないので、このようなコンストラクタは一般的に避けるべきです。

### plusplus
* This option prohibits the use of unary increment and decrement operators. Some people think that ++ and -- reduces the quality of their coding styles and there are programming languages—such as Python—that go completely without these operators.
* このオプションは単項演算子インクリメントとデクリメントの使用を禁止します。`++`と`--`はコーディングスタイルの品質を下げると考える人もおり、Pythonなどの言語ではこの演算子が完全になくなっています。


### quotmark
* This option enforces the consistency of quotation marks used throughout your code. It accepts three values: true if you don't want to enforce one particular style but want some consistency, "single" if you want to allow only single quotes and "double" if you want to allow only double quotes.
* このオプションは、クオート記号の一貫性を矯正します。3つの値を取ります。
 * `true`: 1つの特定のスタイルにしたくないけど、いくらかの一貫性が欲しいとき
 * `"single"`: シングルクオートのみ許可
 * `"double"`: ダブルクオートのみ許可
 

### undef
* This option prohibits the use of explicitly undeclared variables. This option is very useful for spotting leaking and mistyped variables.
* このオプションは、明示的に宣言されていない変数の使用を禁止します。このオプションはリークやタイプミスを見つけるのに有効です。

```
/*jshint undef:true */
function test() {
  var myVar = 'Hello, World';
  console.log(myvar); // Oops, typoed here. JSHint with undef will complain タイポがあります。
}
```

* If your variable is defined in another file, you can use /*global ... */ directive to tell JSHint about it.
* 他のファイルで定義された変数は、`/*global ... */`を使うことでJSHintに教えることができます。

### unused

* This option warns when you define and never use your variables. It is very useful for general code cleanup, especially when used in addition to undef.
* このオプションは宣言したが使われていない変数に警告を出します。コードの掃除に便利です。特に`undef`と合わせて使ったとき。

```
/*jshint unused:true */
 
function test(a, b) {
  var c, d = 2;
  
  return a + d;
}
 
test(1, 2);
 
// Line 3: 'b' was defined but never used.
// Line 4: 'c' was defined but never used.
```
* In addition to that, this option will warn you about unused global variables declared via /*global ... */ directive.
* これに加えて、このオプションは、`/*global ... */`で宣言した使用していないグローバル変数にも警告を出します。

* This can be set to vars to only check for variables, not function parameters, or strict to check all variables and parameters. The default (true) behavior is to allow unused parameters that are followed by a used parameter.
* `"vars"`: 変数だけチェックし、関数パラメータはチェックしない
* `"strict"`: すべての変数と関数パラメータをチェックする
* `true`: デフォルト。使用しているパラメータの後ろの使用していないパラメータを許可する。


### strict
* This option requires all functions to run in ECMAScript 5's strict mode. Strict mode is a way to opt in to a restricted variant of JavaScript. Strict mode eliminates some JavaScript pitfalls that didn't cause errors by changing them to produce errors. It also fixes mistakes that made it difficult for the JavaScript engines to perform certain optimizations.
* このオプションは、すべての関数をECMAScript 5 のstrict modeで動作させることを要求します。strict modeはJavaScriptの厳格版TODO。strict mode は、エラーを引き起こさないJavaScriptの落とし穴をエラーが出るようにすることで、排除します。また、Javascriptエンジンが最適化するのを難しくしているミスを修正します。

* Note: This option enables strict mode for function scope only. It prohibits the global scoped strict mode because it might break third-party widgets on your page. If you really want to use global strict mode, see the globalstrict option.
* 注意：このオプションは、関数スコープでstrict modeを有効にします。Third party widgetを破壊するためグローバルのstrict modeを禁止します。global strict modeを使用したいなら、`globalstrict`オプションを参照してください。


### maxparams
* This option lets you set the max number of formal parameters allowed per function:
* このオプションは、関数の仮引数の最大数を指定します。

```
/*jshint maxparams:3 */
 
function login(request, onSuccess) {
  // ...
}
 
// JSHint: Too many parameters per function (4).
function logout(request, isManual, whereAmI, onSuccess) {
  // ...
}
```

### maxdepth
* This option lets you control how nested do you want your blocks to be:
* このオプションは、ブロックのネストの数を制限します。


```
/*jshint maxdepth:2 */
 
function main(meaning) {
  var day = true;
 
  if (meaning === 42) {
    while (day) {
      shuffle();
      if (tired) { //JSHint: Blocks are nested too deeply (3).
          sleep();
      }
    }
  }
}
```

### maxstatements
* This option lets you set the max number of statements allowed per function:
* このオプションは、関数のステートメントの最大数を指定します。

```
/*jshint maxstatements:4 */
 
function main() {
  var i = 0;
  var j = 0;
　
  // Function declarations count as one statement. Their bodies
  // don't get taken into account for the outer function.
  function inner() {
    var i2 = 1;
    var j2 = 1;
　
    return i2 + j2;
  }
　
  j = i + j;
  return j; // JSHint: Too many statements per function. (5)
}
```

### maxcomplexity
* This option lets you control cyclomatic complexity throughout your code. Cyclomatic complexity measures the number of linearly independent paths through a program's source code. Read more about cyclomatic complexity on Wikipedia.
* このオプションは、サイクロマチック複雑度を設定します。サイクロマチック複雑度は、コードの独立したパスの数を図るものです。詳しい情報は、Wikipediaを参考にしてください。


### maxlen
* This option lets you set the maximum length of a line.
* このオプションは、1行あたりの最大文字数を設定します。

## Relaxing options
* When set to true, these options will make JSHint produce less warnings about your code.

### asi
* This option suppresses warnings about missing semicolons. There is a lot of FU# JSHint Options

* This is a complete list of all configuration options accepted by JSHint. If you see something missing, you should either file a bug or email me.

## Enforcing options

* When set to true, these options will make JSHint produce more warnings about your code.

### bitwise
* This option prohibits the use of bitwise operators such as ^ (XOR), | (OR) and others. Bitwise operators are very rare in JavaScript programs and quite often & is simply a mistyped &&.

### camelcase
* This option allows you to force all variable names to use either camelCase style or UPPER_CASE with underscores.

### curly
* This option requires you to always put curly braces around blocks in loops and conditionals. JavaScript allows you to omit curly braces when the block consists of only one statement, for example:

```
while (day)
  shuffle();
```
* However, in some circumstances, it can lead to bugs (you'd think that sleep() is a part of the loop while in reality it is not):

```
while (day)
  shuffle();
  sleep();
```

### eqeqeq
* This options prohibits the use of == and != in favor of === and !==. The former try to coerce values before comparing them which can lead to some unexpected results. The latter don't do any coercion so they are generally safer. If you would like to learn more about type coercion in JavaScript, we recommend Truth, Equality and JavaScript by Angus Croll.

### es3
* This option tells JSHint that your code needs to adhere to ECMAScript 3 specification. Use this option if you need your program to be executable in older browsers—such as Internet Explorer 6/7/8/9—and other legacy JavaScript environments.

### forin
* This option requires all for in loops to filter object's items. The for in statement allows for looping through the names of all of the properties of an object including those inherited throught the prototype chain. This behavior can lead to unexpected items in your object so it is generally safer to always filter inherited properties out as shown in the example:

```
for (key in obj) {
  if (obj.hasOwnProperty(key)) {
    // We are sure that obj[key] belongs to the object and was not inherited.
  }
}
```
* For more in-depth understanding of for in loops in JavaScript, read Exploring JavaScript for-in loops by Angus Croll.

### freeze
* This options prohibits overwriting prototypes of native objects such as Array, Date and so on.

```
/* jshint freeze:true */
Array.prototype.count = function (value) { return 4; };
// -> Warning: Extending prototype of native object: 'Array'.
```

### immed
* This option prohibits the use of immediate function invocations without wrapping them in parentheses. Wrapping parentheses assists readers of your code in understanding that the expression is the result of a function, and not the function itself.

### indent
* This option sets a specific tab width for your code.

### latedef
* This option prohibits the use of a variable before it was defined. JavaScript has function scope only and, in addition to that, all variables are always moved—or hoisted— to the top of the function. This behavior can lead to some very nasty bugs and that's why it is safer to always use variable only after they have been explicitly defined.

* Setting this option to "nofunc" will allow function declarations to be ignored.

* For more in-depth understanding of scoping and hoisting in JavaScript, read JavaScript Scoping and Hoisting by Ben Cherry.

### newcap
* This option requires you to capitalize names of constructor functions. Capitalizing functions that are intended to be used with new operator is just a convention that helps programmers to visually distinguish constructor functions from other types of functions to help spot mistakes when using this.

* Not doing so won't break your code in any browsers or environments but it will be a bit harder to figure out—by reading the code—if the function was supposed to be used with or without new. And this is important because when the function that was intended to be used with new is used without it, this will point to the global object instead of a new object.

### noarg
* This option prohibits the use of arguments.caller and arguments.callee. Both .caller and .callee make quite a few optimizations impossible so they were deprecated in future versions of JavaScript. In fact, ECMAScript 5 forbids the use of arguments.callee in strict mode.

### noempty
* This option warns when you have an empty block in your code. JSLint was originally warning for all empty blocks and we simply made it optional. There were no studies reporting that empty blocks in JavaScript break your code in any way.

### nonbsp
* This option warns about "non-breaking whitespace" characters. These characters can be entered with option-space on Mac computers and have a potential of breaking non-UTF8 web pages.

### nonew
* This option prohibits the use of constructor functions for side-effects. Some people like to call constructor functions without assigning its result to any variable:

```
new MyConstructor();
```
* There is no advantage in this approach over simply calling MyConstructor since the object that the operator new creates isn't used anywhere so you should generally avoid constructors like this one.

### plusplus
* This option prohibits the use of unary increment and decrement operators. Some people think that ++ and -- reduces the quality of their coding styles and there are programming languages—such as Python—that go completely without these operators.

### quotmark
* This option enforces the consistency of quotation marks used throughout your code. It accepts three values: true if you don't want to enforce one particular style but want some consistency, "single" if you want to allow only single quotes and "double" if you want to allow only double quotes.

### undef
* This option prohibits the use of explicitly undeclared variables. This option is very useful for spotting leaking and mistyped variables.

```
/*jshint undef:true */

function test() {
  var myVar = 'Hello, World';
  console.log(myvar); // Oops, typoed here. JSHint with undef will complain
}
```
* If your variable is defined in another file, you can use /*global ... */ directive to tell JSHint about it.

### unused

* This option warns when you define and never use your variables. It is very useful for general code cleanup, especially when used in addition to undef.

```
/*jshint unused:true */

function test(a, b) {
  var c, d = 2;

  return a + d;
}

test(1, 2);

// Line 3: 'b' was defined but never used.
// Line 4: 'c' was defined but never used.
```
* In addition to that, this option will warn you about unused global variables declared via /*global ... */ directive.

* This can be set to vars to only check for variables, not function parameters, or strict to check all variables and parameters. The default (true) behavior is to allow unused parameters that are followed by a used parameter.

### strict
* This option requires all functions to run in ECMAScript 5's strict mode. Strict mode is a way to opt in to a restricted variant of JavaScript. Strict mode eliminates some JavaScript pitfalls that didn't cause errors by changing them to produce errors. It also fixes mistakes that made it difficult for the JavaScript engines to perform certain optimizations.

* Note: This option enables strict mode for function scope only. It prohibits the global scoped strict mode because it might break third-party widgets on your page. If you really want to use global strict mode, see the globalstrict option.

### maxparams
* This option lets you set the max number of formal parameters allowed per function:

```
/*jshint maxparams:3 */

function login(request, onSuccess) {
  // ...
}

// JSHint: Too many parameters per function (4).
function logout(request, isManual, whereAmI, onSuccess) {
  // ...
}
```

### maxdepth
* This option lets you control how nested do you want your blocks to be:

```
/*jshint maxdepth:2 */

function main(meaning) {
  var day = true;

  if (meaning === 42) {
    while (day) {
      shuffle();

      if (tired) { // JSHint: Blocks are nested too deeply (3).
          sleep();
      }
    }
  }
}
```

### maxstatements
* This option lets you set the max number of statements allowed per function:

```
/*jshint maxstatements:4 */

function main() {
  var i = 0;
  var j = 0;

  // Function declarations count as one statement. Their bodies
  // don't get taken into account for the outer function.
  function inner() {
    var i2 = 1;
    var j2 = 1;

    return i2 + j2;
  }

  j = i + j;
  return j; // JSHint: Too many statements per function. (5)
}
```

### maxcomplexity
* This option lets you control cyclomatic complexity throughout your code. Cyclomatic complexity measures the number of linearly independent paths through a program's source code. Read more about cyclomatic complexity on Wikipedia.

### maxlen
* This option lets you set the maximum length of a line.


## Relaxing options
* When set to true, these options will make JSHint produce less warnings about your code.

### asi
* This option suppresses warnings about missing semicolons. There is a lot of FUD about semicolon spread by quite a few people in the community. The common myths are that semicolons are required all the time (they are not) and that they are unreliable. JavaScript has rules about semicolons which are followed by all browsers so it is up to you to decide whether you should or should not use semicolons in your code.
* For more information about semicolons in JavaScript read An Open Letter to JavaScript Leaders Regarding Semicolons by Isaac Schlueter and JavaScript Semicolon Insertion.

### boss
* This option suppresses warnings about the use of assignments in cases where comparisons are expected. More often than not, code like if (a = 10) {} is a typo. However, it can be useful in cases like this one:
* ```for (var i = 0, person; person = people[i]; i++) {} ```
* You can silence this error on a per-use basis by surrounding the assignment with parenthesis, such as:
* ```for (var i = 0, person; (person = people[i]); i++) {}```

### debug
* This option suppresses warnings about the debugger statements in your code.

### eqnull
* This option suppresses warnings about == null comparisons. Such comparisons are often useful when you want to check if a variable is null or undefined.

### esnext
* This option tells JSHint that your code uses ECMAScript 6 specific syntax. Note that these features are not finalized yet and not all browsers implement them.
* More info:
 * Draft Specification for ES.next (ECMA-262 Ed. 6)

### evil
* This option suppresses warnings about the use of eval. The use of eval is discouraged because it can make your code vulnerable to various injection attacks and it makes it hard for JavaScript interpreter to do certain optimizations.

### expr
* This option suppresses warnings about the use of expressions where normally you would expect to see assignments or function calls. Most of the time, such code is a typo. However, it is not forbidden by the spec and that's why this warning is optional.

### funcscope
* This option suppresses warnings about declaring variables inside of control structures while accessing them later from the outside. Even though JavaScript has only two real scopes—global and function—such practice leads to confusion among people new to the language and hard-to-debug bugs. This is why, by default, JSHint warns about variables that are used outside of their intended scope.

```
function test() {
  if (true) {
    var x = 0;
  }

  x += 1; // Default: 'x' used out of scope.
            // No warning when funcscope:true
}
```

### globalstrict
* This option suppresses warnings about the use of global strict mode. Global strict mode can break third-party widgets so it is not recommended.
* For more info about strict mode see the strict option.

### iterator
* This option suppresses warnings about the __iterator__ property. This property is not supported by all browsers so use it carefully.

### lastsemic
* This option suppresses warnings about missing semicolons, but only when the semicolon is omitted for the last statement in a one-line block:
 * ```var name = (function() { return 'Anton' }());```
* This is a very niche use case that is useful only when you use automatic JavaScript code generators.

### laxbreak
* This option suppresses most of the warnings about possibly unsafe line breakings in your code. It doesn't suppress warnings about comma-first coding style. To suppress those you have to use laxcomma (see below).

### laxcomma
* This option suppresses warnings about comma-first coding style:

```
var obj = {
    name: 'Anton'
  , handle: 'valueof'
  , role: 'SW Engineer'
};
```

### loopfunc
* This option suppresses warnings about functions inside of loops. Defining functions inside of loops can lead to bugs such as this one:

```
var nums = [];

for (var i = 0; i < 10; i++) {
  nums[i] = function (j) {
    return i + j;
  };
}

nums[0](2); // Prints 12 instead of 2
```
* To fix the code above you need to copy the value of i:
```
var nums = [];

for (var i = 0; i < 10; i++) {
  (function (i) {
    nums[i] = function (j) {
        return i + j;
    };
  }(i));
}
```
### maxerr
* This options allows you to set the maximum amount of warnings JSHint will produce before giving up. Default is 50.

### moz
* This options tells JSHint that your code uses Mozilla JavaScript extensions. Unless you develop specifically for the Firefox web browser you don't need this option.
* More info:
 * New in JavaScript 1.7

### multistr
* This option suppresses warnings about multi-line strings. Multi-line strings can be dangerous in JavaScript because all hell breaks loose if you accidentally put a whitespace in between the escape character (\) and a new line.
* Note that even though this option allows correct multi-line strings, it still warns about multi-line strings without escape characters or with anything in between the escape character and a whitespace.
```
/*jshint multistr:true */

var text = "Hello\
World"; // All good.

text = "Hello
World"; // Warning, no escape character.

text = "Hello\
World"; // Warning, there is a space after \
```

### notypeof
* This option suppresses warnings about invalid typeof operator values. This operator has only a limited set of possible return values. By default, JSHint warns when you compare its result with an invalid value which often can be a typo.

```
// 'fuction' instead of 'function'
if (typeof a == "fuction") { // Invalid typeof value 'fuction'
  /* ... */
}
```
* Do not use this option unless you're absolutely sure you don't want these checks.

### proto
* This option suppresses warnings about the __proto__ property.

### scripturl
* This option suppresses warnings about the use of script-targeted URLs—such as javascript:....

### shadow
* This option suppresses warnings about variable shadowing i.e. declaring a variable that had been already declared somewhere in the outer scope.

### sub
* This option suppresses warnings about using [] notation when it can be expressed in dot notation: person['name'] vs. person.name.

### supernew
* This option suppresses warnings about "weird" constructions like new function () { ... } and new Object;. Such constructions are sometimes used to produce singletons in JavaScript:
```
var singleton = new function() {
  var privateVar;

  this.publicMethod  = function () {}
  this.publicMethod2 = function () {}
};
```

### validthis
* This option suppresses warnings about possible strict violations when the code is running in strict mode and you use this in a non-constructor function. You should use this option—in a function scope only—when you are positive that your use of this is valid in the strict mode (for example, if you call your function using Function.call).
* Note: This option can be used only inside of a function scope. JSHint will fail with an error if you will try to set this option globally.

### noyield# JSHint Options

* This is a complete list of all configuration options accepted by JSHint. If you see something missing, you should either file a bug or email me.

## Enforcing options

* When set to true, these options will make JSHint produce more warnings about your code.

### bitwise
* This option prohibits the use of bitwise operators such as ^ (XOR), | (OR) and others. Bitwise operators are very rare in JavaScript programs and quite often & is simply a mistyped &&.

### camelcase
* This option allows you to force all variable names to use either camelCase style or UPPER_CASE with underscores.

### curly
* This option requires you to always put curly braces around blocks in loops and conditionals. JavaScript allows you to omit curly braces when the block consists of only one statement, for example:

```
while (day)
  shuffle();
```
* However, in some circumstances, it can lead to bugs (you'd think that sleep() is a part of the loop while in reality it is not):

```
while (day)
  shuffle();
  sleep();
```

### eqeqeq
* This options prohibits the use of == and != in favor of === and !==. The former try to coerce values before comparing them which can lead to some unexpected results. The latter don't do any coercion so they are generally safer. If you would like to learn more about type coercion in JavaScript, we recommend Truth, Equality and JavaScript by Angus Croll.

### es3
* This option tells JSHint that your code needs to adhere to ECMAScript 3 specification. Use this option if you need your program to be executable in older browsers—such as Internet Explorer 6/7/8/9—and other legacy JavaScript environments.

### forin
* This option requires all for in loops to filter object's items. The for in statement allows for looping through the names of all of the properties of an object including those inherited throught the prototype chain. This behavior can lead to unexpected items in your object so it is generally safer to always filter inherited properties out as shown in the example:

```
for (key in obj) {
  if (obj.hasOwnProperty(key)) {
    // We are sure that obj[key] belongs to the object and was not inherited.
  }
}
```
* For more in-depth understanding of for in loops in JavaScript, read Exploring JavaScript for-in loops by Angus Croll.

### freeze
* This options prohibits overwriting prototypes of native objects such as Array, Date and so on.

```
/* jshint freeze:true */
Array.prototype.count = function (value) { return 4; };
// -> Warning: Extending prototype of native object: 'Array'.
```

### immed
* This option prohibits the use of immediate function invocations without wrapping them in parentheses. Wrapping parentheses assists readers of your code in understanding that the expression is the result of a function, and not the function itself.

### indent
* This option sets a specific tab width for your code.

### latedef
* This option prohibits the use of a variable before it was defined. JavaScript has function scope only and, in addition to that, all variables are always moved—or hoisted— to the top of the function. This behavior can lead to some very nasty bugs and that's why it is safer to always use variable only after they have been explicitly defined.

* Setting this option to "nofunc" will allow function declarations to be ignored.

* For more in-depth understanding of scoping and hoisting in JavaScript, read JavaScript Scoping and Hoisting by Ben Cherry.

### newcap
* This option requires you to capitalize names of constructor functions. Capitalizing functions that are intended to be used with new operator is just a convention that helps programmers to visually distinguish constructor functions from other types of functions to help spot mistakes when using this.

* Not doing so won't break your code in any browsers or environments but it will be a bit harder to figure out—by reading the code—if the function was supposed to be used with or without new. And this is important because when the function that was intended to be used with new is used without it, this will point to the global object instead of a new object.

### noarg
* This option prohibits the use of arguments.caller and arguments.callee. Both .caller and .callee make quite a few optimizations impossible so they were deprecated in future versions of JavaScript. In fact, ECMAScript 5 forbids the use of arguments.callee in strict mode.

### noempty
* This option warns when you have an empty block in your code. JSLint was originally warning for all empty blocks and we simply made it optional. There were no studies reporting that empty blocks in JavaScript break your code in any way.

### nonbsp
* This option warns about "non-breaking whitespace" characters. These characters can be entered with option-space on Mac computers and have a potential of breaking non-UTF8 web pages.

### nonew
* This option prohibits the use of constructor functions for side-effects. Some people like to call constructor functions without assigning its result to any variable:

```
new MyConstructor();
```
* There is no advantage in this approach over simply calling MyConstructor since the object that the operator new creates isn't used anywhere so you should generally avoid constructors like this one.

### plusplus
* This option prohibits the use of unary increment and decrement operators. Some people think that ++ and -- reduces the quality of their coding styles and there are programming languages—such as Python—that go completely without these operators.

### quotmark
* This option enforces the consistency of quotation marks used throughout your code. It accepts three values: true if you don't want to enforce one particular style but want some consistency, "single" if you want to allow only single quotes and "double" if you want to allow only double quotes.

### undef
* This option prohibits the use of explicitly undeclared variables. This option is very useful for spotting leaking and mistyped variables.

```
/*jshint undef:true */

function test() {
  var myVar = 'Hello, World';
  console.log(myvar); // Oops, typoed here. JSHint with undef will complain
}
```
* If your variable is defined in another file, you can use /*global ... */ directive to tell JSHint about it.

### unused

* This option warns when you define and never use your variables. It is very useful for general code cleanup, especially when used in addition to undef.

```
/*jshint unused:true */

function test(a, b) {
  var c, d = 2;

  return a + d;
}

test(1, 2);

// Line 3: 'b' was defined but never used.
// Line 4: 'c' was defined but never used.
```
* In addition to that, this option will warn you about unused global variables declared via /*global ... */ directive.

* This can be set to vars to only check for variables, not function parameters, or strict to check all variables and parameters. The default (true) behavior is to allow unused parameters that are followed by a used parameter.

### strict
* This option requires all functions to run in ECMAScript 5's strict mode. Strict mode is a way to opt in to a restricted variant of JavaScript. Strict mode eliminates some JavaScript pitfalls that didn't cause errors by changing them to produce errors. It also fixes mistakes that made it difficult for the JavaScript engines to perform certain optimizations.

* Note: This option enables strict mode for function scope only. It prohibits the global scoped strict mode because it might break third-party widgets on your page. If you really want to use global strict mode, see the globalstrict option.

### maxparams
* This option lets you set the max number of formal parameters allowed per function:

```
/*jshint maxparams:3 */

function login(request, onSuccess) {
  // ...
}

// JSHint: Too many parameters per function (4).
function logout(request, isManual, whereAmI, onSuccess) {
  // ...
}
```

### maxdepth
* This option lets you control how nested do you want your blocks to be:

```
/*jshint maxdepth:2 */

function main(meaning) {
  var day = true;

  if (meaning === 42) {
    while (day) {
      shuffle();

      if (tired) { // JSHint: Blocks are nested too deeply (3).
          sleep();
      }
    }
  }
}
```

### maxstatements
* This option lets you set the max number of statements allowed per function:

```
/*jshint maxstatements:4 */

function main() {
  var i = 0;
  var j = 0;

  // Function declarations count as one statement. Their bodies
  // don't get taken into account for the outer function.
  function inner() {
    var i2 = 1;
    var j2 = 1;

    return i2 + j2;
  }

  j = i + j;
  return j; // JSHint: Too many statements per function. (5)
}
```

### maxcomplexity
* This option lets you control cyclomatic complexity throughout your code. Cyclomatic complexity measures the number of linearly independent paths through a program's source code. Read more about cyclomatic complexity on Wikipedia.

### maxlen
* This option lets you set the maximum length of a line.


## Relaxing options
* When set to true, these options will make JSHint produce less warnings about your code.

### asi
* This option suppresses warnings about missing semicolons. There is a lot of FUD about semicolon spread by quite a few people in the community. The common myths are that semicolons are required all the time (they are not) and that they are unreliable. JavaScript has rules about semicolons which are followed by all browsers so it is up to you to decide whether you should or should not use semicolons in your code.
* For more information about semicolons in JavaScript read An Open Letter to JavaScript Leaders Regarding Semicolons by Isaac Schlueter and JavaScript Semicolon Insertion.

### boss
* This option suppresses warnings about the use of assignments in cases where comparisons are expected. More often than not, code like if (a = 10) {} is a typo. However, it can be useful in cases like this one:
* ```for (var i = 0, person; person = people[i]; i++) {} ```
* You can silence this error on a per-use basis by surrounding the assignment with parenthesis, such as:
* ```for (var i = 0, person; (person = people[i]); i++) {}```

### debug
* This option suppresses warnings about the debugger statements in your code.

### eqnull
* This option suppresses warnings about == null comparisons. Such comparisons are often useful when you want to check if a variable is null or undefined.

### esnext
* This option tells JSHint that your code uses ECMAScript 6 specific syntax. Note that these features are not finalized yet and not all browsers implement them.
* More info:
 * Draft Specification for ES.next (ECMA-262 Ed. 6)

### evil
* This option suppresses warnings about the use of eval. The use of eval is discouraged because it can make your code vulnerable to various injection attacks and it makes it hard for JavaScript interpreter to do certain optimizations.

### expr
* This option suppresses warnings about the use of expressions where normally you would expect to see assignments or function calls. Most of the time, such code is a typo. However, it is not forbidden by the spec and that's why this warning is optional.

### funcscope
* This option suppresses warnings about declaring variables inside of control structures while accessing them later from the outside. Even though JavaScript has only two real scopes—global and function—such practice leads to confusion among people new to the language and hard-to-debug bugs. This is why, by default, JSHint warns about variables that are used outside of their intended scope.

```
function test() {
  if (true) {
    var x = 0;
  }

  x += 1; // Default: 'x' used out of scope.
            // No warning when funcscope:true
}
```

### globalstrict
* This option suppresses warnings about the use of global strict mode. Global strict mode can break third-party widgets so it is not recommended.
* For more info about strict mode see the strict option.

### iterator
* This option suppresses warnings about the __iterator__ property. This property is not supported by all browsers so use it carefully.

### lastsemic
* This option suppresses warnings about missing semicolons, but only when the semicolon is omitted for the last statement in a one-line block:
 * ```var name = (function() { return 'Anton' }());```
* This is a very niche use case that is useful only when you use automatic JavaScript code generators.

### laxbreak
* This option suppresses most of the warnings about possibly unsafe line breakings in your code. It doesn't suppress warnings about comma-first coding style. To suppress those you have to use laxcomma (see below).

### laxcomma
* This option suppresses warnings about comma-first coding style:

```
var obj = {
    name: 'Anton'
  , handle: 'valueof'
  , role: 'SW Engineer'
};
```

### loopfunc
* This option suppresses warnings about functions inside of loops. Defining functions inside of loops can lead to bugs such as this one:

```
var nums = [];

for (var i = 0; i < 10; i++) {
  nums[i] = function (j) {
    return i + j;
  };
}

nums[0](2); // Prints 12 instead of 2
```
* To fix the code above you need to copy the value of i:
```
var nums = [];

for (var i = 0; i < 10; i++) {
  (function (i) {
    nums[i] = function (j) {
        return i + j;
    };
  }(i));
}
```
### maxerr
* This options allows you to set the maximum amount of warnings JSHint will produce before giving up. Default is 50.

### moz
* This options tells JSHint that your code uses Mozilla JavaScript extensions. Unless you develop specifically for the Firefox web browser you don't need this option.
* More info:
 * New in JavaScript 1.7

### multistr
* This option suppresses warnings about multi-line strings. Multi-line strings can be dangerous in JavaScript because all hell breaks loose if you accidentally put a whitespace in between the escape character (\) and a new line.
* Note that even though this option allows correct multi-line strings, it still warns about multi-line strings without escape characters or with anything in between the escape character and a whitespace.
```
/*jshint multistr:true */

var text = "Hello\
World"; // All good.

text = "Hello
World"; // Warning, no escape character.

text = "Hello\
World"; // Warning, there is a space after \
```

### notypeof
* This option suppresses warnings about invalid typeof operator values. This operator has only a limited set of possible return values. By default, JSHint warns when you compare its result with an invalid value which often can be a typo.

```
// 'fuction' instead of 'function'
if (typeof a == "fuction") { // Invalid typeof value 'fuction'
  /* ... */
}
```
* Do not use this option unless you're absolutely sure you don't want these checks.

### proto
* This option suppresses warnings about the __proto__ property.

### scripturl
* This option suppresses warnings about the use of script-targeted URLs—such as javascript:....

### shadow
* This option suppresses warnings about variable shadowing i.e. declaring a variable that had been already declared somewhere in the outer scope.

### sub
* This option suppresses warnings about using [] notation when it can be expressed in dot notation: person['name'] vs. person.name.

### supernew
* This option suppresses warnings about "weird" constructions like new function () { ... } and new Object;. Such constructions are sometimes used to produce singletons in JavaScript:
```
var singleton = new function() {
  var privateVar;

  this.publicMethod  = function () {}
  this.publicMethod2 = function () {}
};
```

### validthis
* This option suppresses warnings about possible strict violations when the code is running in strict mode and you use this in a non-constructor function. You should use this option—in a function scope only—when you are positive that your use of this is valid in the strict mode (for example, if you call your function using Function.call).
* Note: This option can be used only inside of a function scope. JSHint will fail with an error if you will try to set this option globally.

### noyield# JSHint Options

* This is a complete list of all configuration options accepted by JSHint. If you see something missing, you should either file a bug or email me.

## Enforcing options

* When set to true, these options will make JSHint produce more warnings about your code.

### bitwise
* This option prohibits the use of bitwise operators such as ^ (XOR), | (OR) and others. Bitwise operators are very rare in JavaScript programs and quite often & is simply a mistyped &&.

### camelcase
* This option allows you to force all variable names to use either camelCase style or UPPER_CASE with underscores.

### curly
* This option requires you to always put curly braces around blocks in loops and conditionals. JavaScript allows you to omit curly braces when the block consists of only one statement, for example:

```
while (day)
  shuffle();
```
* However, in some circumstances, it can lead to bugs (you'd think that sleep() is a part of the loop while in reality it is not):

```
while (day)
  shuffle();
  sleep();
```

### eqeqeq
* This options prohibits the use of == and != in favor of === and !==. The former try to coerce values before comparing them which can lead to some unexpected results. The latter don't do any coercion so they are generally safer. If you would like to learn more about type coercion in JavaScript, we recommend Truth, Equality and JavaScript by Angus Croll.

### es3
* This option tells JSHint that your code needs to adhere to ECMAScript 3 specification. Use this option if you need your program to be executable in older browsers—such as Internet Explorer 6/7/8/9—and other legacy JavaScript environments.

### forin
* This option requires all for in loops to filter object's items. The for in statement allows for looping through the names of all of the properties of an object including those inherited throught the prototype chain. This behavior can lead to unexpected items in your object so it is generally safer to always filter inherited properties out as shown in the example:

```
for (key in obj) {
  if (obj.hasOwnProperty(key)) {
    // We are sure that obj[key] belongs to the object and was not inherited.
  }
}
```
* For more in-depth understanding of for in loops in JavaScript, read Exploring JavaScript for-in loops by Angus Croll.

### freeze
* This options prohibits overwriting prototypes of native objects such as Array, Date and so on.

```
/* jshint freeze:true */
Array.prototype.count = function (value) { return 4; };
// -> Warning: Extending prototype of native object: 'Array'.
```

### immed
* This option prohibits the use of immediate function invocations without wrapping them in parentheses. Wrapping parentheses assists readers of your code in understanding that the expression is the result of a function, and not the function itself.

### indent
* This option sets a specific tab width for your code.

### latedef
* This option prohibits the use of a variable before it was defined. JavaScript has function scope only and, in addition to that, all variables are always moved—or hoisted— to the top of the function. This behavior can lead to some very nasty bugs and that's why it is safer to always use variable only after they have been explicitly defined.

* Setting this option to "nofunc" will allow function declarations to be ignored.

* For more in-depth understanding of scoping and hoisting in JavaScript, read JavaScript Scoping and Hoisting by Ben Cherry.

### newcap
* This option requires you to capitalize names of constructor functions. Capitalizing functions that are intended to be used with new operator is just a convention that helps programmers to visually distinguish constructor functions from other types of functions to help spot mistakes when using this.

* Not doing so won't break your code in any browsers or environments but it will be a bit harder to figure out—by reading the code—if the function was supposed to be used with or without new. And this is important because when the function that was intended to be used with new is used without it, this will point to the global object instead of a new object.

### noarg
* This option prohibits the use of arguments.caller and arguments.callee. Both .caller and .callee make quite a few optimizations impossible so they were deprecated in future versions of JavaScript. In fact, ECMAScript 5 forbids the use of arguments.callee in strict mode.

### noempty
* This option warns when you have an empty block in your code. JSLint was originally warning for all empty blocks and we simply made it optional. There were no studies reporting that empty blocks in JavaScript break your code in any way.

### nonbsp
* This option warns about "non-breaking whitespace" characters. These characters can be entered with option-space on Mac computers and have a potential of breaking non-UTF8 web pages.

### nonew
* This option prohibits the use of constructor functions for side-effects. Some people like to call constructor functions without assigning its result to any variable:

```
new MyConstructor();
```
* There is no advantage in this approach over simply calling MyConstructor since the object that the operator new creates isn't used anywhere so you should generally avoid constructors like this one.

### plusplus
* This option prohibits the use of unary increment and decrement operators. Some people think that ++ and -- reduces the quality of their coding styles and there are programming languages—such as Python—that go completely without these operators.

### quotmark
* This option enforces the consistency of quotation marks used throughout your code. It accepts three values: true if you don't want to enforce one particular style but want some consistency, "single" if you want to allow only single quotes and "double" if you want to allow only double quotes.

### undef
* This option prohibits the use of explicitly undeclared variables. This option is very useful for spotting leaking and mistyped variables.

```
/*jshint undef:true */

function test() {
  var myVar = 'Hello, World';
  console.log(myvar); // Oops, typoed here. JSHint with undef will complain
}
```
* If your variable is defined in another file, you can use /*global ... */ directive to tell JSHint about it.

### unused

* This option warns when you define and never use your variables. It is very useful for general code cleanup, especially when used in addition to undef.

```
/*jshint unused:true */

function test(a, b) {
  var c, d = 2;

  return a + d;
}

test(1, 2);

// Line 3: 'b' was defined but never used.
// Line 4: 'c' was defined but never used.
```
* In addition to that, this option will warn you about unused global variables declared via /*global ... */ directive.

* This can be set to vars to only check for variables, not function parameters, or strict to check all variables and parameters. The default (true) behavior is to allow unused parameters that are followed by a used parameter.

### strict
* This option requires all functions to run in ECMAScript 5's strict mode. Strict mode is a way to opt in to a restricted variant of JavaScript. Strict mode eliminates some JavaScript pitfalls that didn't cause errors by changing them to produce errors. It also fixes mistakes that made it difficult for the JavaScript engines to perform certain optimizations.

* Note: This option enables strict mode for function scope only. It prohibits the global scoped strict mode because it might break third-party widgets on your page. If you really want to use global strict mode, see the globalstrict option.

### maxparams
* This option lets you set the max number of formal parameters allowed per function:

```
/*jshint maxparams:3 */

function login(request, onSuccess) {
  // ...
}

// JSHint: Too many parameters per function (4).
function logout(request, isManual, whereAmI, onSuccess) {
  // ...
}
```

### maxdepth
* This option lets you control how nested do you want your blocks to be:

```
/*jshint maxdepth:2 */

function main(meaning) {
  var day = true;

  if (meaning === 42) {
    while (day) {
      shuffle();

      if (tired) { // JSHint: Blocks are nested too deeply (3).
          sleep();
      }
    }
  }
}
```

### maxstatements
* This option lets you set the max number of statements allowed per function:

```
/*jshint maxstatements:4 */

function main() {
  var i = 0;
  var j = 0;

  // Function declarations count as one statement. Their bodies
  // don't get taken into account for the outer function.
  function inner() {
    var i2 = 1;
    var j2 = 1;

    return i2 + j2;
  }

  j = i + j;
  return j; // JSHint: Too many statements per function. (5)
}
```

### maxcomplexity
* This option lets you control cyclomatic complexity throughout your code. Cyclomatic complexity measures the number of linearly independent paths through a program's source code. Read more about cyclomatic complexity on Wikipedia.

### maxlen
* This option lets you set the maximum length of a line.


## Relaxing options
* When set to true, these options will make JSHint produce less warnings about your code.

### asi
* This option suppresses warnings about missing semicolons. There is a lot of FUD about semicolon spread by quite a few people in the community. The common myths are that semicolons are required all the time (they are not) and that they are unreliable. JavaScript has rules about semicolons which are followed by all browsers so it is up to you to decide whether you should or should not use semicolons in your code.
* For more information about semicolons in JavaScript read An Open Letter to JavaScript Leaders Regarding Semicolons by Isaac Schlueter and JavaScript Semicolon Insertion.

### boss
* This option suppresses warnings about the use of assignments in cases where comparisons are expected. More often than not, code like if (a = 10) {} is a typo. However, it can be useful in cases like this one:
* ```for (var i = 0, person; person = people[i]; i++) {} ```
* You can silence this error on a per-use basis by surrounding the assignment with parenthesis, such as:
* ```for (var i = 0, person; (person = people[i]); i++) {}```

### debug
* This option suppresses warnings about the debugger statements in your code.

### eqnull
* This option suppresses warnings about == null comparisons. Such comparisons are often useful when you want to check if a variable is null or undefined.

### esnext
* This option tells JSHint that your code uses ECMAScript 6 specific syntax. Note that these features are not finalized yet and not all browsers implement them.
* More info:
 * Draft Specification for ES.next (ECMA-262 Ed. 6)

### evil
* This option suppresses warnings about the use of eval. The use of eval is discouraged because it can make your code vulnerable to various injection attacks and it makes it hard for JavaScript interpreter to do certain optimizations.

### expr
* This option suppresses warnings about the use of expressions where normally you would expect to see assignments or function calls. Most of the time, such code is a typo. However, it is not forbidden by the spec and that's why this warning is optional.

### funcscope
* This option suppresses warnings about declaring variables inside of control structures while accessing them later from the outside. Even though JavaScript has only two real scopes—global and function—such practice leads to confusion among people new to the language and hard-to-debug bugs. This is why, by default, JSHint warns about variables that are used outside of their intended scope.

```
function test() {
  if (true) {
    var x = 0;
  }

  x += 1; // Default: 'x' used out of scope.
            // No warning when funcscope:true
}
```

### globalstrict
* This option suppresses warnings about the use of global strict mode. Global strict mode can break third-party widgets so it is not recommended.
* For more info about strict mode see the strict option.

### iterator
* This option suppresses warnings about the __iterator__ property. This property is not supported by all browsers so use it carefully.

### lastsemic
* This option suppresses warnings about missing semicolons, but only when the semicolon is omitted for the last statement in a one-line block:
 * ```var name = (function() { return 'Anton' }());```
* This is a very niche use case that is useful only when you use automatic JavaScript code generators.

### laxbreak
* This option suppresses most of the warnings about possibly unsafe line breakings in your code. It doesn't suppress warnings about comma-first coding style. To suppress those you have to use laxcomma (see below).

### laxcomma
* This option suppresses warnings about comma-first coding style:

```
var obj = {
    name: 'Anton'
  , handle: 'valueof'
  , role: 'SW Engineer'
};
```

### loopfunc
* This option suppresses warnings about functions inside of loops. Defining functions inside of loops can lead to bugs such as this one:

```
var nums = [];

for (var i = 0; i < 10; i++) {
  nums[i] = function (j) {
    return i + j;
  };
}

nums[0](2); // Prints 12 instead of 2
```
* To fix the code above you need to copy the value of i:
```
var nums = [];

for (var i = 0; i < 10; i++) {
  (function (i) {
    nums[i] = function (j) {
        return i + j;
    };
  }(i));
}
```
### maxerr
* This options allows you to set the maximum amount of warnings JSHint will produce before giving up. Default is 50.

### moz
* This options tells JSHint that your code uses Mozilla JavaScript extensions. Unless you develop specifically for the Firefox web browser you don't need this option.
* More info:
 * New in JavaScript 1.7

### multistr
* This option suppresses warnings about multi-line strings. Multi-line strings can be dangerous in JavaScript because all hell breaks loose if you accidentally put a whitespace in between the escape character (\) and a new line.
* Note that even though this option allows correct multi-line strings, it still warns about multi-line strings without escape characters or with anything in between the escape character and a whitespace.
```
/*jshint multistr:true */

var text = "Hello\
World"; // All good.

text = "Hello
World"; // Warning, no escape character.

text = "Hello\
World"; // Warning, there is a space after \
```

### notypeof
* This option suppresses warnings about invalid typeof operator values. This operator has only a limited set of possible return values. By default, JSHint warns when you compare its result with an invalid value which often can be a typo.

```
// 'fuction' instead of 'function'
if (typeof a == "fuction") { // Invalid typeof value 'fuction'
  /* ... */
}
```
* Do not use this option unless you're absolutely sure you don't want these checks.

### proto
* This option suppresses warnings about the __proto__ property.

### scripturl
* This option suppresses warnings about the use of script-targeted URLs—such as javascript:....

### shadow
* This option suppresses warnings about variable shadowing i.e. declaring a variable that had been already declared somewhere in the outer scope.

### sub
* This option suppresses warnings about using [] notation when it can be expressed in dot notation: person['name'] vs. person.name.

### supernew
* This option suppresses warnings about "weird" constructions like new function () { ... } and new Object;. Such constructions are sometimes used to produce singletons in JavaScript:
```
var singleton = new function() {
  var privateVar;

  this.publicMethod  = function () {}
  this.publicMethod2 = function () {}
};
```

### validthis
* This option suppresses warnings about possible strict violations when the code is running in strict mode and you use this in a non-constructor function. You should use this option—in a function scope only—when you are positive that your use of this is valid in the strict mode (for example, if you call your function using Function.call).
* Note: This option can be used only inside of a function scope. JSHint will fail with an error if you will try to set this option globally.

### noyield# JSHint Options

* This is a complete list of all configuration options accepted by JSHint. If you see something missing, you should either file a bug or email me.

## Enforcing options

* When set to true, these options will make JSHint produce more warnings about your code.

### bitwise
* This option prohibits the use of bitwise operators such as ^ (XOR), | (OR) and others. Bitwise operators are very rare in JavaScript programs and quite often & is simply a mistyped &&.

### camelcase
* This option allows you to force all variable names to use either camelCase style or UPPER_CASE with underscores.

### curly
* This option requires you to always put curly braces around blocks in loops and conditionals. JavaScript allows you to omit curly braces when the block consists of only one statement, for example:

```
while (day)
  shuffle();
```
* However, in some circumstances, it can lead to bugs (you'd think that sleep() is a part of the loop while in reality it is not):

```
while (day)
  shuffle();
  sleep();
```

### eqeqeq
* This options prohibits the use of == and != in favor of === and !==. The former try to coerce values before comparing them which can lead to some unexpected results. The latter don't do any coercion so they are generally safer. If you would like to learn more about type coercion in JavaScript, we recommend Truth, Equality and JavaScript by Angus Croll.

### es3
* This option tells JSHint that your code needs to adhere to ECMAScript 3 specification. Use this option if you need your program to be executable in older browsers—such as Internet Explorer 6/7/8/9—and other legacy JavaScript environments.

### forin
* This option requires all for in loops to filter object's items. The for in statement allows for looping through the names of all of the properties of an object including those inherited throught the prototype chain. This behavior can lead to unexpected items in your object so it is generally safer to always filter inherited properties out as shown in the example:

```
for (key in obj) {
  if (obj.hasOwnProperty(key)) {
    // We are sure that obj[key] belongs to the object and was not inherited.
  }
}
```
* For more in-depth understanding of for in loops in JavaScript, read Exploring JavaScript for-in loops by Angus Croll.

### freeze
* This options prohibits overwriting prototypes of native objects such as Array, Date and so on.

```
/* jshint freeze:true */
Array.prototype.count = function (value) { return 4; };
// -> Warning: Extending prototype of native object: 'Array'.
```

### immed
* This option prohibits the use of immediate function invocations without wrapping them in parentheses. Wrapping parentheses assists readers of your code in understanding that the expression is the result of a function, and not the function itself.

### indent
* This option sets a specific tab width for your code.

### latedef
* This option prohibits the use of a variable before it was defined. JavaScript has function scope only and, in addition to that, all variables are always moved—or hoisted— to the top of the function. This behavior can lead to some very nasty bugs and that's why it is safer to always use variable only after they have been explicitly defined.

* Setting this option to "nofunc" will allow function declarations to be ignored.

* For more in-depth understanding of scoping and hoisting in JavaScript, read JavaScript Scoping and Hoisting by Ben Cherry.

### newcap
* This option requires you to capitalize names of constructor functions. Capitalizing functions that are intended to be used with new operator is just a convention that helps programmers to visually distinguish constructor functions from other types of functions to help spot mistakes when using this.

* Not doing so won't break your code in any browsers or environments but it will be a bit harder to figure out—by reading the code—if the function was supposed to be used with or without new. And this is important because when the function that was intended to be used with new is used without it, this will point to the global object instead of a new object.

### noarg
* This option prohibits the use of arguments.caller and arguments.callee. Both .caller and .callee make quite a few optimizations impossible so they were deprecated in future versions of JavaScript. In fact, ECMAScript 5 forbids the use of arguments.callee in strict mode.

### noempty
* This option warns when you have an empty block in your code. JSLint was originally warning for all empty blocks and we simply made it optional. There were no studies reporting that empty blocks in JavaScript break your code in any way.

### nonbsp
* This option warns about "non-breaking whitespace" characters. These characters can be entered with option-space on Mac computers and have a potential of breaking non-UTF8 web pages.

### nonew
* This option prohibits the use of constructor functions for side-effects. Some people like to call constructor functions without assigning its result to any variable:

```
new MyConstructor();
```
* There is no advantage in this approach over simply calling MyConstructor since the object that the operator new creates isn't used anywhere so you should generally avoid constructors like this one.

### plusplus
* This option prohibits the use of unary increment and decrement operators. Some people think that ++ and -- reduces the quality of their coding styles and there are programming languages—such as Python—that go completely without these operators.

### quotmark
* This option enforces the consistency of quotation marks used throughout your code. It accepts three values: true if you don't want to enforce one particular style but want some consistency, "single" if you want to allow only single quotes and "double" if you want to allow only double quotes.

### undef
* This option prohibits the use of explicitly undeclared variables. This option is very useful for spotting leaking and mistyped variables.

```
/*jshint undef:true */

function test() {
  var myVar = 'Hello, World';
  console.log(myvar); // Oops, typoed here. JSHint with undef will complain
}
```
* If your variable is defined in another file, you can use /*global ... */ directive to tell JSHint about it.

### unused

* This option warns when you define and never use your variables. It is very useful for general code cleanup, especially when used in addition to undef.

```
/*jshint unused:true */

function test(a, b) {
  var c, d = 2;

  return a + d;
}

test(1, 2);

// Line 3: 'b' was defined but never used.
// Line 4: 'c' was defined but never used.
```
* In addition to that, this option will warn you about unused global variables declared via /*global ... */ directive.

* This can be set to vars to only check for variables, not function parameters, or strict to check all variables and parameters. The default (true) behavior is to allow unused parameters that are followed by a used parameter.

### strict
* This option requires all functions to run in ECMAScript 5's strict mode. Strict mode is a way to opt in to a restricted variant of JavaScript. Strict mode eliminates some JavaScript pitfalls that didn't cause errors by changing them to produce errors. It also fixes mistakes that made it difficult for the JavaScript engines to perform certain optimizations.

* Note: This option enables strict mode for function scope only. It prohibits the global scoped strict mode because it might break third-party widgets on your page. If you really want to use global strict mode, see the globalstrict option.

### maxparams
* This option lets you set the max number of formal parameters allowed per function:

```
/*jshint maxparams:3 */

function login(request, onSuccess) {
  // ...
}

// JSHint: Too many parameters per function (4).
function logout(request, isManual, whereAmI, onSuccess) {
  // ...
}
```

### maxdepth
* This option lets you control how nested do you want your blocks to be:

```
/*jshint maxdepth:2 */

function main(meaning) {
  var day = true;

  if (meaning === 42) {
    while (day) {
      shuffle();

      if (tired) { // JSHint: Blocks are nested too deeply (3).
          sleep();
      }
    }
  }
}
```

### maxstatements
* This option lets you set the max number of statements allowed per function:

```
/*jshint maxstatements:4 */

function main() {
  var i = 0;
  var j = 0;

  // Function declarations count as one statement. Their bodies
  // don't get taken into account for the outer function.
  function inner() {
    var i2 = 1;
    var j2 = 1;

    return i2 + j2;
  }

  j = i + j;
  return j; // JSHint: Too many statements per function. (5)
}
```

### maxcomplexity
* This option lets you control cyclomatic complexity throughout your code. Cyclomatic complexity measures the number of linearly independent paths through a program's source code. Read more about cyclomatic complexity on Wikipedia.

### maxlen
* This option lets you set the maximum length of a line.


## Relaxing options
* When set to true, these options will make JSHint produce less warnings about your code.

### asi
* This option suppresses warnings about missing semicolons. There is a lot of FUD about semicolon spread by quite a few people in the community. The common myths are that semicolons are required all the time (they are not) and that they are unreliable. JavaScript has rules about semicolons which are followed by all browsers so it is up to you to decide whether you should or should not use semicolons in your code.
* For more information about semicolons in JavaScript read An Open Letter to JavaScript Leaders Regarding Semicolons by Isaac Schlueter and JavaScript Semicolon Insertion.

### boss
* This option suppresses warnings about the use of assignments in cases where comparisons are expected. More often than not, code like if (a = 10) {} is a typo. However, it can be useful in cases like this one:
* ```for (var i = 0, person; person = people[i]; i++) {} ```
* You can silence this error on a per-use basis by surrounding the assignment with parenthesis, such as:
* ```for (var i = 0, person; (person = people[i]); i++) {}```

### debug
* This option suppresses warnings about the debugger statements in your code.

### eqnull
* This option suppresses warnings about == null comparisons. Such comparisons are often useful when you want to check if a variable is null or undefined.

### esnext
* This option tells JSHint that your code uses ECMAScript 6 specific syntax. Note that these features are not finalized yet and not all browsers implement them.
* More info:
 * Draft Specification for ES.next (ECMA-262 Ed. 6)

### evil
* This option suppresses warnings about the use of eval. The use of eval is discouraged because it can make your code vulnerable to various injection attacks and it makes it hard for JavaScript interpreter to do certain optimizations.

### expr
* This option suppresses warnings about the use of expressions where normally you would expect to see assignments or function calls. Most of the time, such code is a typo. However, it is not forbidden by the spec and that's why this warning is optional.

### funcscope
* This option suppresses warnings about declaring variables inside of control structures while accessing them later from the outside. Even though JavaScript has only two real scopes—global and function—such practice leads to confusion among people new to the language and hard-to-debug bugs. This is why, by default, JSHint warns about variables that are used outside of their intended scope.

```
function test() {
  if (true) {
    var x = 0;
  }

  x += 1; // Default: 'x' used out of scope.
            // No warning when funcscope:true
}
```

### globalstrict
* This option suppresses warnings about the use of global strict mode. Global strict mode can break third-party widgets so it is not recommended.
* For more info about strict mode see the strict option.

### iterator
* This option suppresses warnings about the __iterator__ property. This property is not supported by all browsers so use it carefully.

### lastsemic
* This option suppresses warnings about missing semicolons, but only when the semicolon is omitted for the last statement in a one-line block:
 * ```var name = (function() { return 'Anton' }());```
* This is a very niche use case that is useful only when you use automatic JavaScript code generators.

### laxbreak
* This option suppresses most of the warnings about possibly unsafe line breakings in your code. It doesn't suppress warnings about comma-first coding style. To suppress those you have to use laxcomma (see below).

### laxcomma
* This option suppresses warnings about comma-first coding style:

```
var obj = {
    name: 'Anton'
  , handle: 'valueof'
  , role: 'SW Engineer'
};
```

### loopfunc
* This option suppresses warnings about functions inside of loops. Defining functions inside of loops can lead to bugs such as this one:

```
var nums = [];

for (var i = 0; i < 10; i++) {
  nums[i] = function (j) {
    return i + j;
  };
}

nums[0](2); // Prints 12 instead of 2
```
* To fix the code above you need to copy the value of i:
```
var nums = [];

for (var i = 0; i < 10; i++) {
  (function (i) {
    nums[i] = function (j) {
        return i + j;
    };
  }(i));
}
```
### maxerr
* This options allows you to set the maximum amount of warnings JSHint will produce before giving up. Default is 50.

### moz
* This options tells JSHint that your code uses Mozilla JavaScript extensions. Unless you develop specifically for the Firefox web browser you don't need this option.
* More info:
 * New in JavaScript 1.7

### multistr
* This option suppresses warnings about multi-line strings. Multi-line strings can be dangerous in JavaScript because all hell breaks loose if you accidentally put a whitespace in between the escape character (\) and a new line.
* Note that even though this option allows correct multi-line strings, it still warns about multi-line strings without escape characters or with anything in between the escape character and a whitespace.
```
/*jshint multistr:true */

var text = "Hello\
World"; // All good.

text = "Hello
World"; // Warning, no escape character.

text = "Hello\
World"; // Warning, there is a space after \
```

### notypeof
* This option suppresses warnings about invalid typeof operator values. This operator has only a limited set of possible return values. By default, JSHint warns when you compare its result with an invalid value which often can be a typo.

```
// 'fuction' instead of 'function'
if (typeof a == "fuction") { // Invalid typeof value 'fuction'
  /* ... */
}
```
* Do not use this option unless you're absolutely sure you don't want these checks.

### proto
* This option suppresses warnings about the __proto__ property.

### scripturl
* This option suppresses warnings about the use of script-targeted URLs—such as javascript:....

### shadow
* This option suppresses warnings about variable shadowing i.e. declaring a variable that had been already declared somewhere in the outer scope.

### sub
* This option suppresses warnings about using [] notation when it can be expressed in dot notation: person['name'] vs. person.name.

### supernew
* This option suppresses warnings about "weird" constructions like new function () { ... } and new Object;. Such constructions are sometimes used to produce singletons in JavaScript:
```
var singleton = new function() {
  var privateVar;

  this.publicMethod  = function () {}
  this.publicMethod2 = function () {}
};
```

### validthis
* This option suppresses warnings about possible strict violations when the code is running in strict mode and you use this in a non-constructor function. You should use this option—in a function scope only—when you are positive that your use of this is valid in the strict mode (for example, if you call your function using Function.call).
* Note: This option can be used only inside of a function scope. JSHint will fail with an error if you will try to set this option globally.

### noyieldD about semicolon spread by quite a few people in the community. The common myths are that semicolons are required all the time (they are not) and that they are unreliable. JavaScript has rules about semicolons which are followed by all browsers so it is up to you to decide whether you should or should not use semicolons in your code.
* For more information about semicolons in JavaScript read An Open Letter to JavaScript Leaders Regarding Semicolons by Isaac Schlueter and JavaScript Semicolon Insertion.

### boss
* This option suppresses warnings about the use of assignments in cases where comparisons are expected. More often than not, code like if (a = 10) {} is a typo. However, it can be useful in cases like this one:
* ```for (var i = 0, person; person = people[i]; i++) {} ```
* You can silence this error on a per-use basis by surrounding the assignment with parenthesis, such as:
* ```for (var i = 0, person; (person = people[i]); i++) {}```

### debug
* This option suppresses warnings about the debugger statements in your code.

### eqnull
* This option suppresses warnings about == null comparisons. Such comparisons are often useful when you want to check if a variable is null or undefined.

### esnext
* This option tells JSHint that your code uses ECMAScript 6 specific syntax. Note that these features are not finalized yet and not all browsers implement them.
* More info:
 * Draft Specification for ES.next (ECMA-262 Ed. 6)

### evil
* This option suppresses warnings about the use of eval. The use of eval is discouraged because it can make your code vulnerable to various injection attacks and it makes it hard for JavaScript interpreter to do certain optimizations.

### expr
* This option suppresses warnings about the use of expressions where normally you would expect to see assignments or function calls. Most of the time, such code is a typo. However, it is not forbidden by the spec and that's why this warning is optional.

### funcscope
* This option suppresses warnings about declaring variables inside of control structures while accessing them later from the outside. Even though JavaScript has only two real scopes—global and function—such practice leads to confusion among people new to the language and hard-to-debug bugs. This is why, by default, JSHint warns about variables that are used outside of their intended scope.

```
function test() {
  if (true) {
    var x = 0;
  }

  x += 1; // Default: 'x' used out of scope.
            // No warning when funcscope:true
}
```

### globalstrict
* This option suppresses warnings about the use of global strict mode. Global strict mode can break third-party widgets so it is not recommended.
* For more info about strict mode see the strict option.

### iterator
* This option suppresses warnings about the __iterator__ property. This property is not supported by all browsers so use it carefully.

### lastsemic
* This option suppresses warnings about missing semicolons, but only when the semicolon is omitted for the last statement in a one-line block:
 * ```var name = (function() { return 'Anton' }());```
* This is a very niche use case that is useful only when you use automatic JavaScript code generators.

### laxbreak
* This option suppresses most of the warnings about possibly unsafe line breakings in your code. It doesn't suppress warnings about comma-first coding style. To suppress those you have to use laxcomma (see below).

### laxcomma
* This option suppresses warnings about comma-first coding style:

```
var obj = {
    name: 'Anton'
  , handle: 'valueof'
  , role: 'SW Engineer'
};
```

### loopfunc
* This option suppresses warnings about functions inside of loops. Defining functions inside of loops can lead to bugs such as this one:

```
var nums = [];

for (var i = 0; i < 10; i++) {
  nums[i] = function (j) {
    return i + j;
  };
}

nums[0](2); // Prints 12 instead of 2
```
* To fix the code above you need to copy the value of i:
```
var nums = [];

for (var i = 0; i < 10; i++) {
  (function (i) {
    nums[i] = function (j) {
        return i + j;
    };
  }(i));
}
```
### maxerr
* This options allows you to set the maximum amount of warnings JSHint will produce before giving up. Default is 50.

### moz
* This options tells JSHint that your code uses Mozilla JavaScript extensions. Unless you develop specifically for the Firefox web browser you don't need this option.
* More info:
 * New in JavaScript 1.7

### multistr
* This option suppresses warnings about multi-line strings. Multi-line strings can be dangerous in JavaScript because all hell breaks loose if you accidentally put a whitespace in between the escape character (\) and a new line.
* Note that even though this option allows correct multi-line strings, it still warns about multi-line strings without escape characters or with anything in between the escape character and a whitespace.
```
/*jshint multistr:true */

var text = "Hello\
World"; // All good.

text = "Hello
World"; // Warning, no escape character.

text = "Hello\
World"; // Warning, there is a space after \
```

### notypeof
* This option suppresses warnings about invalid typeof operator values. This operator has only a limited set of possible return values. By default, JSHint warns when you compare its result with an invalid value which often can be a typo.

```
// 'fuction' instead of 'function'
if (typeof a == "fuction") { // Invalid typeof value 'fuction'
  /* ... */
}
```
* Do not use this option unless you're absolutely sure you don't want these checks.

### proto
* This option suppresses warnings about the __proto__ property.

### scripturl
* This option suppresses warnings about the use of script-targeted URLs—such as javascript:....

### shadow
* This option suppresses warnings about variable shadowing i.e. declaring a variable that had been already declared somewhere in the outer scope.

### sub
* This option suppresses warnings about using [] notation when it can be expressed in dot notation: person['name'] vs. person.name.

### supernew
* This option suppresses warnings about "weird" constructions like new function () { ... } and new Object;. Such constructions are sometimes used to produce singletons in JavaScript:
```
var singleton = new function() {
  var privateVar;

  this.publicMethod  = function () {}
  this.publicMethod2 = function () {}
};
```

### validthis
* This option suppresses warnings about possible strict violations when the code is running in strict mode and you use this in a non-constructor function. You should use this option—in a function scope only—when you are positive that your use of this is valid in the strict mode (for example, if you call your function using Function.call).
* Note: This option can be used only inside of a function scope. JSHint will fail with an error if you will try to set this option globally.

### noyield
* This option suppresses warnings about generator functions with no yield statement in them.
