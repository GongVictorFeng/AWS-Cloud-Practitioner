# AWS-Cloud-Practitioner

## Before the Cloud 
Example 1 - Online Shopping APP
* Challenge: 
  * Peak usage during holidays and weekends
  * Less load during rest of the time
* Solution (before the Cloud):
  * Procure (Buy) infrastructure for peak load
    * the infrastructure would be idling during period of low loads

Example 2 - Startup
* Challenge:
  * It suddenly becomes popular
  * How to handle the sudden increase in load
* Solution (before the Cloud):
  * Procure (Buy) infrastructure assuming they would be successful
    * what if they are not successful

Challenges before the Cloud:
  * High costs of procuring infrastructure
  * Needs ahead of time planning (hard to predict the future)
  * Low infrastructure utilization
  * Dedicated infrastructure maintenance team (Startup usually can not afford)

## Silver lining in the Cloud
On-demand resource provision - also called Elasticity
* Advantages:
  * Trade "capital expense" for "variable expense"
  * Benefit from massive economies of scale
  * Stop guessing capacity
  * Increase speed and agility
  * Stop spending money running and maintaining data centers
  * "Go global" in minutes

## Regions and Zones
* Imagine that your application is deployed in a data center in London
* What would be the challenges?
  * Slow access for users from other parts of the world (high latency)
  * What if the data center crashes
    * Your application goes down (low availability)

Multiple data centers
* Let's add in one more data center in London
* What would be the challenges?
  * Slow access for users from other parts of the world
  * Solved: What if one data center crashes?
    * Your application is till available from the other data center
  * What if the entire region of London is unavailable?
    * Your application goes down

Multiple regions
* Let's add a new region: Singapore
* What would be the challenges?
  * Partly solved: Slow access for users from other parts of the world
  * Solved: What if one data center crashes?
  * Solved: What if the entire region of London is unavailable
    * Your application is served from Singapore

Regions
* Imagine setting up your own data centers in different regions around the world
* AWS provides 20+ regions around the world (expanding every year)
* Advantages:
  * Low Latency
  * Global Footprint
  * Adhere to government regulations
  * High Availability

Availability Zones
* Each AWS Region consists of multiple, isolated and physically separated availability zones
* Availability zones in a region are connected through low-latency links
* Each Availability zone:
  * Can have one or more discrete data centers
  * Has redundant power, networking, and connectivity
* (Advantage) Increase availability and fault tolerance of applications in the same regin 