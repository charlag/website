---
title: On metals
layout: post.liquid
is_draft: true
published_date: "2020-04-11 12:00:00 +0100"
---

With this post I want to start doing something I wanted to do for a long time
- complain about tech. Okay, not really but I want to talk about some things
which I don't see being discussed enough and surely you want to know my opinion.

Today's post is about.. *sigh* Javascript frontend framework. The one you
probably never heard of. It's called [mithril](https://mithril.js.org). The
reason I want to talk about it is because we use it at work and my lord someone
restrain me.. no, actually it's not that bad, it's just... quirky. This is the
first adjective I had for it since I learned it and few years since my first
contact I still feel the same.

Here I need to add remark that I do this in a good faith. I am very grateful to
all the people who maintain it and it is in no way attack on any of them or the
library itself. I'm trying to look at this from the very specific point of a
specific user.

So what is it's selling point? Surely it must have one? React is pure and tries
to get everything it can out of it, like scheduled rendering. Vue is
"progrssive" JavaScript framework (so it looks like HTML because templates).
Svelte is "disappearing" JS framework (more like "embedded"). Angular is.. uuuuh
tempaltes? I guess? So what's the deal with Mithril? "Mithril is a modern
client-side JavaScript framework for building Single Page Applications. It's
small (< 10kb gzip), fast and provides routing and XHR utilities out of the
box." "Isn't being small a Preact thing?" Yes. No. It's complicated. Preact is a
little smaller but it's *just* React UI. It's not enough to build an app with
just that. Mithril includes routing and... network for some reasons. So I guess
Mithril's selling point is "the smallest possible bundle to write apps not not
tear your hairs off your head". If React's promise is "purity will let us do
real smart things like conditional and scheduled render", Svelte's one is
"supercompilation" then mithril's one is "it is small enough that we can
optimize the heck out of it".

So what makes it quirky? Many things. The first most noticeable thing is that it
uses hyperscript syntax instead of templates/jsx. You can use JSX but I
wouldn't. It's like writing

```js
m("h1", {class: "title"}, "My first app")
```

instead of

```html
 <h1 class="title">My first app</h1>
```

To be honest I love that. I'm not a fan of writing HTML by hand, it's verbose,
annoying and error-prone. And it's a real Javascript function. Hyperscript is
not invented by mithril but mithril is the first framework I saw which uses it
as a primary element.

So what's quirky about it? Well, no one else uses that and I was people seeing
it for the first time, they don't understand what it is but they learn quickly.

The more quirky thing is what you can put into it. Besides a string you can put
class, object or a function (hold your breath). So it's already *three different
ways you can define components*. And two out of three work not like you think.

Let's start with an object. What's contact for it? It must have a `view()`
function and can have lifecycle functions. That's it. That's a really awesome
part, it doesn't have to extend anything. If you read nothing else and you are
told to define and use component you would probably write a class, instantiate
it with `new MyComponent()` and pass it to `m`. Wrong! That's *another* method
to use mithril, it's "object component". *Whatever you use as a first argument
to `m` is a template*. I wish it was said somewhere bold and clear. What mithril
would do if you did like I said above is *take your object and use it as
template*. Like, literally:

```js
if (typeof vnode3.tag.view === "function") {
  vnode3.state = Object.create(vnode3.tag)
  // ...
}
```

It will break `this` in your class. You will swear at mithril and redefine all
methods as arrow functions. This is what my team did. There's literally
alternative reality of components in our app: one is in this broken style, one
in proper style. I still can't get rid of all of them.

The second method is an object component. Which is, if you read above a
template. So if you will defined one inline, you would have really fun time not
understanding why your component is created again on each render pass. Which
leads us to the second rule which is "first argument to `m` must be stable".

The third method is a closure component. I imagine myself a pure function which
returns children, like in React. This is not the case. This is more like a
factory for the objects. And you can use variables declared inside function as a
state. I must admit that there's some elegancy in that but I think that most
modern JavaScript would rather use classes for this type of thing and I would
leave closure components for pure components. I've never seen this one in a
wild, maybe there are some quirks about it.

The other things about rendering that shocked me is that there's no conditional
rendering. I'm hoping I'm using the right term but it's when react doesn't
re-render you component because props are the same. Okay, there *is* conditional
rendering, you can return special value from `onbeforeupdate()`` but official
docs say that this should be the last resort. I think it's fine for the small
apps but for bigger ones I would rather have it automatic with possibility to
force render the whole tree. The fact that your `view()` will be invoked every
time something happens *anywhere* makes you resort to non-pure things which
kinda defeats the whole point of using such a framework.

So what about other things mithril comes with? Let's talk routing. It's not bad,
it's.. *quirky*. What you are expected to do is to define all app routes in one
place. On all depths. Again, this is only sensible for small apps but for bigger
ones I would really love having nested routers. We have a super clunky system of
`updateUrl()` functions where more functional framework would allow me to render
based on the url part I care about. There are two ways to do this: 1. grab
`m.route.get()` which returns you basically the whole URL as a string and you
need to parse it again which defeats the purpose of router or 2. parse all the
params in your router and pass it to the component as props, possibly through
several levels of nesting. I don't feel good about either. And you can get query
params easily which is not a problem in modern browsers anyway, that's not what
I need router for, I need router to parse URL for me. It asks to be nestable,
the syntax is `m.route(domElement, defaultRoute, routeResolvers)` where
`routeResolvers` is a map from route to the object which tells what to render.
Just drop the first argument and let me use it in any `view()` function! Isn't
this the most obvious thing to do? They even expose `parsePathname()` function
but it doesn't do this magical path variable parsing (where you define
`/path/:user` and `:user` is a variable part) nor does it split path into parts.
Why do I need it otherwise again?

What else? Network utilities. It comes with it's own Promise polyfill (!). On
one side, I'm fascinated that such a small library includes all of that on the
other hand… why? It's 2020, if you *need* a Promise polyfill, you should bring
your own. I must admit, we don't use it. We have our own network stack with
application-level caching and I understand where `fetch()` sucks (no progress
events) but I don't understand why it can't be a separate thing. Unlike routing
it is not coupled to the UI layer in any way. And mithril has two other optional
components: steam (super small and quirky reactive library) and ospec (small,
even quirkier super-opinionated testing framework). We use both of them. Maybe
there's some value in xhr module but I would say it's a good idea to separate
them.

And that about it. There are other bits here and there (you can define lifecycle
methods at both inside the component and outside and both will be called, nodes
with `onremove` callback are not recycled, you can define parameters as css
selectors, app wildly breaking on invalid selector, being written in ES5 instead
of just providing ES5-compiled version). It gives you an impression that it was
written to please everyone to write things the way they want yet it is very easy
to trip over something especially if the app is bigger than 5 components. Don't
get me wrong, for the mithril size it *delivers*. It is indeed very fast, it is
for the most part a good subset and flexibility comes in handy. It serves huge
multiplatform [app](https://mail.tutanota.com) as well as
[website](https://tutanota.com) about the app with more than million monthly
visitors, rending both its static and dynamic versions. But also it's probably
the library with the biggest LOC to quirk ratio I've seen.

I won't persuade anyone to use or not use it, I think that your project
requirements should define it, maybe you are better served with a framework with
bigger community (and bigger choice of libraries), maybe XHR and json-p are
exactly the things you need. I just wanted to provide some pitfalls which I've
seen people falling over and over into and possibly provide some feedback for the
future.
