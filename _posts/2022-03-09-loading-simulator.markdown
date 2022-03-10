---
layout: post
title:  "Loading Simulator"
date:   2022-03-09 00:39:14 -0500
categories: art
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/92kTHyFeEdk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

For my class "Creative Embedded Systems", I was given an ESP32 microcontroller, a potentiometer, a joystick, and a button. I was tasked with creating an interactive visualisation using those components. 

I started out by envisioning an outline of what I wanted. I often play games, and am often encountered with a loading screen. A loading screen is interesting as a concept in itself. Often ignored as an empty space between content and something undesirable and to be minimised, I wanted to explore the possibilites of this space. Additionally, I wanted to parody the various "Simulator Games" that have become popular in recent times, hence "Loading Simulator 2022".


### Implementation
The architecture of the project is as follows. Sensor data is collected by the ESP32, which is then sent to the computer as a string which is in a JSON format. The computer runs a JavaScript program that reads in the string and converts it into a JSON object, which is then used to control various elements on the screen. The visualisation is written using p3.js.

For the loading bar, I wanted the progress to get closer to 1, but never reach it (as a commentary on the length of loading times). Hence, I used a sigmoid function that approached that value asymptotically.

The contoller enclosure is made out of cardboard.

![PXL_20220310_053957084](https://user-images.githubusercontent.com/6265129/157605463-1f0cfcb0-42dd-4470-8b3b-6d4e4f52e94a.jpg)
![PXL_20220310_054018956](https://user-images.githubusercontent.com/6265129/157605483-61067e94-b514-43bd-8122-a84fa1742c05.jpg)

### Implementation Challenges
In terms of implementation, I encountered a few challenges.

On the ESP32 side, I encountered the issue of not having female-to-female connectors available to me, which would have made connections extremely easy. However, since they were unavailable, I had to improvise a solution that allowed me to connect components, but still allowed for easy disconnection. In the makerspace, I found some pin extenders and I soldered the sensors onto the male side. This way, when I connect the pin extenders to the ESP32, all the connections are in the right place.

![PXL_20220308_004816777](https://user-images.githubusercontent.com/6265129/157605340-35ca6939-bd29-403a-b6ce-4d86a95381b0.jpg)


On the Game side, I encountered the issue of the serial readings being often broken up into lines inconsistently, preventing the use of JSON.parse(). I solved this by writing a string builder that makes sure the resulting string is a valid JSON object.


The code for the piece, as well as instructions on how to run it, can be found [here][codebase]


[codebase]: https://github.com/AlephFive/ESP32_proj2