---
title: HTTP Protocol
date: February 14 2013 11:07
layout: note
---

# Caching #
Conditional GET
: If the object in the browser cache is 'fresh', the server won't resent the response.  Conditional GET has last modified date from cache.  Browsers save object in cache with a last modified tag.  Server can respond with a 304 Not Modified message if the image hasn't changed since that date.  If modified, it returns a 200 OK with the object's data.

What is the average time to retrieve a web object?
: `T_mean = hit_ratio * t_cache + (1 - hit_ratio) * t_server`

What is the mean access time from a disk cache?
: Depends on many different things, but in the area of 1-10 ms

So, if the hit ratio is 60%?
: `T_mean = .6 * 10 ms + .4 * 1000 ms = 406 ms`

Having a disk cache reduced the average response time from 1 second to ~400 ms.

What determines the hit ratio?
: Cache size - can retain more stuff
: *Locality of references* - how often the same web object requested
: How long objects remain 'fresh' or unchanged
: Object references that can't be cached. I.E., dynamically generated content, protected content, content purchased each use, content that must be always up-to-date, advertisements ('pay-per-click').

# Chapter 2 - Problem 1 #

	A: dog.com - 20,000 bits - 2*50 ms + .2 ms = 100.2 ms

	A: dog.com/dog-banner.jpg - 2*50 ms + 15 000 / 100 000 000 = 100.15 ms
	B: cat.com/meow-add.jpg - 2*10 ms + 10 000 / 100 000 000 = 20.1 ms
	C: bird.com/chirp-add.jpg - 2*20 ms + 10 000 / 100 000 000 = 40.1 ms
	D: cat.com/puss-chow-add.jpg - 2*10 ms + 10 000 / 100 000 000 = 20.1 ms

	B: www.dog.com/dog-chow-add.jpg - 2*50 ms + 0.1 ms = 100.1 ms
	D: www2.dog.com/cookie.crumb - 2*50 ms + 0.05 ms = 100.05 ms

Persistent, reusing domain first

	A: dog.com - 2*50 ms + .2 ms = 100.2 ms
	A: dog.com/dog-banner.jpg - 50 ms + .15 ms = 50.15 ms
	A: dog.com/dog-chow-add.jpg - 50 ms + .1 ms = 50.1 ms

	B: cat.com/meow-add.jpg - 2*10 ms + .1 ms = 20.1 ms
	B: cat.com/puss-chow-add.jpg - 10 ms + .1 ms = 10.1 ms

