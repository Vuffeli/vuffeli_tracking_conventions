# VuffeliTrackingConventions
A markdown project describing our use of tracking utm tags in Vuffeli ApS

# TL;DR

>## ALL UTM TAGS SHOULD ALWAYS ONLY BE LOWER CASE

------

# [Click here to go to Google link builder](https://ga-dev-tools.appspot.com/campaign-url-builder/)

------

## Facebook link should look like this:

>https://vuffeli.dk/?utm_source=facebook&utm_medium=cpa&utm_campaign=christmas&utm_term=ll%280-3%25%29-purchases_26_08_2019&utm_content=ellie

This tells Google Analytics everything we need to know about the effectiveness of an ad.

It tells us that the visitor came from __facebook__, that it was a __cpa__ ad, that the campaign was made for __christmas__ that the audience was __ll%280-3%25%29-purchases_26_08_2019__ (url encoded version of "ll(0-3%)-purchases_26_08_2019" encoding and decoding can be done online [here](https://www.urlencoder.org/)) and lastly the specific ad was __ellie__.

When writing the utm tags for an ad it is important to include all tags as facebook seemingly does not create any automatically.
The input field for tracking tags under the ad called "Webadresseparametre (valgfrit)" should contain the following to create the desired link
```
utm_source=facebook&utm_medium=cpa&utm_campaign=christmas&utm_term=ll%280-3%25%29-purchases_26_08_2019&utm_content=ellie
```
------
## Email links should look like this:

>https://vuffeli.dk/?utm_source=campaignmonitor&utm_medium=email&utm_campaign=onboarding&utm_term=newcustomersegment&utm_content=bottom_link

It tells us that the visitor came from __campaignmonitor__, that it was an __email__, that the campaign was made for __onboarding__ that the segment was __newcustomersegment__ and lastly the specific link was __bottom_link__.

------
# /TL;DR

# What is a utm tag?
>UTM parameters are simply tags that you add to a URL. When someone clicks on a URL with UTM parameters, those tags are sent back to your Google Analytics for tracking.

A URL containing UTM tags looks like this:
https://vuffeli.dk/?utm_source=facebook&utm_medium=cpa&utm_campaign=ellie&utm_term=hunde%2Bmad&utm_content=logolink#top

First we break down the URL into its constituents.

## Protocol - https://
------

This is the protocol, it tells the browser how to connect to the website.
Traditionally we have two options:

- http
    - http is an insecure communication protocol that converts the data into packages and sends them over the internet to and from a website, to and from a browser whereas https is the secure version of this same protocol.

and 

- https
    - https works by adding transport layer security(TLS) to http thereby making it implausible for anyone to "read" the messages sent between the browser and the server.

## Domain -  vuffeli.dk
------

This is the domain, it refers to a record in a registry that ties a domain name to an internet protocol(IP) address.

What is actually happening behind the scenes is that the browser is asking the domain name service(dns) what IP corresponds to that particular domain name as a browser always has to connect to the server via an IP address in the end.

The server will for example be asked
 - what is the IP address of vuffeli.dk

and will answer with something like
 - 192.168.1.1

 ## Path - /
------

The "/" after the domain is actually the "path" corresponding the "location" on the website.
A single "/" just corresponds to an "empty" path that is almost always the front page of a website.

## Query string - ?utm_source=facebook&utm_medium=cpa&utm_campaign=ellie&utm_term=hunde%2Bmad&utm_content=logolink
------

The query string as it is called is everything that comes after a "?" but before a "#".
It consists of "key" and "value" pairs where a "=" is in between the key and value.
Each pair is in turn seperated by a "&" character.
It was originally used to send data from a form to a server allowing browsers to send things like search queries to the server and getting a search result response.

If we split it up into pairs and then keys and values we get the following:

```
- utm_source=facebook
    
    - key is "utm_source"

    - value is "facebook"

- utm_medium=cpa
    
    - key is "utm_medium"

    - value is "cpa"

- utm_campaign=ellie
    
    - key is "utm_campaign"

    - value is "ellie"

- utm_term=hunde+mad
    
    - key is "utm_term"

    - value is "hunde+mad"

- utm_content=logolink
    
    - key is "utm_content"

    - value is "logolink"

```

note: the %2B between "hunde" and "mad" in "hunde%2Bmad" is actually a URL encoded "+" sign.
    The reason we url encode is so we can have signs traditionally used in the path part of the url used in the query string as well without the browser getting confused about what belongs where.

In most cases adding an arbitrary extra query string will not harm anyones ability to use a link as it is by most servers considered "extra" data of less that critical importance.
This means that as well as containing all the above pairs we might add "&banana=yellow" to the query string before the "#" without any serious consequence.

The reason for our use of query strings is to facilitate tracking of user behavior on and around our websites.

> __Therefore it is critical that as many links as humanly possible contain as many utm tags as possible.
When a utm tag is present on a link and that URL is tracked using Google Analytics it allows us to see all the data with which the clicked link was tagged.__

The following utm tags are valid in the eyes of Google.

1. utm_source
2. utm_medium
3. utm_campaign
4. utm_term
5. utm_content

While the first three are __required__ for a valid tracking link the last two can be omitted without Google Analytics taking issue.

## utm_source

The utm_source tag is meant to tell Google Analytics from where the visitor came.
Example values of this are
```
facebook
google
bing
newsletter
orderconfirmation
inboundmarketing
welcomeemails
```

## utm_medium

The utm_medium is meant to tell Google Analytics what kind of medium was used.
Example values of this are
```
cpa
cpc
banner
email
ad
```

## utm_campaign

The utm_campaign is meant to tell Google Analytics what marketing campaign the link was in.
Example values of this are
```
spring_sale
christmas
aeldresagen
```

## utm_term

The utm_term is meant to tell Google Analytics what specific words were searched for.
Example values of this are
```
hunde+mad
vuffeli+jul
vuffeli
ellie+hundemad
5+gode+raad+til+kræsenhed+hos+hunde
```
while the original meaning of this tag is to capture keywords related to search I propose that we instead use it to signify the audience used so that valid example values instead become.
```
CA-Checkouts_15_08_2019
CA-AddToCart_15_08_2019
CA-Web_Traffic_15_08_2019
LL(0-3%)-Purchases_26_08_2019
LL(3-6%)-Purchases_26_08_2019
LL(6-10%)-Purchases_26_08_2019
```

This allows us to see in Google Analytics what audiences are most effective and what their behavior is when on our website.

## utm_content

The utm_content is meant to tell Google Analytics what specific content was clicked.
Example values of this are
```
logolink
textlink
hoverlink_top
bottom_cta
```

While I think we should still use this broadly I propose that in cpa and cpc marketing contexts we use it to specify the precise ad that was clicked.
Examples of this are
```
Thomas
Ellie
Sofus
Collage
Lager
Holly
```

Using this in combination with audience as term we get the ability to see specifically what audiences a specific ad performed well on and what audience did not like aforementioned ad.

## Hash - #top
------

The hash is sometimes used in conjunction with javascript to convey things like scroll position.

It is not important to know or understand for our case.