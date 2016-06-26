+++
date = "2013-06-01T19:17:25-04:00"
title = "Tiptoeing through the internet"

+++

# Tiptoeing through the internet (part 1: HTTP)

It seems like these days every link you click on the internet sets off a chain reaction of events, notifying a vast array of tracking websites of your movement, and kicking off dozens of scripts to dazzle you while obscuring the content you’re trying to read.

This is how I fight back.

## How the web works

In order to properly defend against the intrusion of privacy the modern web is fraught with, you must first understand it. As Sun Tzu said, “know thy enemy”, and all that. So, here’s a short overview of how the web works.

The web operates over [HTTP](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol) (hence URLs beginning with “http://”). When you visit, say, some [CNN.com](http://www.cnn.com/) story your browser uses the HTTP protocol to tell CNN’s server that it wants a certain page, and one of CNN’s servers eventually responds with the content. I said “visit”, and this could mean typing “cnn.com” into your browser’s URL bar or it could mean clicking on a link (they work the same from the point of view of CNN’s server).

Using Chrome’s Developer Tools (View –> Developer –> Developer Tools), you can watch this request get sent. Here’s what I saw when I tried it:

```
GET /2013/06/02/us/massachusetts-bear-shot/index.html?hpt=hp_t2 HTTP/1.1
Host: www.cnn.com
Connection: keep-alive
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1521.3 Safari/537.36
Referer: http://www.cnn.com/
Accept-Encoding: gzip,deflate,sdch
Accept-Language: en-US,en;q=0.8
Cookie: ug=51ab9a100805d30a3d146b12f11960b7; ugs=1; optimizelyEndUserId=oeu1370200593265r0.5996987270191312; SelectedEdition=www; tnr:usrvtstg01=1370200603036%7C0%7C0%7C1%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C0%7C1%7Cf%7C1%7C5%7C1370200603036; s_vi=[CS]v1|28D5CD0F051D1296-40000103E021983F[CE]; mbox=session#1370200591135-76154#1370202746|check#true#1370200946; optimizelySegments=%7B%22170962340%22%3A%22false%22%2C%22171657961%22%3A%22gc%22%2C%22172148679%22%3A%22none%22%2C%22172265329%22%3A%22direct%22%7D; optimizelyBuckets=%7B%7D; tnr:sesctmp01=1370200902756; rsi_segs_ttn=A09801_10001|A09801_10313|A09801_0; _chartbeat2=9e41jhuek431pgvd.1370200605946.1370200911558.00000000000001; CG=US:NY:New+York; s_ppv=24; optimizelyPendingLogEvents=%5B%22n%3Dengagement%26u%3Doeu1370200593265r0.5996987270191312%26t%3D1370200923907%22%5D; s_cc=true; s_sq=cnn-adbp-domestic%3D%2526pid%253Dcnn%25253Ain%25253A%25252F%2526pidt%253D1%2526oid%253Dhttp%25253A%25252F%25252Fwww.cnn.com%25252F2013%25252F06%25252F02%25252Fus%25252Fmassachusetts-bear-shot%25252Findex.html%25253Fhpt%25253Dhp_t2%2526ot%253DA
```

Let’s dissect this a bit. The first line:

```
GET /2013/06/02/us/massachusetts-bear-shot/index.html?hpt=hp_t2 HTTP/1.1
```

Every HTTP request begins with one of a few specific *verbs*, which the server can use to help decide how to respond. The two most common verbs are `GET`, which is what your browser sends when you click a link or type in a URL, and `POST`, which is what your browser sends when you submit a form to the server.

Next it says what exactly to get, the *resource*. Here it’s an article about a bear in Boston. Historically, this was generally a file on the server, which is why the resource I’m getting looks like a file path with folders and whatnot with all those slashes. However, nowadays, that’s probably all dynamically generated, and CNN’s server is just taking the string as a whole and using it to determine what to retrieve from its database.

Lastly, the browser says it’s using HTTP version 1.1.

Now, none of this is too crazy, and thus far pretty transparent. The whole “/2013/06….index.html” is right there in your browser URL bar, so it probably doesn’t come as a shock that your browser is sending that to CNN. After all, CNN needs to know what article you want to read.

But that’s only the veeeerrrrrryy tip of the iceberg of what gets sent to whom. In this very first request, even, along with the “GET” and the resource you want, your browser sends a load of *headers*.

The HTTP spec says that each request begins with the verb, the resource, and the HTTP version. Next comes headers. Each header begins with a field name, say, “First-Name”, then a colon, and then its value, say, “Gabriel”. The browser can choose to send as many headers as it wants, each on its own line, and the server will get all of them though it might ignore unexpected ones. Here’s the first header from my request:

```
Host: www.cnn.com
```

This tells CNN’s server that my browser is expecting the resource `/blah/something-about-bears/` related to `www.cnn.com`. Importantly, this doesn’t change where my request is sent. Before this request, my browser looked up the IP address of `www.cnn.com` and saw it belongs to `157.166.240.11`. It then sent this `GET` request to that server.

So why is my browser telling the CNN server its own name? Because one server can host multiple websites. If `157.166.240.11` also hosts, say, `www.theonion.com`, and both sites have a `/journalistic_integrity.html` resource, then telling the server to `GET /journalistic_integrity.html` is ambiguous. It won’t know whether to return the page saying stories are only loosely based on reality and are meant to be entertainment, or whether to return The Onion’s.

The takeaway here is that sites with completely different domain names can live on the same server. In fact, this is the case with tons of sites these days. Amazon offers a service called [EC2](http://aws.amazon.com/ec2/), which has at one time or another been used by reddit, netflix, dropbox, zynga, and lots, lots more. So, even though those are all completely separate companies, visitor’s sent their GET requests to web properties owned by Amazon each time.

Okay, moving on. Now a few boring headers (I’m skipping around because order doesn’t matter):

```
Connection: keep-alive
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip,deflate,sdch
Accept-Language: en-US,en;q=0.8
```

This is just some technical mumbo jumbo to tell the server what sort of capabilities your browser has, so it knows how to most efficiently return the data. This has a privacy implication related to your browser’s fingerprint, which I’ll get to later.

And now the good stuff.

```
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1521.3 Safari/537.36
```

Here my browser is telling CNN a surprising amount about itself and my operating system. Why should CNN know that I run OS X 10.8.3? If it’s the most recent version, it might mean I have a large disposable income, so the site I’m at could choose to show me more expensive prices. Or, maybe it’s an out of date version with a security vulnerability in it, in which case I’m stomping about the internet yelling to every server I come across: “Hey, look at me! I can be exploited!”

```
Referer: http://www.cnn.com/
```

This header indicates the page you’re coming from, if you clicked a link. In this case, I clicked a link on CNN’s home page to the bear article, so my referer (note: this header is actually misspelled in the spec, so most people refer to it by its misspelling…) is cnn.com. That’s fine, but there are some privacy implications for 3rd party requests (which I’ll get to), or clicking a link to another site. In particular, if you Google/Bing/etc something, and then click a link in the results, the site you land on will see that you came from Google/Bing/etc and *often the specific search you did*. I’m going to Bing, “my testicles are itchy”, click a link, and see what referer my browser sends:

```
Referer: http://www.bing.com/search?q=my+testicles+are+itchy&go=&qs=n&form=QBLH&pq=my+testicles+are+itchy&sc=0-19&sp=-1&sk=
```

You’ll see in there that it’s clear I searched “my testicles are itchy”, clearly indicating this is a problem I’m suffering, and not, say, a research article I’m writing or something else. So, that leaks a bit more information than you may intend to (obviously, just by visiting that page, one could deduce *likely* reasons for having done so, but this makes it a bit more definite.)

```
Cookie: ug=51ab9a100805d30a3d146b12f11960b7; ugs=1; optimizelyEndUserId=o...
```

And lastly, the cookie. This is how a site remembers you from click to click, or when you come back the next day after logging in. The site sends back a cookie in one of its responses, and then your browser gives the cookie back on all subsequent loads. Importantly, it associates the cookie with the domain of the site that gave it to you, and always sends all relevant cookies with each request. This will matter with 3rd party requests in just a moment, you’ll see.

* Panopticlick
* RequestPolicy
* CookieMonster
* NoScript
* RefControl
