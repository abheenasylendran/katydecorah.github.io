---
title: Organizing a conference with node
category: notes
image: https://cloud.githubusercontent.com/assets/2180540/17576600/6ad2076e-5f42-11e6-8b3a-d2ca29823192.png
tags:
- Ela Conf
---

Last month I wrote about [Organizing a conference with bots](http://katydecorah.com/notes/ela-conf-bots/) where I set up Zapier zaps to keep the transactional pieces of Ela Conf moving.

Now that we have each proposal in its own GitHub ticket, the organizers and I decided that we would start reviewing proposals by using [Github reactions](https://developer.github.com/v3/reactions/) on each ticket: :+1: or :-1:. We'd also leave comments on tickets to discuss other ideas for a specific talk and leave ideas.

We ended up with 109 proposals. 109 tickets to review. I immediately saw the need for some help in the review process.

## Evaluating Github issue reactions

I wrote a script called `cfp-review` that:

1. Collects all `speaker` and `lightning talk` labeled tickets.
2. Fetches the reactions on the ticket.
3. Makes decisions based on reactions:
  + If the talk has 4 :+1: then change the ticket's milestone to "Four :+1:"
  + If the talk has 4 :-1: then change the ticket's milestone to "Send rejection email"
4. If we haven't left a reaction to a specific ticket, then assign us to it.

This script was incredibly helpful in sorting and reminding us to review.

## Fetching data from Github issues

I wrote a script called `cfp-to-csv` that:

1. Grabs all `speaker` and `lightning talk` labeled tickets. 
2. Parses the data in the ticket to get their first name, email, type of talk, and talk title.
3. Makes the data unique when needed. In some cases a speaker submitted more than one proposal. I used the email address and the key and appended titles together.
4. Formats the data and writes a CSV file to the repo. 

We were able to import that CSV file into MailChimp and send all of the women who submitted a proposal a personalized email thanking them for their work and letting them know when they'll hear from us.

## Creating Jekyll pages from Github issues

I wrote a script called `get-bios` that:

1. Grabs all `speaker accepted` labeled tickets.
2. Parses the data in the ticket and formats the data by creating yaml front matter and then adding their bio as the page content.
3. Creates a markdown file where the file name is `firstname-lastname.md` and is saved to the `_speakers/` Jekyll collection and the content is the data formatted above.

===

The groundwork for these scripts were recycled from internal Mapbox tools that I worked on with [Emily DuBois](), a very patient and gracious teacher <3.