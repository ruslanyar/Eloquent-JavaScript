{{meta {docid: values}}}

# Значения, типы и операторы

{{quote {author: "Master Yuan-Ma", title: "The Book of Programming", chapter: true}

Под поверхностью машины программа движется. Без усилий она расширяется и сжимается. В великой гармонии электроны рассеиваются и перегруппировываются. Формы на мониторе - лишь рябь на воде. Сущность незримо пребывает внизу.

quote}}

{{index "Yuan-Ma", "Book of Programming"}}

{{figure {url: "img/chapter_picture_1.jpg", alt: "Illustration of a sea of dark and bright dots (bits) with islands in it", chapter: framed}}}

{{index "binary data", data, bit, memory}}

В мире компьютера существуют только данные. Вы можете читать данные, изменять их, создавать новые - но то, что не является данными, не может быть упомянуто. Все эти данные хранятся в виде длинных последовательностей битов и поэтому в основе своей одинаковы.

{{index CD, signal}}

_Биты_ - это любые двузначные значения, обычно описываемые как нули и единицы. Внутри компьютера они принимают такие формы, как высокий или низкий электрический заряд, сильный или слабый сигнал, блестящее или тусклое пятно на поверхности компакт-диска. Любая часть дискретной информации может быть сведена к последовательности нулей и единиц и, таким образом, представлена в битах.

{{index "binary number", "decimal number"}}

Например, мы можем выразить число 13 в битах. Это работает так же, как и с десятичными числами, но вместо 10 различных ((цифр)) у нас только 2, и вес каждой из них увеличивается в 2 раза справа налево. Вот биты, составляющие число 13, с весами цифр, показанными под ними:

```{lang: null}
   0   0   0   0   1   1   0   1
 128  64  32  16   8   4   2   1
```

Это двоичное число 00001101. Его ненулевые цифры означают 8, 4 и 1 и в сумме дают 13.

## Значения

{{index [memory, organization], "volatile data storage", "hard drive"}}

Представьте море битов — океан из них. Типичный современный компьютер имеет более 100 миллиардов битов в своём временном хранилище данных (оперативной памяти). Постоянное хранилище (жёсткий диск или его эквивалент) обычно имеет ещё на несколько порядков больше.

Чтобы иметь возможность работать с такими объёмами битов, не теряясь при этом, мы разделяем их на фрагменты, которые представляют собой части информации. В среде JavaScript эти фрагменты называются __(значения)ми__. Хотя все значения состоят из битов, они играют разные роли. Каждое значение имеет ((тип)), который определяет его роль. Некоторые значения - это числа, некоторые - фрагменты текста, некоторые - функции и так далее.

{{index "garbage collection"}}

Чтобы создать значение, вам достаточно просто вызвать его имя. Это удобно. Вам не нужно собирать строительный материал для ваших значений или платить за них. Вы просто вызываете одно, и __вжуух__ — оно у вас есть. Конечно, значения не создаются из воздуха. Конечно, значения не создаются из воздуха. Каждое из них должно где-то храниться, и если вы хотите использовать огромное количество значений одновременно, у вас может закончиться память компьютера. К счастью, это проблема только в том случае, если вам нужно использовать их все одновременно. Как только вы перестаёте использовать значение, оно исчезает, оставляя свои биты для переработки в строительный материал для следующего поколения значений.

Оставшаяся часть этой главы знакомит с атомарными элементами программ на JavaScript, то есть с простыми типами значений и операторами, которые могут действовать на такие значения.

## Числа

{{index [syntax, number], number, [number, notation]}}

Значения типа __number__ — это, что неудивительно, числовые значения. В программе на JavaScript они записываются следующим образом:

```
13
```

{{index "binary number"}}

Использование этого в программе приведёт к тому, что в памяти компьютера появится битовая последовательность для числа 13.

{{index [number, representation], bit}}

Для хранения одного числового значения JavaScript использует фиксированное количество битов равное 64. Существует ограниченное количество комбинаций, которые можно создать с помощью 64 битов, что ограничивает количество различных чисел, которые могут быть представлены. Имея __N__ десятичных ((цифр)), можно представить 10^N^ чисел. Аналогично, имея 64 двоичных цифры, можно представить 2^64^ различных чисел, что составляет около 18 квинтиллионов (18 с 18 нулями). Это очень много.

Раньше память компьютеров была намного меньше, и люди часто использовали группы из 8 или 16 битов для представления чисел. Было легко случайно __переполнить__ такие маленькие числа — т.е. получить число, которое не помещается в заданное количество битов. Сегодня даже компьютеры, которые помещаются в карман, имеют достаточно памяти, поэтому вы можете свободно использовать 64-битные блоки и беспокоиться о переполнении только при работе с действительно астрономическими числами.

{{index sign, "floating-point number", "sign bit"}}

Однако не все целые числа меньше 18 квинтиллионов помещаются в тип number JavaScript. Эти биты также хранят отрицательные числа, поэтому один бит указывает на знак числа. Ещё более серьезной проблемой является представление нецелых чисел. Для этого некоторые биты используются для хранения положения десятичной точки. Фактическое максимальное целое число, которое может быть записано, находится в диапазоне около 9 квадриллионов (15 нулей) — что всё ещё достаточно много.

{{index [number, notation], "fractional number"}}

Дробные числа записываются с помощью точки:

```
9.81
```

{{index exponent, "scientific notation", [number, notation]}}

Для очень больших или очень маленьких чисел вы также можете использовать научную (экспоненциальную) нотацию, добавляя _e_ (_экспонента_), за которым следует показатель степени числа.

```
2.998e8
```

Это 2.998 × 10^8^ = 299,800,000.

{{index pi, [number, "precision of"], "floating-point number"}}

Вычисления с целыми числами (также называемыми _((integer))s_), которые меньше вышеупомянутых 9 квадриллионов, гарантированно всегда будут точными.  К сожалению, вычисления с дробными числами обычно таковыми не являются. Так же, как π (пи) не может быть точно выражено конечным числом десятичных знаков, так и многие числа теряют точность, когда для их хранения доступно только 64 бита. Это досадно, но вызывает практические проблемы только в определенных ситуациях. Важно осознавать это и относиться к дробным числовым значениям как к приблизительным, а не как к точным.

### Арифметика

{{index [syntax, operator], operator, "binary operator", arithmetic, addition, multiplication}}

Основное, что можно делать с числами, — это арифметические операции. Арифметические операции, такие как сложение или умножение, берут два числовых значения и производят из них новое число. Вот как они выглядят в JavaScript:

```{meta: "expr"}
100 + 4 * 11
```

{{index [operator, application], asterisk, "plus character", "* operator", "+ operator"}}

Символы `+` и `*` называются _операторами_. Первый обозначает сложение, а второй — умножение. Размещение оператора между двумя значениями применит его к этим значениям и создаст новое.

{{index grouping, parentheses, precedence}}

Означает ли этот пример "Сложите 4 и 100, а затем умножьте результат на 11", или умножение выполняется до сложения? Как вы могли догадаться, умножение выполняется первым. Как и в математике, вы можете изменить это, заключив сложение в скобки.

```{meta: "expr"}
(100 + 4) * 11
```

{{index "hyphen character", "slash character", division, subtraction, minus, "- operator", "/ operator"}}

Для вычитания используется оператор `-`. Деление можно выполнить с помощью оператора `/`.

Когда операторы встречаются вместе без скобок, порядок их применения определяется _((приоритетом))_ операторов. Пример показывает, что умножение выполняется перед сложением. Оператор `/` имеет тот же приоритет, что и `*`. Аналогично, `+` и `-` имеют одинаковый приоритет. Когда несколько операторов с одинаковым приоритетом оказываются рядом, как в `1 - 2 + 1`, они применяются слева направо: `(1 - 2) + 1`.

Не беспокойтесь слишком сильно об этих правилах приоритета. Если сомневаетесь, просто добавьте скобки.

{{index "modulo operator", division, "remainder operator", "% operator"}}

Существует ещё один арифметический оператор, который вы можете не сразу узнать. Символ `%` используется для обозначения операции _остатка от деления_. `X % Y` — это остаток от деления `X` на `Y`. Например, `314 % 100` даёт `14`, а `144 % 12` — `0`. Приоритет оператора остатка такой же, как у умножения и деления. Вы также часто можете видеть, что этот оператор называют _модулем_.

### Специальные числа

{{index [number, "special values"], infinity}}

В JavaScript есть три специальных значения, которые считаются числами, но не ведут себя как обычные числа. Первые два — это `Infinity` и `-Infinity`, которые представляют положительную и отрицательную бесконечности. `Infinity - 1` всё равно будет `Infinity`, и так далее. Однако не стоит слишком доверять вычислениям, основанным на бесконечности. Это математически некорректно и быстро приведёт к следующему специальному числу: `NaN`.

{{index NaN, "not a number", "division by zero"}}

`NaN` означает  "not a number" ("не число"), несмотря на то, что оно _является_ значением числового типа. Такой результат вы получите, например, когда попытаетесь вычислить `0 / 0` (ноль делить на ноль), `Infinity - Infinity` или любые другие числовые операции, которые не дают осмысленного результата.

## Строки

{{indexsee "grave accent", backtick}}

{{index [syntax, string], text, character, [string, notation], "single-quote character", "double-quote character", "quotation mark", backtick}}

Следующий базовый тип данных - _((string))_ (строка). Строки используются для представления текста. Они записываются путем заключения их содержимого в кавычки.

```
`Down on the sea`
"Lie on the ocean"
'Float on the ocean'
```

Для обозначения строк можно использовать одинарные, двойные или обратные кавычки, при условии, что кавычки в начале и в конце строки совпадают.

{{index "line break", "newline character"}}

You can put almost anything between quotes to have JavaScript make a string value out of it. But a few characters are more difficult. You can imagine how putting quotes between quotes might be hard, since they will look like the end of the string. _Newlines_ (the characters you get when you press [enter]{keyname}) can be included only when the string is quoted with backticks (`` ` ``).

{{index [escaping, "in strings"], ["backslash character", "in strings"]}}

To make it possible to include such characters in a string, the following notation is used: a backslash (`\`) inside quoted text indicates that the character after it has a special meaning. This is called _escaping_ the character. A quote that is preceded by a backslash will not end the string but be part of it. When an `n` character occurs after a backslash, it is interpreted as a newline. Similarly, a `t` after a backslash means a ((tab character)). Take the following string:

```
"This is the first line\nAnd this is the second"
```

This is the actual text in that string:

```{lang: null}
This is the first line
And this is the second
```

There are, of course, situations where you want a backslash in a string to be just a backslash, not a special code. If two backslashes follow each other, they will collapse together, and only one will be left in the resulting string value. This is how the string "_A newline character is written like `"`\n`"`._" can be expressed:

```
"A newline character is written like \"\\n\"."
```

{{id unicode}}

{{index [string, representation], Unicode, character}}

Strings, too, have to be modeled as a series of bits to be able to exist inside the computer. The way JavaScript does this is based on the _((Unicode))_ standard. This standard assigns a number to virtually every character you would ever need, including characters from Greek, Arabic, Japanese, Armenian, and so on. If we have a number for every character, a string can be described by a sequence of numbers. And that's what JavaScript does.

{{index "UTF-16", emoji}}

There's a complication though: JavaScript's representation uses 16 bits per string element, which can describe up to 2^16^ different characters. However, Unicode defines more characters than that—about twice as many, at this point. So some characters, such as many emoji, take up two "character positions" in JavaScript strings. We'll come back to this in [Chapter ?](higher_order#code_units).

{{index "+ operator", concatenation}}

Strings cannot be divided, multiplied, or subtracted. The `+` operator _can_ be used on them, not to add, but to _concatenate_—to glue two strings together. The following line will produce the string `"concatenate"`:

```{meta: "expr"}
"con" + "cat" + "e" + "nate"
```

String values have a number of associated functions (_methods_) that can be used to perform other operations on them. I'll say more about these in [Chapter ?](data#methods).

{{index interpolation, backtick}}

Strings written with single or double quotes behave very much the same—the only difference lies in which type of quote you need to escape inside of them. Backtick-quoted strings, usually called _((template literals))_, can do a few more tricks. Apart from being able to span lines, they can also embed other values.

```{meta: "expr"}
`half of 100 is ${100 / 2}`
```

When you write something inside `${}` in a template literal, its result will be computed, converted to a string, and included at that position. This example produces the string `"half of 100 is 50"`.

## Unary operators

{{index operator, "typeof operator", type}}

Not all operators are symbols. Some are written as words. One example is the `typeof` operator, which produces a string value naming the type of the value you give it.

```
console.log(typeof 4.5)
// → number
console.log(typeof "x")
// → string
```

{{index "console.log", output, "JavaScript console"}}

{{id "console.log"}}

We will use `console.log` in example code to indicate that we want to see the result of evaluating something. (More about that in the [next chapter](program_structure).)

{{index negation, "- operator", "binary operator", "unary operator"}}

The other operators shown so far in this chapter all operated on two values, but `typeof` takes only one. Operators that use two values are called _binary_ operators, while those that take one are called _unary_ operators. The minus operator (`-`) can be used both as a binary operator and as a unary operator.

```
console.log(- (10 - 2))
// → -8
```

## Boolean values

{{index Boolean, operator, true, false, bit}}

It is often useful to have a value that distinguishes between only two possibilities, like "yes" and "no" or "on" and "off". For this purpose, JavaScript has a _Boolean_ type, which has just two values, true and false, written as those words.

### Comparison

{{index comparison}}

Here is one way to produce Boolean values:

```
console.log(3 > 2)
// → true
console.log(3 < 2)
// → false
```

{{index [comparison, "of numbers"], "> operator", "< operator", "greater than", "less than"}}

The `>` and `<` signs are the traditional symbols for "is greater than" and "is less than", respectively. They are binary operators. Applying them results in a Boolean value that indicates whether they hold true in this case.

Strings can be compared in the same way.

```
console.log("Aardvark" < "Zoroaster")
// → true
```

{{index [comparison, "of strings"]}}

The way strings are ordered is roughly alphabetic but not really what you'd expect to see in a dictionary: uppercase letters are always "less" than lowercase ones, so `"Z" < "a"`, and nonalphabetic characters (!, -, and so on) are also included in the ordering. When comparing strings, JavaScript goes over the characters from left to right, comparing the ((Unicode)) codes one by one.

{{index equality, ">= operator", "<= operator", "== operator", "!= operator"}}

Other similar operators are `>=` (greater than or equal to), `<=` (less than or equal to), `==` (equal to), and `!=` (not equal to).

```
console.log("Garnet" != "Ruby")
// → true
console.log("Pearl" == "Amethyst")
// → false
```

{{index [comparison, "of NaN"], NaN}}

There is only one value in JavaScript that is not equal to itself, and that is `NaN` ("not a number").

```
console.log(NaN == NaN)
// → false
```

`NaN` is supposed to denote the result of a nonsensical computation, and as such, it isn't equal to the result of any _other_ nonsensical computations.

### Logical operators

{{index reasoning, "logical operators"}}

There are also some operations that can be applied to Boolean values themselves. JavaScript supports three logical operators: _and_, _or_, and _not_. These can be used to "reason" about Booleans.

{{index "&& operator", "logical and"}}

The `&&` operator represents logical _and_. It is a binary operator, and its result is true only if both the values given to it are true.

```
console.log(true && false)
// → false
console.log(true && true)
// → true
```

{{index "|| operator", "logical or"}}

The `||` operator denotes logical _or_. It produces true if either of the values given to it is true.

```
console.log(false || true)
// → true
console.log(false || false)
// → false
```

{{index negation, "! operator"}}

_Not_ is written as an exclamation mark (`!`). It is a unary operator that flips the value given to it—`!true` produces `false` and `!false` gives `true`.

{{index precedence}}

When mixing these Boolean operators with arithmetic and other operators, it is not always obvious when parentheses are needed. In practice, you can usually get by with knowing that of the operators we have seen so far, `||` has the lowest precedence, then comes `&&`, then the comparison operators (`>`, `==`, and so on), and then the rest. This order has been chosen such that, in typical expressions like the following one, as few parentheses as possible are necessary:

```{meta: "expr"}
1 + 1 == 2 && 10 * 10 > 50
```

{{index "conditional execution", "ternary operator", "?: operator", "conditional operator", "colon character", "question mark"}}

The last logical operator we will look at is not unary, not binary, but _ternary_, operating on three values. It is written with a question mark and a colon, like this:

```
console.log(true ? 1 : 2);
// → 1
console.log(false ? 1 : 2);
// → 2
```

This one is called the _conditional_ operator (or sometimes just _the ternary operator_ since it is the only such operator in the language). The operator uses the value to the left of the question mark to decide which of the two other values to "pick". If you write `a ? b : c`, the result will be `b` when `a` is true and `c` otherwise.

## Empty values

{{index undefined, null}}

There are two special values, written `null` and `undefined`, that are used to denote the absence of a _meaningful_ value. They are themselves values, but they carry no information.

Many operations in the language that don't produce a meaningful value yield `undefined` simply because they have to yield _some_ value.

The difference in meaning between `undefined` and `null` is an accident of JavaScript's design, and it doesn't matter most of the time. In cases where you actually have to concern yourself with these values, I recommend treating them as mostly interchangeable.

## Automatic type conversion

{{index NaN, "type coercion"}}

In the [introduction](intro), I mentioned that JavaScript goes out of its way to accept almost any program you give it, even programs that do odd things. This is nicely demonstrated by the following expressions:

```
console.log(8 * null)
// → 0
console.log("5" - 1)
// → 4
console.log("5" + 1)
// → 51
console.log("five" * 2)
// → NaN
console.log(false == 0)
// → true
```

{{index "+ operator", arithmetic, "* operator", "- operator"}}

When an operator is applied to the "wrong" type of value, JavaScript will quietly convert that value to the type it needs, using a set of rules that often aren't what you want or expect. This is called _((type coercion))_. The `null` in the first expression becomes `0` and the `"5"` in the second expression becomes `5` (from string to number). Yet in the third expression, `+` tries string concatenation before numeric addition, so the `1` is converted to `"1"` (from number to string).

{{index "type coercion", [number, "conversion to"]}}

When something that doesn't map to a number in an obvious way (such as `"five"` or `undefined`) is converted to a number, you get the value `NaN`. Further arithmetic operations on `NaN` keep producing `NaN`, so if you find yourself getting one of those in an unexpected place, look for accidental type conversions.

{{index null, undefined, [comparison, "of undefined values"], "== operator"}}

When comparing values of the same type using the `==` operator, the outcome is easy to predict: you should get true when both values are the same, except in the case of `NaN`. But when the types differ, JavaScript uses a complicated and confusing set of rules to determine what to do. In most cases, it just tries to convert one of the values to the other value's type. However, when `null` or `undefined` occurs on either side of the operator, it produces true only if both sides are one of `null` or `undefined`.

```
console.log(null == undefined);
// → true
console.log(null == 0);
// → false
```

That behavior is often useful. When you want to test whether a value has a real value instead of `null` or `undefined`, you can compare it to `null` with the `==` or `!=` operator.

{{index "type coercion", [Boolean, "conversion to"], "=== operator", "!== operator", comparison}}

What if you want to test whether something refers to the precise value `false`? Expressions like `0 == false` and `"" == false` are also true because of automatic type conversion. When you do _not_ want any type conversions to happen, there are two additional operators: `===` and `!==`. The first tests whether a value is _precisely_ equal to the other, and the second tests whether it is not precisely equal. Thus `"" === false` is false, as expected.

I recommend using the three-character comparison operators defensively to prevent unexpected type conversions from tripping you up. But when you're certain the types on both sides will be the same, there is no problem with using the shorter operators.

### Short-circuiting of logical operators

{{index "type coercion", [Boolean, "conversion to"], operator}}

The logical operators `&&` and `||` handle values of different types in a peculiar way. They will convert the value on their left side to Boolean type in order to decide what to do, but depending on the operator and the result of that conversion, they will return either the _original_ left-hand value or the right-hand value.

{{index "|| operator"}}

The `||` operator, for example, will return the value to its left when that value can be converted to true and will return the value on its right otherwise. This has the expected effect when the values are Boolean and does something analogous for values of other types.

```
console.log(null || "user")
// → user
console.log("Agnes" || "user")
// → Agnes
```

{{index "default value"}}

We can use this functionality as a way to fall back on a default value. If you have a value that might be empty, you can put `||` after it with a replacement value. If the initial value can be converted to false, you'll get the replacement instead. The rules for converting strings and numbers to Boolean values state that `0`, `NaN`, and the empty string (`""`) count as false, while all the other values count as true. That means `0 || -1` produces `-1`, and `"" || "!?"` yields `"!?"`.

{{index "?? operator", null, undefined}}

The `??` operator resembles `||` but returns the value on the right only if the one on the left is `null` or `undefined`, not if it is some other value that can be converted to `false`. Often, this is preferable to the behavior of `||`.

```
console.log(0 || 100);
// → 100
console.log(0 ?? 100);
// → 0
console.log(null ?? 100);
// → 100
```

{{index "&& operator"}}

The `&&` operator works similarly but the other way around. When the value to its left is something that converts to false, it returns that value, and otherwise it returns the value on its right.

Another important property of these two operators is that the part to their right is evaluated only when necessary. In the case of `true || X`, no matter what `X` is—even if it's a piece of program that does something _terrible_—the result will be true, and `X` is never evaluated. The same goes for `false && X`, which is false and will ignore `X`. This is called _((short-circuit evaluation))_.

{{index "ternary operator", "?: operator", "conditional operator"}}

The conditional operator works in a similar way. Of the second and third values, only the one that is selected is evaluated.

## Summary

We looked at four types of JavaScript values in this chapter: numbers, strings, Booleans, and undefined values. Such values are created by typing in their name (`true`, `null`) or value (`13`, `"abc"`).

You can combine and transform values with operators. We saw binary operators for arithmetic (`+`, `-`, `*`, `/`, and `%`), string concatenation (`+`), comparison (`==`, `!=`, `===`, `!==`, `<`, `>`, `<=`, `>=`), and logic (`&&`, `||`, `??`), as well as several unary operators (`-` to negate a number, `!` to negate logically, and `typeof` to find a value's type) and a ternary operator (`?:`) to pick one of two values based on a third value.

This gives you enough information to use JavaScript as a pocket calculator but not much more. The [next chapter](program_structure) will start tying these expressions together into basic programs.
