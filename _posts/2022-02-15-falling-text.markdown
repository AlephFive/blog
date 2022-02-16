---
layout: post
title:  "Falling Text"
date:   2022-02-15 10:39:14 -0500
categories: art
---


<iframe width="560" height="315" src="https://www.youtube.com/embed/AR0eMbk_z5M" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


The post should give an overview of your artistic vision. In particular for this assignment, you should address how you have specialized your generative art to the space. What creative decisions did you work lead you to, and which decisions did you take? How were your decisions motivated by your larger creative vision for this project. In the same vein, also address any technical issues you encountered in your work. Particularly focus on issues that other artists may encounter when developing with your hardware setup.



I started out by envisioning an outline of what I wanted, namely text that is falling.

I tested a few colours for the text

Difficulty in developing with this hardware setup is the relatively sparse amounts of documentation. Getting the text to draw without graphical artifacts slightly difficult, but was overcome via trial-and-error.












## How to run:

We are using the Arduino IDE. To enable IDE support for the ESP32, first open up Preferences and under "Additional Boards Manager URLs", add the following URL:
```
https://dl.espressif.com/dl/package_esp32_index.json
```
![BoardsManagerURL](https://user-images.githubusercontent.com/6265129/153997561-184baff3-dad6-4699-b3ea-dfbc9214f8ea.jpg)

Then, go to "Tools/Board:/Board Manager" and install ESP32:

![BoardsManager](https://user-images.githubusercontent.com/6265129/153997769-d04a40cc-fc14-4832-a115-e32f032be1a6.jpg)

Then, go to "Tools/Manage Libraries" and search for tft_eSPI. Install it.

![ManageLibs](https://user-images.githubusercontent.com/6265129/153997596-e524be05-fd41-4741-9025-56ad5be9ab33.jpg)

After that, go to "Tools/Board:" and select "TIGO T1".

![BoardSelect](https://user-images.githubusercontent.com/6265129/153997616-e5988c80-6d34-4566-b800-3d8c03f9ffd7.jpg)

Now, simply connect your board and click upload.


## Additional Notes:

If you want to use this in an installation, you can plug in a battery using the JST connector on the back of the ESP32.





