# Introduction

For my project, the same appearance of Piano tiles and falling notes is used but with Digital Rain effect, inspired by the Matrix Rain visualisation, through a blend of procedural randomness and cascading symbols. Additionally, in regards to interactivity, the Super Mario Theme song is added in the background providing a seamless effect along with the rain matrix.

In my project the rhythm of the falling raindrops synchronises with the Super Mario WAV file. While making the raindrops fall, they are made to appear like playing musical notes on a keyboard in synchrony with the rhythm of the music. This creates an illusion to the effect that the pouring symbols are perceived as similar to the musical notes, reasserting the correlation between vision movement and music.

My application is based on C++ and Windows Console API and employs multi-threading to output animation and audio playback in parallel. The falling animated characters are created dynamically over alternating patterns that change at prime time intervals, thereby producing another timing difference in the look.
Over the course of the rest of my blog, I will discuss the following aspects of the project:

Design & Test: High-level system design, interaction between components and with themselves, and how it is tested.

Algorithm: Explanation of logic utilised to create rain, motion, and randomness.

Problem-Solving: Problems found during implementation and how they were solved. 

Modern C++ Insight & Reflection: Key C++ features utilised and where the author could have improved.


