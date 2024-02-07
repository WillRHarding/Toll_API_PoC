# Toll_API_PoC
A PoC for a web app that retrieves the toll cost using the scenario name as a parameter in a GET request. It can be found ![here](https://www.wharding.com). 

The site started out as part of the Cloud Resume Challenge, an entry level project designed to expose participants to AWS services and provides a high-level guide on how to carry it out. The visitor counter in the footer is only remaining part of the challenge on the site. The more interesting part (at least to me) is the Pin Routes scenario toll cost calculator. We've had clients come to us and ask for tolls to be calculated as part of the main solution. It's possible but resource heavy to develop, but I've wanted to create a web app that acts as an add-on for Pin Routes for some time. Only since I started learning about AWS have I realised it's possible with the current resources we have, and so I've been working on a proof of concept - partly to show we could do it, partly to prove _I_ could do it.

**Toll Calculator**

This my first project using 3rd party APIs. Toll Guru are a company that provide toll costs of a route given to them. Pin Routes can provide the routes. I just needed to hook them up and present the answer. Security was a concern from the start - I'm working with demo data and have set it up in a way that only a specific scenario can be used. There is no possibility of client data or PII being exposed to anyone outside of CACI and no data from scenarios is saved. I'm also disabling the API when it's not being demoed.




**Visit Counter**

The visitor counter is comprised of a GET request that triggers a Lambda function to add a record to a DynamoDB table and return the count. For some extra flare I set up a domain I've had for a while using a DNS 
![image](https://github.com/WillRHarding/Toll_API_PoC/assets/138053790/f8d49e11-84aa-4423-ad9a-36d816d1a65c)

