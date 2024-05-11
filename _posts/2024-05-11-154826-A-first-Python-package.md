---
layout: post
title: A first Python package
tags: development
categories: zwift, software
---
We had a day off on Thursday this week - Ascension day in English and Auffahrt in German. This also meant that almost no
one was working on Friday, even though I did. So the day was quiet and I finished a bit early in the afternoon.

This combined with the he DIRT Racing Series going into our "off season" (e.g. Summer) when we won't have regular races
going and I don't need to worry so much about keeping our system stable. I've started looking at how to get the code
base into better shape and undo all the horrible hacks I've put in place to patch in one or another great idea we've
come up with to adjust the rules in the middle of the season. 

One first step in this was to extract the logic used to access Zwift from the main code base. I had a nudget to do this
from the Zwiftracing.app discord server where someone on the API chat was looking for Python code to talk to Zwiftpower.
I'd spent a good chunk of last summer figuring out how to finally get this working reliably and it was almost in good
enough shape to be presentable on its own.

So, one holiday day and a late Friday evening later, I had the code extracted, a wrapper script created to use it and a
new library [published on Pypi](https://pypi.org/project/zpdatafetch/). 

I needed to learn a few new tricks along the way, which is part of the fun.

- How to properly create a Python package for publication on Pypi. I was helped along in this by the Manning book
  [Publishing Python Packages](https://www.manning.com/books/publishing-python-packages) which I'd picked up a few weeks
  earlier knowing this was something I wanted to figure out. This helped, but setting up a different package with
  different assumptions and of course the need to just do it my way of course introduced some additional challenges.
- How to have the package deploy an executable (something in bin and not lib). I thought that just deploying the library
  wasn't sufficient. I know from my own experience that a small executable can help a lot to explore and doubles as a
  guide for how to use the library in your own code. It also helps to validate some assumptions for using the library
  itself. Even though the code is coming out of another package where it's actively used, I'm also stripping out bits
  that aren't relevant for a generic library and there was a chance that would lead to wrong assumptions. The wrapper
  program helped there a bit.
- How to get [Github actions](https://docs.github.com/en/actions) to test, build and publish the package to PyPi on
  commit. How to make sure every commit didn't lead to a new package and a host of other tricks to do with it. I've not
  dealt with Github actions or even worked with CI/CD in a few decades, for that matter. As with most toolkits that want
  to make life easier, there's enough of the inner workings kept hidden away that it was frustrating trying to bend it
  to my will. Lots to learn here - definitely still a work in progress.

So far, I'm pretty happy with the result. As far as I know I may be the only one to use it. But then maybe not. As
mentioned, I was triggered to set it up by a request from someone else. He might have downloaded a copy. Time will tell
if it actually gets used.
