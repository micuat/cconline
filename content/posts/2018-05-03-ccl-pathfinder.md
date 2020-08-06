+++
author = "Naoto Hieda"
title = "NOVA: Choreographic Coding Lab + Pathfinder"
date = "2018-05-03"
description = "report"
tags = [ "report", "ccl", "workshop", "pathfinder" ]
+++

![](/images/2018-05-03-ccl-pathfinder.jpg)

The first edition of [NOVA Festival](http://www.pointhub.ro/nova) was organized by Point theatre in Bucharest, Romania from April 20 to 29. I was invited to the festival to give a workshop about choreographic coding and Pathfinder with Christian Mio Loclair, who created Pathfinder at the first Choreographic Coding Lab (CCL). It is the first dance-tech festival in Romania, and both international and local artists presented talks, workshops and performances to stimulate the local community. There was NOVA Lab, which is a week-long workshop for local media artists and dancers, and the festival closed with performances of NOVA Lab participants. Some of them as well as professional dancers came to our workshop, which created a unique mixture of skill sets.

If you do not know about Pathfinder, please take a look a the following video by onformative and Mio to get the idea. In short, Pathfinder shows a sequence of geometry whose size, position and shape are randomly determined. Instead of receiving inputs from a dancer, these geometric patters are intended to inspire the dancer. I met Mio last year at CCL in Amsterdam and since then I restructured and [open-sourced](https://github.com/micuat/Pathrefinder) the code.

{{< rawhtml >}}
<iframe title="vimeo-player" src="https://player.vimeo.com/video/112040292" width="640" height="360" frameborder="0" allowfullscreen></iframe>
{{< /rawhtml >}}

We started the workshop with algorithmic choreography, which Mio calls as “human particles” or a “particle dance.” Participants were asked to imagine a virtual plate balanced at the middle of the stage, and they traveled the space constantly not to tip the plate. It is not so difficult until one of them was asked to disturb the balance. Then we did some exercises with a partner; we started with a rule that one has to stare at a partner while moving. But since a few pairs are moving at the same time on the stage and we often lost track of the partner, we extended the rule to say loudly that if I have more time, I will find another partner. We also tried non one-to-one mapping; we first picked a partner without saying and then we followed the partner. Since two people can choose the same partner, this created a complex relational structure resulting in an interesting flocking behavior. Mio mentioned that the rules must not be too obvious to the audience, but if it is too complex people will not understand at all.

These practices are not new in dance; however when we introduce the idea of algorithm, these practices mean more than a dance practice. During the workshop, as an example, I showed the particles that I coded.

{{< rawhtml >}}
<iframe width="560" height="315" src="https://www.youtube.com/embed/kLaub4aTmtM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
{{< /rawhtml >}}

These particles have simple rules; they attract each other until they collide, and when they collide, a strong repulsion force moves the particles away (by the way, this is inspired by physics of atoms). But you will notice that these simple rules create some sort of equilibrium at the end of the video. Similarly we found some choreographic rules for our bodies that creates a static state; for instance, in the balanced plate example, dancers will eventually stop moving until the disturbing particle is introduced. Also, in the following-partner example, when all the dancers chose the neighbor, everyone ended up running in a circle, just like particles finding an equilibrium state. The partner exercise includes not only a physics model but also pointers and references; finding a new partner can be seen as a null pointer exception.

![](/images/2018-05-03-ccl-pathfinder-2.jpg)

The second half of the workshop was about Pathfinder. We started with projecting Pathfinder on the floor and did a solo and a duet. Some created their own rules while moving with the generative visual, such as to jump when one sees a rectangle shape. Then, some of the dancers asked us if it is possible to make the Pathfinder interactive. The idea of Pathfinder is to move shapes in a random order so that one may find some transitions surprising; therefore, the original Pathfinder does not have any interactions. Nevertheless, I have done some experiments with sensors such as Interaxon Muse. Although it is a brain wave sensor, for the workshop, I only used the accelerometer for head orientation tracking, mapped to a 2D plane using Wekinator. One dancer wears a Muse, and the other dance with Pathfinder. Thanks to the nature of Pathfinder, geometric movements are not immediately affected by the sensor but rather follows movements in an ambient manner. Therefore, the interaction between the sensor and patterns are not obvious, which makes the dance interesting; as Mio mentioned before, the rules need to have adequate complexity and this sensor-Pathfinder interaction achieved it although it was not intentionally designed to do so.

The workshop was a great success and I appreciate the Point team to be so kind to offer us such an opportunity as well as their hospitality, serving tasty and healthy food to us everyday. Also all the encounters including the team, volunteers and artists were precious, especially it was great to meet Antoni and Mio again, which made me feel like a small CCL reunion. I am willing to come back to the festival next year.

Photo credit: Andrei Gîndac