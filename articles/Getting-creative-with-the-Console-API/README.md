# Getting creative with the Console API!

**Debugging** in JavaScript has always been inseparably connected with the **Console API**, which is most of the time used only through `console.log()`. But, did you know that it doesn't have to be this way? Hasn't `console.log()` already bored you with its **monolithic** output? Do you want to make your logs better, to make them **prettier**? 💅 If so, follow me, as we'll discover how colorful and playful Console API can really be!

# [Console.log()](https://developer.mozilla.org/en-US/docs/Web/API/Console/log)

Believe it or not, but `console.log()` itself has some additional functionalities you may not know about. Of course, its basic purpose - **logging** - remains untouched. The only thing we can do is to make it look prettier! Let's try that, shall we? 😁

## String subs

The only thing tightly related to `console.log()` method is that you can use it with so-called **string substitution**. This basically provides you an option to use specific expressions in a string, that will later be replaced by provided arguments. It can look somewhat like this:

```javascript
console.log("Object value: %o with string substitution",
    {string: "str", number: 10});

12
```

Nice, huh? The catch is there are multiple variants of string substitution expression:

- **%o / %O** - for objects;
- **%d / %i** - for integers;
- **%s** - for strings;
- **%f** - for floating-point numbers;

But, with that said, you may wonder why to even use such a feature? Especially when you can easily pass multiple values to log, like this:

```javascript
console.log("Object value: ",
    {string: "str", number: 10},
    " with string substitution");

123
```

Also, for strings and numbers, you can just use **string literals**! So, what's the deal? Well, first, I'd say that when doing some nice console logging, you just want some nice strings, and string subs allow you to do just that, with ease! As for the alternatives above - you must agree - you need to keep your eyes open for all those spaces. 🛸 With subs, it's just much more convenient. As for string literals tho, they haven't been around as long as these subs (surprise! 🤯) and... they don't provide the same, nice formatting for objects. But yeah, as long as you're working with numbers and strings only, you may prefer **a different approach**.

## CSS

There's one more string-sub-like directive that we haven't learned before. It's **%c** and it allows you to apply **CSS styles** string to your logged messages! 😮 Let me show you how to use it!

```javascript
console.log("Example %cCSS-styled%c %clog!",
    "color: red; font-family: monoscope;",
    "", "color: green; font-size: large; font-weight: bold");

123
```

The above example makes some extensive use of %c directive. As you can see, styles are applied to everything that **follows** the directive. The only way to escape is to use yet another directive. And that's exactly what we're doing here. If you want to use normal, unstyled log format, you'll need to pass an empty string. I think that it goes without saying, that values provided to the %c directive as well as other string subs needs to be submitted in the expected order, one by one as further arguments. 😉

# Grouping & tracing

We're only getting started and we've already introduced CSS to our logs - wow! What other secrets does Console API have?

## Grouping

Doing too much of console logging is not really healthy - it can lead to worse readability and thus... meaningless logs. It's always good to have some **structure** in place. You can achieve exactly that with `console.group()`. By using that method, you're able to create deep, collapsible structures in your console - **groups**! This not only allows you to hide but organize your logs as well. There's also a `console.groupCollapsed()` method if you want for your group to be collapsed by default. Of course, groups can be **nested** as much as you'd like (with common sense). You can also make your group have what-seems-like header-log, by passing a list of arguments to it (just like with `console.log()`). Every console call done after invoking the group method, will find its place inside created group. To exit it, you have to use a special `console.groupEnd()` method. Simple, right? 😁

```javascript
console.group();
console.log("Inside 1st group");
console.group();
console.log("Inside 2nd group");
console.groupEnd();
console.groupEnd();
console.log("Outer scope");

1234567
```

I think you've already noticed that you can just *copy&paste* the code inside all provided snippets to your console and play with them the way you want!

## Tracing

Another useful information you can get through the Console API is a path that leads to the current call (**execution path**/**stack trace**). You know, a list of in-code places links that were executed (e.g. functions chains) to get to the current `console.trace()` call, because that's the method we're talking about. This information is extremely useful whether it's for detecting **side-effect** or inspecting the flow of your code. Just drop the below fragment to your code to see what I'm talking about.

```javascript
console.trace("Logging the way down here!");

1
```

# Console.XXX

You probably already know some different methods of Console API. I'm talking about the ones that add some **additional information** to your logs. But, let's make a quick overview of them as well, shall we?

## Warning

The `console.warn()` method behaves just like the console.log (like most of these logging methods do), but, in addition, it has it's own **warning-like style**. ⚠ In most browsers, it should be **yellow**and have a warning symbol somewhere (for natural reasons). Calls to this method also return the **trace by default**, so you can quickly find where the warning (and possible bug) comes from.

```javascript
console.warn("This is a warning!");

1
```

## Error

The `console.error()` method, similarly to `console.warn()` outputs a message with stack traces, that's specially styled. It's usually **red** with the addition of an error icon. ❌ It clearly notifies the user that something is not right. Here an important thing is that this .error() method is **just a console message** without any additional options, like stopping code execution (to do this you need to throw an error). Just a simple note, as many newcomers can feel a bit unsure about this kind of behavior.

```javascript
console.error("This is an error!");

1
```

## Info & debug

There are two more methods that can be used to add some order to your logs. We're talking about `console.info()` and `console.debug()`. 🐞 Outputs of these don't always have a unique style - in some browsers it's just an **info icon**. Instead what these and also previous methods allow you to do is applying certain categories to your console messages. In different browsers (e.g. in my Chromium-based one) the dev-tools UI provides you an option to select a certain **category of logs** to display, e.g. errors, debugging messages or info. Just one more organizing feature!

```javascript
console.info("This is very informative!");
console.debug("Debugging a bug!");

12
```

## Assert

There's even a specific Console API method that gives you a shortcut for any conditional logging (**assertions**). It's called `console.assert()`. Just like the standard `console.log()` method, it can take an infinite number of arguments, with the difference being that the first one needs to be a **boolean**. If it resolves to true, then the assertion is left quiet, otherwise, it **logs an error** (same as .error() method) to the console with all passed arguments.

```javascript
console.assert(true, "This won't be logged!");
console.assert(false, "This will be logged!");

12
```

And, after all that mess, you may want to make your console messages board look a bit cleaner. No problem! Just use the `console.clear()` method and see all your old logs go away! It's such a useful feature, that it even has **it's own button** (and shortcut) in console interfaces of most browsers! 👍

# Timing

Console API even provides a small set of functions related to **timing**. ⌚ With their help, you can make a quick and dirty **performance tests** for parts of your code. As I said before, this API is simple. You start with `console.time()` method that can take an optional argument as a **label** or identification for the given timer. The mentioned timer starts just at the moment of invoking this method. Then you can use `console.timeLog()` and `console.timeEnd()` methods (with optional label argument) to log your time (in **milliseconds**) and end respected timer accordingly.

```javascript
console.time();
// code snippet 1
console.timeLog(); // default: [time] ms
// code snippet 2
console.timeEnd(); // default: [time] ms
1234
```

Of course, if you're doing some real benchmarking or performance tests, I'd recommend using the **Performance API**, that's specially designed for this purpose.

# Counting

In case you have so many logs that you don't know how many times given parts of the code have been executed - you've guessed it! - there's an API for that! The `console.count()` method does possibly the most basic thing it can - it counts **how many times it's been called**. 🧮 You can, naturally, pass an optional argument providing a label for a given counter (defaults to default). You can later reset chosen counter with `console.countReset()` method.

```javascript
console.count(); // default: 1
console.count(); // default: 2
console.count(); // default: 3
console.countReset();
console.count(); // default: 1
1234
```

Personally, I don't see many use-cases for this particular features, but it's good that something like that exist at all. Maybe it's just me...

# Tables

I think this is one of the most underrated features of Console API (beyond the CSS styles mentioned previously). 👏 The ability to output real, **sortable tables** to your console can be extremely useful when debugging and inspecting **flat** or **two-dimensional** **objects** and **arrays**. Yeah, that's right - you can actually display a table in your console. All it takes is just a simple `console.table()` call with one argument - most likely object or array (primitive values are just normally logged and more than 2-dimensional structures are truncated to smaller counterparts. Just try the snippet below to see what I mean!

```javascript
console.table([[0,1,2,3,4], [5,6,7,8,9]]);

1
```

# Console ASCII art

Console art wouldn't be the same without **ASCII art**! With the help of **image-to-ascii** module (can be found on **NPM**) you can convert a normal image to its ASCII counterpart with ease! 🖼 In addition to that, this module provides many **customizable settings** and options to create the output you want. Here's a simple example of this library in use:

```javascript
import imageToAscii from "image-to-ascii";

imageToAscii(
"https://d2vqpl3tx84ay5.cloudfront.net/500x/tumblr_lsus01g1ik1qies3uo1_400.png",
{
    colored: false,
}, (err, converted) => {
    console.log(err || converted);
});

123456789
```

With the code above, you can create **stunning JS logo**, just like the one in your console right now! 🤯

With the help of CSS styles, some padding, and background properties, you can also output a **full-fledged image** to your console! For example, you can take a look at **console.image** module (available on **NPM** too) to play with this feature as well. But still, I think ASCII is a bit more... **stylish**. 💅

# Modern logs

As you can see, your logs and debugging process as a whole doesn't have to be so monochrome! There's a lot more goodness out there than simple `console.log()`. With the knowledge from this article, the choice is now yours! You can stay with traditional `console.log()` and pretty fine formatting of different structures provided by your browser, or you can add some freshness to your console with the techniques described above. Anyway, just **keep having fun**... even if you're fighting with a really nasty bug! 🐞

I hoped you like the article and it allowed you to learn something new. As always, consider **sharing it** with others so anyone can have their consoles **full of colors** 🌈 and leave **your opinion**down below through **a reaction** or **a comment**! Also, **follow me** **on Twitter**, **on my Facebook page** and **sign up** for the (soon-to-be) **newsletter**! Again, thanks for reading and I'll see you in the next one! ✌