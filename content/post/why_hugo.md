+++
tags = ["hugo"]
author = "Andy Downs"
type = "post"
date = "2017-02-21T16:46:10Z"
title = "Why Hugo"
categories = [
  "Blog"
]

+++

I eventually settled on Hugo after looking at a lot of the popular static site generators, mainly [Hugo](https://gohugo.io), [Jekyll](https://jekyllrb.com/) and [Pelican](https://blog.getpelican.com/). My requirements were fairly simple and I was prepared to choose something with an opinionated way of doing things. I basically wanted something that was simple to get going that had some nice themes. If you have looked at any of the three platforms you would probably see that they could all meet my basic requirements.

With Jekyll and Pelican I started with understanding how you used them, but with both of them I felt like I was installing a lot of dependencies. I then realised a non functional requirement that speaks more to me than the software, I don't like installing stuff.. I am not a Ruby or Python dev, I can read and modify both but haven't had the opportunity to write anything remotely serious in either. So when intructions started talking about virtualenvs etc I suddenly thought, why am I not running this in a container? I can have all the requirements installed there not on my box, it is portable, I'll probably learn something etc.

So I stated playing with building containers, without really understanding what the workflow would/should look like. Suddenly felt my self going down a rabbit hole. If you have learned a new tech recently where you don't understand the eco system you are probably familiar with the feeling. This is the point when I remebered I am actually trying to write down some of the things I have been doing and have been using the tech that is going to display it as a mechanism to procrastinate.

I eventually settled on Hugo for the basic fact it was the first one I actually started to write some content in. With [Hugo](https://gohugo.io)) because it is written in Go you basically have one binary that you use. I won't go into the usage as the [Getting Started](https://gohugo.io/overview/introduction/) is pretty good at getting you going. While I currently used the [Hyde-y](https://github.com/enten/hyde-y) theme, I found it simple to add overrides to the layouts I didn't particularly like. This stopped my being paralysed by indescision at all the available themes. This was also a problem with Jekyll and Pelican, or should I say me.

So the conclusion is to keep an eye on your end goal. You will always learn as you build/create something try not to get sucked down a rabbit hole, sometimes you look up and realise it is a long way up to get out which can be disheartening.
