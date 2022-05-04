---
layout: post
title:  "Drum Beat Programmer"
date:   2022-05-04 01:00:14 -0500
categories: art
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/5N8ggmoUmLg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

For the final project for my class "Creative Embedded Systems", I decided to take advantage of my experience and passion in drumming to put it to use.

I wanted to create a device which allows you to easily create a drum beat. There are countless musical techniques and rhythms, but including all of them in my project would be impossible. Hence I decided to simplify things in two aspects: Instrumentation and Rhythm. For instrumentation, I limited the output to Hi-Hat, Snare Drum, and Bass Drum. These three instruments are the most crucial aspects of a drum set, and is also the most commonly used, and hence most drum patterns could be covered by this choice. In terms of Rhythm, I decided to stick to straight 4/4 time and divide the bar into eight 8th notes. This way, most common non-jazz rhythms are covered, and is also much simpler to understand as opposed to other time signatures or swing beats.


![plane](https://miro.medium.com/max/700/1*UWeiESU62Dr3_E9IWOIZ4Q.jpeg)

![Plane_open](https://miro.medium.com/max/700/1*4DswH9LDBM2T4CO9fM4QPw.jpeg)

### Implementation
The system was divided into two parts, an ESP32 part which handles user input and drum beat programming, and a web-app part which takes serial input from the ESP32 and plays audio. I decided to do this since the ESP32 is unable to play audio. This need made me decide to use a wired connection to a computer. Additionally, since this system requires a wired connection, there would be no need for a battery as the power can be supplied from the wired connection.

The Drum Programmer part is done on the ESP32. Here, a graphical representation of a single bar drum pattern is displayed on the ESP32's LCD screen. The pattern consists of a 8-by-3 grid of dots. The 8 dots horizontally represent all the 8th notes in a single bar of a 4/4 measure. The 3 dots vertically represent the 3 main instruments of a drum set -- hi-hat, snare drum, and bass drum. The user uses a joystick to control the position of a "cursor". The user can then use the button to "toggle" that dot. If the dot is filled, it means that the instrument (e.g. snare drum) is played at that moment in time (e.g. the "downbeat of beat 3"). By filling a bunch of dots, the user can program a drum pattern. To play the drum pattern, the user can "unpause" using the button on the ESP. When "unpaused" a vertical line representing the current time position moves rightwards, and each time it reaches a group of 3 dots it sends a signal via serial to the Javascript system which plays the corresponding drum hit. The signal is structured as follows: "{ABC}" where each letter is either a 1 or a 0, representing if the specific instruments plays at that moment in time, or not. The potentiometer controls the BPM value, which speeds up or slows down the drum beat.

The software design is as follows. There are two threads running. A render thread and a "play" thread. The render thread is on a loop that runs every 20ms and renders the 8-by-3 grid based on the stored 2D array. The "play" thread loop runs at an interval determined by the BPM value, and pauses when the pause button is toggled. This thread is responsible for sending the serial information to the web-app.

For the web-app part, the system uses Howl.js library to play audio. A string builder ensures valid serial input, and the serial input is read and plays the correct audio clips.

### Implementation Challenges
In terms of implementation challenges, we encountered a few challenges.

In terms of hardware, there was the issue of malfunction of the joystick and push button. The joystick has a malfunctioning x-axis, which lead to joystick not being able to move the cursor up. When the joystick was at full tilt in the positive x-direction, it erroneously maxes out the input on the y-axis. I was able to cancel out this simultaneous movement at the cost of preventing the joystick from moving upward. However, the system remained usable as I implemented cursor "loop-back". If the user wanted to move the cursor up by one, they would simply move down twice and arrive at the intended position.

Secondly, the push button was malfunctioning. When using digital interrupts, the button will constantly output a connection despite not being pressed. I solved this by creating a custom button input detector using analogInput() instead.

On the web-app side, I encountered the issue of the serial readings being often broken up into lines inconsistently. I solved this by writing a string builder that makes sure the resulting string begins with a '{' and ends with a '}'.

The code for the ESP32 and the web-app, as well as instructions on how to run it, can be found [here][codebase]


[codebase]: https://github.com/AlephFive/ESP_DrumMachine