# Frequentist AB Testing

## A/B Testing

The process of providing two or more different experiences across two or more subgroups of population. This goal is to measure the change in behaivor of the subgroups upon receiving the respective experiences.

For instance, This can be applied to:

- A recommendation algorithm.
- UI changes
- Demand forecasting biewrs of a new release
- ML-web based caching

Some independent variable to measure this changes could be:

- Increment profit or revenew
- number, rate, or probability of ads clicked.
- listening screen time

And used to add Directonality of dependent variables:

- Like anticipating multiple changes to another changes that can make a lose.

We can select the experiment participants:

- Country
- New users/ longterm users
- web/app

Then we form an Hypothesis:

If we replace X with Y for some set of users `[a,b,c, ...]`  will go `[up/down]` and some `[invariants]` won't change.

So then we can measure the treatment experience (the new one) and the control experience (the current one) to see which one is better. 

For the Freuent A/B testing you start with a baseline metric. Then define the target changes that can beat the costs of running this experiement to take care of our costs. 

## A/A Test

An A/B test which the experiences are identical to one another. This is done to an effort to determine statistical validity of the A/B tool, the metric being monitored, and the analysis process being used.

## User Agent

An identifier used to describe the software application which a user is using to interact with another software application. For isntance, an HTTP request to a website typically includes de User Agent so the website knows how to render the webpage.

## Session ID

A unique identifier asigned to a user to keep track user's connected interactions. For instance, a session may include a user logging in, purchasing an item, and logging out. Here, the session ID would be used to reference the group of those three interactions. This session ID can be stored in the user's internet browser as acookie.

## Cookie

A small piece of data stored by a browser which indicates stateful information for a particular website. For isntance, a cookie can be stored in your browser after you log in to a website to indicate that you are logged in. This will stop subsequent pages to ask you to log in again.