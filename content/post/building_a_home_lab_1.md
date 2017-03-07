+++
draft = true
type = "post"
categories = ["Blog"]
date = "2017-02-28T07:44:12Z"
title = "Building a home lab: pt 1"
tags = ["about"]
#description = "Building a home lab: part 1"
author = "Andy Downs"

+++

In my job I am lucky that I get to play with the new projects and products so I can get to understand them. This is great but sometimes running VMs on your laptop is not enough. While I can do a lot of testing in a public cloud, sometimes you need to see it happening on tin. I am pretty sure that most people who do jobs similar to me have some sort of home lab. These appear to range from a beefy machine under the desk to full on garage full of server racks, check out [Reddit](https://www.reddit.com/r/homelab/).

Well over a year ago my friend Dave started talking about building a home lab/cluster, he had been talking to his co-host of the [Roaring Elephant](https://roaringelephant.org) podcast about his set up and was looking to build his own. I'd been thinking about NUC based lab or secondhand workstations, so we decided to collaborate.

We set out the main requirements and started to haggle on which was more important and which we would compromise on. Luckily we had a similar set so there wasn't too many disagreements. The main things were :

* Quiet as possible
* 5-10 Nodes
* Low power usage
* All "contained" - Work with as few requirements on home network as possible
* Tidy - 1 Power 1 Network in/out
* Vaguely portable/extendable

It goes without saying that we would want it performant as possible, but speed/throughput isn't the use case. With these in mind our biggest discussion was about network ports, most of this was failure to count.

We settled on building using mini-ITX based system and set about working out how. We looked at a number of different boards and soon found that to keep the power wiring simple we wanted a DC jack in. After trialing a couple of boards and the ATX/DC adaptors options, the [ASRock Q1900DC-ITX](http://www.asrock.com/mb/intel/q1900dc-itx/) was our chosen. Vicious The main reasons over other boards is that it did all of the following :

1. Fanless
2. DC power
3. 16GB Ram
4. Quad Core

I'm hoping there may be newer boards a year on but we struggled to find any that could do the above. After a bit of to and fro we aimed for 8 nodes in what we were now referring to as the cluster. One of these would be a master and the other 7 workers.

We decided on 128GB SSDs as the best £/GB at the time with the master node having a bigger disk.

At that point it was on to the buying. Well creating a list, arguing about network ports, choosing LEDs and so on. It took a while for everything to arrive as we shopped around, for instance the supplier we found for the mother board was a good deal cheaper but could only supply 2-3 a time. When you are ordering 16 x of something it is work waiting. It ended up with piles like this  

![boxes!](static/boxes.jpg)

We came to the conclusion that we were going to have to create a custom "case" to house . I'd seen [Render Pockets](http://renderpockets.com) which is a great looking solution and a bit of an inspiration. A few of our requirements meant we to go a different way. With our "skills" wood seemed like the best material to work with. More on that in the next blog...
