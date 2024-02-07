# Toll_API_PoC
A PoC for a web app that retrieves the toll cost using the scenario name as a parameter in a GET request. It can be found [here](https://www.wharding.co.uk). 

The site started out as part of the Cloud Resume Challenge, an entry level project designed to expose participants to AWS services and provides a high-level guide on how to carry it out. The visitor counter in the footer is only remaining part of the challenge on the site. The more interesting part (at least to me) is the Pin Routes scenario toll cost calculator. We've had clients come to us and ask for tolls to be calculated as part of the main solution. It's possible but resource heavy to develop, but I've wanted to create a web app that acts as an add-on for Pin Routes for some time. Only since I started learning about AWS have I realised it's possible with the current resources we have, and so I've been working on a proof of concept - partly to show we could do it, partly to prove _I_ could do it.

**Toll Calculator**

This my first project using 3rd party APIs. Toll Guru are a company that provide toll costs of a route given to them. Pin Routes can provide the routes. I just needed to hook them up and present the answer. Security was a concern from the start - I'm working with demo data and have set it up in a way that only a specific scenario can be used. There is no possibility of client data or PII being exposed to anyone outside of CACI and no data from scenarios is saved. I'm also disabling the API when it's not being demoed.

![image](https://github.com/WillRHarding/Toll_API_PoC/assets/138053790/33e223b6-96c3-4f5f-9be4-820a01568638)

I should say from the beginning - I am not, nor do I want to be, a web designer. The site is bare bones and I got most of the HTML from ChatGPT. I just needed a front end to show that I could achieve what I set out. 

I started with the Lambda function. With help from Postman I set up the OAuth for Pin Routes and could request export data for the dev-testing environment by specifying the scenario name. 

Next was TollGuru. I've used them before and they give a free trial to play with. I formatted the Pin Routes export such that I could send off the list of places, in order, to TollGuru, and receive the toll cost. Then it was a case of sending off a response from the Lambda function.

**The API**

I used API Gateway to configure the connections between my site and the Lambda function. I originally had set the API to a POST, my thinking being that I was submitting a scenario name, therefore it counted as a POST. Tinkering wth CORS for hours (or days...) eventually led to a realsation that I can use the scenario name as a parameter in the URL, and switched the API to a GET, sidestepping CORS. 

**Other Services**

Every new service I encountered was like climbing a mountain. I had to learn how to add layers to Lambda functions to add a package, configure API logging for CloudWatch, create a GitHub repo to store the web page. There's so much more to be done before it could be considered a complete proof-of-concept, but I'm proud of what I've achieved given where I started.

**Visit Counter**


As a bonus, the visitor counter is comprised of a GET request that triggers a Lambda function to add a record to a DynamoDB table and return the count. I's what's left of the Cloud Resume Challenge I completed - a structured project for complete newbies.
![image](https://github.com/WillRHarding/Toll_API_PoC/assets/138053790/f8d49e11-84aa-4423-ad9a-36d816d1a65c)



