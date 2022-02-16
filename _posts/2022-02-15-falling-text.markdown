---
layout: post
title:  "Falling Text"
date:   2022-02-15 10:39:14 -0500
categories: art
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/AR0eMbk_z5M" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

For my class "Creative Embedded Systems", I was given an ESP32 microcontroller and a prompt of "Generative Art", and tasked with creating a small section of a larger collaborative art piece that was displayed at Barnard College. 

I started out by envisioning an outline of what I wanted. To coordinate an overall structure for the collaborate art installation, a requirement was made the the individual ESP32 microcontrollers needed to display text. Hence, I became interested in exploring the deconstruction of text. I wanted to see what happens when a large block of text, with coherent and overarching meaning, behaved and intereacted as it was broken into pieces of words. I came up with the idea of having those words individually fall, as if affected by some directional gravity, and have the next word start falling as soon as the previous word hit the floor. I wanted it to feel like the words are disconnected from one another, yet still let some remanent of connection between them remain.

I then explored what text I wanted to be displayed. I decided on the introduction section of the ESP32 Wikipedia page. I liked it because, not only was it "meta", when deconstructed and displayed its vocabulary stood very well on its own, especially technical words such as "Xtensa", "RISC-V", and "low-noise". The text would fall as if drawn by gravity, and then instantly appear back at the top again, as if by teleportation, but this time in the form of another word. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/Er9rJSrpn1w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

I tested a few colours for the text, but yellow stood out most for me. I also experimented with font size, and ended up choosing a small font size. I wanted to show the deconstruction of paragraphs and sentences, rather than individual words into letters, hence the small screen neccessitated small font to avoid word-wrapping. This also had an unintentional, but welcome effect of drawing the audience closer, encouraging them to take in the detailed aspects of our installation. 

In terms of the physical aspects of the installation, each ESP32 was wrapped in paper card, and hung from the ceiling using black string. A lithium-ion battery was used to ensure the displays will last for a few hours.

<iframe width="560" height="315" src="https://www.youtube.com/embed/qzmGjLM0F00" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

On the technical side there were a few points of difficulty in developing with this hardware setup, namely the relatively sparse amounts of documentation for the display library.  Getting the text to draw without graphical artifacts was slightly difficult, but was I overcame it via trial-and-error. Example programs was indispensable in helping me create this project, and I encourage other artists to use them as reference when using ESP32 in their projects.

Overall I really liked the effect of the piece. The yellow contrasted nicely with the grey-blue background wall, and the variations in what my classmates did was really cool to see and I felt my piece complemented the overall installation well.

The code for the piece, as well as instructions on how to run it, can be found [here][codebase]


[codebase]: https://github.com/AlephFive/ESP32_miniproj