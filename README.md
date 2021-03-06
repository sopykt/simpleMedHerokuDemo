[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/cowie/simpleMedHerokuDemo)

Simple Demo Org - Heroku Connect (HLS/Medical Edition)
======================

This is a straightforward demo to show off how you can combine the best of Heroku and Force.com into a multi-part App Cloud demo. This requires some flexibility and use of potentially non-free elements of Heroku, and is mainly for Salesforce SE's - If you are a prospect/customer and would like to see this all in action, please reach out to your friendly neighborhood Salesforce representative.

This will require a total of ZERO code to implement. Point and click, son. Components we need on Salesforce? Nada but the standard stuff. Components we need on Heroku? Postgres, Node, handful of node libraries, and Heroku Connect, everything autodeploying.


Script/Story
-------------
Today we're taking a look at what it looks like to develop a custom app with the App Cloud. In our scenario, we have our internal folk all over Salesforce, which they use for things like rounding apps, care planning, scheduling, the works. There has been a recent push for custom mobile applications as a way to get the Ask-a-Nurse hotline to scale out to millions of users. We want to do some basic stuff, sharing information, collecting biometrics on IoT devices, but also push information out, in this case, that an Influenza breakout is occurring, and alerts should be pushed if users are within specific geographical regions. We want to collect information on counts of people in these areas reporting symptoms for analytics and followup, but most importantly, identify ahead of time those who are part of high risk populations reporting symptoms, so we can get in front of them and potentially save their lives.

Salesforce is phenomenal at workflows once we've identified these high risk people, but the problem we have is serving up a page that, in the event of a global epidemic, may get extremely high spikes of usages in tens to hundreds of millions of concurrent users. For that, Heroku is a fantastic solution to deploy instantly, and scale rapidly to handle even those levels of users, and Heroku Connect is the glue that ties the two together, making it easy to pass the high risk patient information over to Salesforce for follow-up, according to our existing workflow rules.

The integration and the workflow rules on the Salesforce side are all done through point and click tools easy enough for Business Analysts and Admins to work on, freeing your developers to build specifically the elements that innovate: The mobile app, its featuresets and intelligence, as opposed to setting up piping for data to flow across systems. It's a faster way to develop the most simple to complex application, for an audience of dozens to hundreds of millions.

Today, we're going to set up and deploy that application, along with wiring up the integration, in minutes. No code, no command line.

 

Setup
-------------
### Prep
* Get a copy of CRM for Hospitals Demo Org
* Sign up for a Heroku license. 

### Install - could be part of the demo. It's nerdy.
At this point, you can either start the demo now, and show the power of instant deployment, or run this step ahead of time. 
* Hit the Heroku Deploy button above to create a net new Heroku app, no command line required.
* Name your app something you'll remember if you've got a bunch of em. 
* Go into your CRM for Hospitals Demo Org, and find the Helen Highrisk contact ID. Copy this, and paste it in the box on the heroku page under Config Variables called 'HELEN_HIGHRISK_ID'. 
* Click the 'Deploy for Free' button at the bottom to start the deployment.
* Click the 'Manage App' button at the bottom - this is your dashboard for the app. Click 'View' to load the actual app itself in your browser.

What you're doing right now is the equivilant of a 'git push heroku master' command, but instead of deploying from code on your local machine, you're deploying direct from my code here. This is a step most devs would take after doing initial testing and dev on their local box and it's time to get started testing in a real environment. 


(OPTIONAL)
* Clone this repository locally, use Heroku Toolbelt to push to Heroku.
Looks cooler, requires command line, only do it if you know what you're doing.

### Demo
* Special Note: If you set this all up days ago and haven't run it since then, run your app once by going to whatever.herokuapp.com. For the free dynos, Heroku will sleep your app, causing a considerable lag time at the first run if it's been awhile. Trust me on this one.



(HC - You can do this beforehand if you have a business user / lack of time)
* After clicking 'Manage App' on the last page (Or, if you didn't, or forgot, or that was days ago, going to https://dashboard.heroku.com/apps and clicking on your app), you'll have your management page. 
* Click on "Heroku Connect" here
* Click on 'Begin Setup' to complete provisioning.
* Click 'Next' (On this page, you're naming the schema in the Heroku database for the Salesforce data. Salesforce is default, and that looks good enough to me.)
* Click "Authorize" - You're now doing an oAuth login into Salesforce so it can get to your datas, your precious, precious datas. Log in and hit allow.
* Create a mapping between Heroku and Salesforce by hitting 'Create Mapping'.
* For the demo, click on Case. 
* Before mapping fields, at the top, MAKE SURE TO CHECK 'Write to Salesforce any updates to your database'.
* Map the following fields (You can do more, but at the very least, do these): 
** ContactID, Origin, Patient__c, Priority, Subject
** Click Save
* You've now mapped your databases. 


(Actual Demo)
* Now it's actually time to demo the app. If you're short on time, you can do the (HC) part early, and just show this. If you do that - 
* Open up Salesforce. Show Helen Highrisk, do whatever demoy stuff you wanna do here before showing this off. Make note of her 'Cases' related list.
Now I flip over to Helen Highrisk's point of view.
* Open your app, it's whatever-you-named-it.herokuapp.com. You can do this on your phone for extra points or on your browser.
* This app is simulating a known user - Helen Highrisk, using information drawn from SFDC and Heroku. It could be a general unauthenticated page too, but just go with it here.
* Note the 'Influenza Breakout' bit at the top, click on 'Report Symptoms'. The rest of the page is fluff.
* Since we know who Helen is, we don't need to ask a bunch of identifying information, but for Influenza we want to doublecheck a few qualifying factors that would make her high risk. 
* Tap one or more of the high risk elements, then hit submit request.
* Index page will change, showing that stuff's been sent.

(HC)
* Open up your Heroku Connect dashboard, and wait 10 seconds for the poll, or hit 'Poll Now' button.
* Show Helen Highrisk's cases - You've now got a new one about the Influenza Outbreak. At this point, wire it to whatever workflows you'd like.

## POST DEMO
* I recommend highly you wipe out the heroku app you built for the demo, so you don't end up with 300 apps in your list and get confused in a future demo. 
