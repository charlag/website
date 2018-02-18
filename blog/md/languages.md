# Language(s)

I liked the idea described in 'In Search Of The Lost Program'. What is a takeaway from it you would ask? "There is no perfect program'? We know that's [not true](https://www.gnu.org/software/emacs/). I would say that to not reinvent all the programs in the world again and again we need 2 things:

* Small building blocks - be it libraries or unix-style utilities
* Language to write these blocks

Let me put it straight: I like learning programming languages. I'm not usually keen to master them, I don't have enough memory for that. But I _do_ like to grasp language's ideas, check language design (which tradeoffs are made?) and so on. I've tried quite a number of them: Java-style OOP, script ones, low-level ones (including assembly), lisps, lazy functional ones, ones with higher-order type systems. By one means I have a complete or even comprehensive pictures, I just want to give you a hint on my background. All I want to say is there are the same ideas everywhere. You can simulate vtables and dynamic dispatch in Haskell and you can simulate currying in Java.

If you paid attention to what's going on with languages you could notice that we are finally breaking out of the stupid 'language = fixed syntax + fixed implementation' paradigm. Notice how there are two components here. They were usually really tightly coupled with each other. Not anymore. How many languages are [hosted on the JVM now](https://www.youtube.com/watch?v=5BMHIeMXTqA)? On CLR? LLVM can run so many things as well as WebAssembly. Hell, even GNU Guile supports multiple front-ends. I believe there it is a really good thing for us, programmers. Compilers are already collection of very small layers stacked on each other, why not decouple them? Decoupling freedom lets us pick any front-end we want.

Another trend is that another component, front-end, tries to expand as much as possible. Scala, Scala Native and Scala.js. Kotlin on JVM, Kotlin to JS, Kotlin Native (which can eventually be compiled to WASM and be run in browser). Clojure and ClojureScript. JavaScript everywhere. Swift on mobile, desktop and server. Programmers are not completely stupid, they understand that re-writing things again is a huge waste. It's not 'Write Once - Run Everywhere'. It is usually 'I don't have to learn new syntax, semantics and libraries for every platform I want to support'.

You may guessed already why I'm talking about languages. We need them to write that building blocks. Currently to interop between languages we use the lowest common denominator - C (sometimes it's Java). I would argue that we could do better?

My question is simple: should we fix one of two parts? Should we agree on the front-end? If so, we need an /extendable/ language. Many people think one-language-to-rule-them-all doesn't work (like C++) because no one knows all of it. I think that the core should be simple enough while giving an ability to use advanced featured when you need them (GHC's LANGUAGE pragmas, Racket's #lang and like that). And of course we need proper macros. If you're going to confine developer to the non-extendable language they will go and write a new one. Is it possible? Would it be beneficial? I can't say.

Should we agree on the platform? Is it possible even? Will it be beneficial? I can't say.

All I want to say is that we're going to make a lot of redundant work if we won't change anything. Please don't make a language an instrument for dominating the market. It is not cool.
