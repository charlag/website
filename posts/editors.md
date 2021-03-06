---
title: Editors
layout: post.liquid
is_draft: false
published_date: "2019-03-7 22:17:26 +0100"
---

I think I talk about text editors suprisingly a lot. I'm not one of those people
who use Emacs as their OS but I think I've tried some things over the years with
varying level of success and I can speak about it.

It must be very boring topic for non-programmers. When you say "text editor"
most people likely think of something like their standard OS text editor
which is indeed very boring think. Fortunately I mean not that.

I think many people been afraid that text will lose its significance with
technology. It did not. It is as important as ever. For most people text
is one of the main ways to communicate with other human beings. For
programmers it's way of self-expression and part of the craft. Many
people chose to do *all* of their things with text editor but I'm not one
of them (yet). For me text editor is for (sic) writing text and for
programming. And I was frustrated a lot with the second thing. As with
most software I can with high degree of confidence say that they're all
bad but in their own ways. “All happy families are alike; each unhappy family is
unhappy in its own way.”.

Up until recently I was waiting for Xi or Xray. There's a good chance you've
never heard about them. These are two very similar projects, one by Googler,
one by Github folks who worked on Atom. Both are written in Rust. Both are
persuading a very hard goal which sounds pretty nice: efficient asynchronous
reading by multiple users/extensions. Both use sophisticated data structures
like ropes to achieve their goals. Both are experimental and don't seem to
rush to the release. My interest in them grows from the fact that they're
written in Rust and from dissatisfaction with everything else. And their
motivation sounds good! Asynchronous plugins, in any language, isn't it great?

No, I don't think so. Not in the "any language" part, at least in a way they
persuade it. I realise now that their goals are rather esoteric. Github wants
realtime collaboration while I think it's not a good idea at all. Shipping
packages as separate binaries is not really nice and leads to the same problems
Vim has currently, when you sometimes need Perl, Python, Ruby, Lua and whatnot.

Let's briefly look at other editors. We have oldies like Vim or Emacs, we have
some 2000s kids like Sublime, Brackets & Atom and we have VS Code. I don't want
to talk about big IDEs and very simplistic editors right now. The former ask you
to give up too much for what they give and the latter is not what I'm talking
about here.

- VS Code is something I've never used myself but I've helped my collegue with
it once. I lose a lot of credibility of talking about editors in someone's eyes
with this statement but I somehow think that it doesn't bring terribly too much
to the plate after Atom except that it's engineered much better so it's faster
etc. I still don't want something that is made by Microsoft. I think they
use it for expanding their influence and I absolutely hate how binaries their
distribute are different thing from the sources and all the tracking things.
I want to sue something made by the community for the community. It's not 
hackable on a level I want to.

- Sublime was never appealing to me. It's pretty rigid, it's commercial, it's
stagnating in my opinion. That's all I have to say about it.

- I used Atom for a long time but I've alway shad performance problems with it.
Really. Always problems with plugins breaking down and command palette not
finding what I want etc etc. It's a pioneer so it had quite some architecture
problems. I gave up on it recently because of the graphical issues, Atom-IDE
being deprecated (Facebook has given up on it) and other issues.

- Brackets seems to be made for web deveopment. While it's a niche I don't think
that's an editor for me. It's not supported by community well enough to have a
lot of packages but it doesn't seem it needs it.

- I like Vim's egonomic and composition ideas (really, nothing else has such a 
simple but beautiful simple of combining editing commands) but configuration
and plugin story always seemed like a miserable pile of hacks to me. That's
not the level of editing I want to use, that's nice for some config files
perhaps.

- I like Emacs'es... many things. Many words have been spoked about it and it's
hard to summarize it quickly. It is pretty much arcane alien from the 70s which
somehow stays alive still. There are many wonderful things about it as well as
own horros but maybe I'll talk about it some other time. I was using it and
giving up on it and I still am.

What do I use? At work we use Intellij and deviations because they mostly 
"just work", at home I do mostly Android development so I'm kind of bound to
Android Studio which manages to eat all my RAM against all guards and I
passionately hate it. Don't get me wrong, I've used Xcode for the significant
part of my career and in comparison to that Android Studio is amazing but
that's just a tool for me which a cannot change.

As a result I became quite good at handling Intellij. But as I said, I think
it's just not worth it. For the things it asks you to give up (hackability,
introspection, resources and sometimes money) it doesn't give you that much
more than a good language server would (and sometimes less).

So for all the small part which is not my job and not the project I
mostly contribute to, my main tools is Emacs again. Or, to be more precisely,
Spacemacs. Space... what? Well, it's Emacs preconfigured to include Evil which
is Extensive Vi Layer or something like that. Basically it emulates Vim and
does so very well. Really well. And it also has much more saner defaults (more
or less). Watch this if you don't believe me: 
[Youtube video titled "Evil Mode: Or, How I Learned to Stop Worrying
and Love Emacs"](https://www.youtube.com/watch?v=JWD1Fpdd4Pc&t=0s&index=5&list=WL)

If you ask my collegues they would probably say that I like to fiddle with
everything and configure it but that's not really true. Maybe it's true from 
their perspective but compared to most Emacs users out there I just like 
defaults. And all these ancient editors are notoriously bad with defaults.
But I want hackability to be there if I need it.

Well, so, Spacemacs has infinite hackability, introspection, made by community,
has a lot of packages for all kinds of things, has ergonomic keybindings if you
know where to get them, what else can you ask for? Well, it's still 33 years
old editor (that's right, initial release was *thirty three years ago*, initial
version is actually *fourty three* years old) and the language support is
lacking at times. Even though Spacemacs claims to be consistent and mnemonic
it's still a wild smash of Vim and Emacs worlds (yeah, there are many ways
to save the file. Or search for a string) which still misses some consistency.
There's a little chance it can get popular - you don't copy text with Ctrl-C in
almost any configs you can find out there. Tell it to people and they'll show
you what they think about it. It has tons of problems, there are some attempts
to move base to Rust and to replace Emacs Lisp (language it's written in) with
Guile which would be blowing-roof awesome from all the points of view and
there's a small core contributor with maintainers who are afraid of touching
any of it (I could reference it but I won't. Search for "Portable buffer"
messages in mailing list). If people use such an ancient peace of software it
must be either exceptionally good or everything else must be exceptionally bad.
I think it's both.
