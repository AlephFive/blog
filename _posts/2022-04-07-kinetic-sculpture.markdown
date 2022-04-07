---
layout: post
title:  "Planey McPlaneFace"
date:   2022-04-06 01:00:14 -0500
categories: art
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/5N8ggmoUmLg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

For my class "Creative Embedded Systems", I was given an ESP32 microcontroller, two servo motors, and two DC motors. I was tasked with creating a kinetic sculpture using those components. I teamed up with Emily Ringel to create this piece of art.

We started out by envisioning an outline of what we wanted. I had a lot of Amazon boxes laying around, so we decided that we would use this material to build our sculpture. We then realised that our sculpture could relate to Amazon as a company. Amazon has tried to build delivery drones for a few years now, though nothing seems to have come to pass yet. We wanted to parody the Amazon delivery drone project by building our very own delivery drone.

The resulting kinetic sculpture has propellors in the front for propulsion, and servos in the back controlling the angle op control surfaces (elevator and rudder). The resulting plane can (almost) fly!

![plane](https://miro.medium.com/max/700/1*UWeiESU62Dr3_E9IWOIZ4Q.jpeg)

![Plane_open](https://miro.medium.com/max/700/1*4DswH9LDBM2T4CO9fM4QPw.jpeg)

### Implementation
The plane consists of a triangular fuselage containing all the ESP32 and wiring, a front wing for lift and propellors, and rear control surfaces. I was in charge of implementing the rear control surfaces, while my partner implemented the front propulsion system. To aid design, we decided to separate the two systems and to control each individually using separate ESP32, while still connecting them to the same Wifi network and command server. The server hosts an API that returns a true/false statement depending on if the systems should activate.

For my rear control surfaces, I controlled two servos which connect to aerodynamic surfaces. The elevator is simply attached to the servo directly using a paperclip. However, the rudder is much more mechanically complex. I designed a pushrod system to control two rudders simultaneously using paperclips soldered together.

![Plane_servo](https://lh3.googleusercontent.com/o61oSMelymStLY6HNdS1g5CialysszR1DW95Ql_QuhDoKGVmuFVxYvtb9xy86UeBQojGaqZcmXlO_nMjNTm4goRdwV6-zMPqWjkvlQ_6Ux97xtLn0kPCThyEfp1fty6GEH_m4RRg9hg_aUK9SBVfgdElqv6r0zy7s8EJWNDRpMAmDwAAqSGa3FSuMGuxuJvrvmAqg6KjKKuPgWHguz6NEZapwLVIwmbMuGogRlNAHXZU8wC8oP7ZgPC1vFG17ehaHmvf2pAVYcwOgXyjdyf9M4unMKPd5naXW4mXJ3dwGkTAatjqflma6dviGztLDjZN9xmwNCwtTCB5nFsAYLmlJaFkR8mivgLQhi6mVlqqKJ80qn7XfSeZWfYrZQQ5cW4-n0Vf3UL7qx6O-qFdC3-Pn2JA9KJoGD2EZoZ4IFbH8CbNxNViWeCK0hjHq82__YZip-UGtG33lZ3VtVuY7VrJRTSPFtMhMqIfGWN-U66R0Ou-urcvpLyenrWoMix5qGSTFLK-WIijr7VHOMxB5Gg36hRT9xWsY3UjZGPspSbYJoqwBos6GlZJst5FPmh3GaFGD4mxZtTwFKBeNe18fmsj_OfFUBmBqCl3Yj4WWCXJh4Qa-Fbw4Mgc4-y1vGW9zS2yUauTPZsrY39xcEiIqtTLDtiWuJJn1XKUVr_K1m5LiA4ZzbYc5ASGaviLiEAx_0yoVKy2eb5hdK0dvotzfoBLiemItNSR-Pg1iKfLCjMR_bxyqs3qUXAEXIic_IdoNpRkM95W7G5L_7RKMxg5bXaJ2X9lgFzpPmM0cRsf=w1206-h904-no?authuser=0)

Structurally, the plane was held together by hot glue, and the body of the plane was held up by wooden q-tips. 

The software architechture of the flight control code is as follows. The ESP32 runs two threads simultaneously. The first thread connects the the server and, when connected, polls the server API in a regular interval. If the server returns false, the control surfaces are set in the default position. Otherwise, the servo motors are commanded to go to a random angle every second.

### Implementation Challenges
In terms of implementation challenges, we encountered a few challenges.

Firstly, my partner encountered problems with 3D printing the propellers, with the support material removal leading to damage. We solved this by changing to a propeller design that did not need support material. The front DC motors were also underpowered due to being connected directly to the ESP32. Additionally, I initially was using hot glue to secure the paperclip pushrod, but it broke easily. This was fixed by soldering paperclips together.

The code for the piece, as well as instructions on how to run it, can be found [here][codebase]


[codebase]: https://github.com/AlephFive/ESP32_flight_control