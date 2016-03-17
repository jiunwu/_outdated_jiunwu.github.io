---
published: true
title: Marketplaces
layout: post
tags: [Stripe, Stripe, Connect, Node]
categories: [Payment]
---
To build a marketplace in 2015 could be relatively easiser than past.
Since [Stripe](https://stripe.com/) updated the "Stripe Connect" around March,
now we can basically allow people accept credit card payment from others
in few steps with Stripe API.

[blog link](https://stripe.com/blog/the-new-connect)

Therefore,
how to build a simple marketplace or online shop ?
I found some projects on Github quite helpful.

Stripe Shop

[link](https://github.com/stripe/shop)

This single page shop was created by Stripe; an official example.
 
From Strip's official documentation, you could see there are always
four languages: ruby, python, php and node.

I personally prefer node.js, so I only introduce node projects here:

Stripe Charge Example

[link](https://github.com/mjhea0/node-stripe-charge)

An example demonstrated how to build a web app with
user login/registration, admin console, CRUD with mongoDB, REST API.

Stripe Charge Example

[link](https://gist.github.com/briancollins/6365455)

A nice example, just one page 80 lines HTML file,
so you can image what you have to do is customized your own CSS style,
and then put it into the views in your Node applications.

Until now,
the essential steps are:

1.  setup a strip account and get the API keys ( 5mins )

2. setup a server-side code handling the token from credit cards and charge

3. setup a client-side interface no matter in mobile app or website( 5mins ). 


Step 2 is also easy, the node backend is extremely easy:
[doc](https://stripe.com/docs/tutorials/charges)

```javascript 

var stripeToken = request.body.stripeToken;

var charge = stripe.charges.create({
  amount: 1000, // amount in cents, again
  currency: "eur",
  source: stripeToken,
  description: "Example charge"
}, function(err, charge) {
  if (err && err.type === 'StripeCardError') {
    // The card has been declined
  }
});

```


I tested it in my android app, Stripe android SDK directly charge the payment
without even the node backend.

With Express, the Stripe Connect codes like these:

```javascript 

// charge, Stripe Connect
app.get('/charge', function(req, res){
    var CONNECTED_STRIPE_ACCOUNT_ID = 'put the id here';
    var TOKEN = req.query.token; 
    stripe.charges.create({
      amount: 1000,
      currency: 'eur',
      customer:' ', // if you are not managed account
      source: TOKEN
    }, {stripe_account: CONNECTED_STRIPE_ACCOUNT_ID});

});

```
