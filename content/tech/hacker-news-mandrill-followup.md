+++
date = "2016-03-03T16:58:29+08:00"
title = "Hacker News Mandrill Followup"

+++

# Hacker News Mandrill Followup

*[Blog readers: this was an email I sent. Since the info was valuable, I figured I’d put it live, too, in case people searching come across it.]*

---

Hi everyone,

This is the promised Mandrill email followup you signed up for [here](https://news.ycombinator.com/item?id=11173325). (If you did not sign up, sorry! It was probably a typo from someone else, but don’t worry — I won’t send anymore emails.) In the end I got 354 signups.

Amazon and SparkPost proactively reached out to me, the others I submitted a support ticket for or found myself. Here are the responses in the order I received them:

## Amazon SES (Simple Email Service)

They put together a little [Welcome, Mandrill Customers!](http://sesblog.amazon.com/post/Tx9AXP03VIZDLH/Welcome-Mandrill-Customers) post which in addition to the usual “Getting Started” stuff at least mentioned some of the differences between their API and Mandrill’s.

## SparkPost

Provided a [Mandrill Migration Guide](https://www.sparkpost.com/mandrill-migration-guide) which among other things indicates they increased their free tier to 100k emails/mo. and they’ll honor your Mandrill pricing. They also have a walkthrough of migrating from Mandrill to SparkPost on heroku (if you’re using SMTP). They also mentioned they have a [community slack channel](http://slack.sparkpost.com/) for any questions.

## Sendgrid

I received CEO Sameer Dholakia’s blog post [Hey Mandrill Customers — We’d Love the Opportunity to Serve You](https://sendgrid.com/blog/hey-mandrill-customers-wed-love-the-opportunity-to-serve-you/) and this [overview of their pricing](https://sendgrid.com/marketing/mandrill-alternative), which includes a 10% discount for Mandrill users. They also sent me a [“How-To” migrate guide](https://sendgrid.com/blog/how-to-migrate-from-mandrill-to-sendgrid/) comparing their API and terminology with Mandrill.

## Mailgun

[Migrating from Mandrill to Mailgun](http://blog.mailgun.com/migrating-from-mandrill-to-mailgun/). Despite the title, it’s mostly about who they are and how they work. They do mention that “Most of the concepts supported in the Mandrill API are also supported in Mailgun’s API” and that if you’re using Mandrill’s SMTP integration it should be pretty easy to switch.

## Elastic Email

Elastic Email sent this [fairly basic landing page](http://elasticemail.com/post/where-to-move-from-mandrill) which explains their service.

## sendwithus

sendwithus emailed me, but because they’re a layer on *top* of Mandrill (and others), had different information. This [Important News for Mandrill Customers](http://blog.sendwithus.com/mandrill-announcement/) post was pretty informative and actually includes a number of the same links in this email. They also included this general [Which Email Service Provider Should You Use?](http://blog.sendwithus.com/which-email-service-provider-should-you-use/) post and this [surprisingly informative guide](https://support.sendwithus.com/templating/mandrill_conversion/) comparing Mandrill templates to the Jinja2 templating language they use.

## Postmark

Responded to my email saying they’d send something, but never did. I found this [Migrating your Mandrill Heroku add-on to Postmark](http://support.postmarkapp.com/article/1003-migrating-your-mandrill-heroku-add-on-to-postmark) guide on their support site, though. **Edit:** they contacted me and provided [Get 100,000 free credits when you setup DMARC for your account](https://postmarkapp.com/blog/100-000-free-credits-to-help-us-support-dmarc), [Why Postmark?](https://postmarkapp.com/why), and [Getting Started with Postmark](http://support.postmarkapp.com/article/1002-getting-started-with-postmark).

## Mailjet

Never responded, but I saw on sendwithus’s post above this [Welcome On Board, Mandrill Customers](https://www.mailjet.com/blog/mandrill-alternative/) post.

---

Well, that’s it. I’ll destroy the Google Form and delete all your email addresses now. Would love to hear what y’all ended up deciding on, though, so please feel free to reply back.

Lastly, I would be remiss if I didn’t take my one opportunity here to say my start-up [CoachUp](https://www.coachup.com/) in Boston is looking for full stack web devs — let me know if you’re interested! Also, I guess [follow me on twitter](https://twitter.com/losvedir)? I tweet only occasionally, mostly about tech stuff, and plan to spend more time with Elixir and Rust this year.

Cheers,

Gabe
