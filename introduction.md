# Introduction

The inspiration for this project is the rhythm games like Piano Tiles and falling keys piano tutorial playthroughs, in which keys or notes fall in a sequential manner. The games provide an entertaining way of learning musical timing and coordination, as well as a visually engaging experience.

For my project I wanted to achieve a similar appearance but with a Digital Rain effect, drawing inspiration from the Matrix Rain visualisation. By combining cascading symbols and procedural randomness, the goal is to create an engaging console like visual spectacle. Furthermore, for the sake of enhancing the interactive experience, the project has background music playback specifically, the Super Mario Theme—adding a retro and playful element.

The project has a unique aspect in that the impact of the falling rain is synchronized with the Super Mario WAV file. When the rain falls, they simulate the look of playing musical notes on a virtual keyboard in harmony with the rhythm of the music. This illusion causes the pouring symbols to look like the actual musical notes themselves, strengthening the connection between the music and movement of sight.

This application is developed on top of C++ and the Windows Console API, leveraging multi-threading to display animation and audio play simultaneously. The animated descending symbols are created dynamically on patterns which vary at prime intervals, developing an extra timing difference in the appearance.

In the course of the subsequent discussion in this paper, I shall describe the following aspects of the project:

- Design & Test: Overall system design, component interactions, and how tests are being approached.
- Algorithm: Explanation of the logic employed to create rain, movement, and randomness.
- Problem-Solving: Issues with development faced and solutions implemented.
= Modern C++ Insight & Reflection: Key C++ concepts utilized and scope for improvement.

This project is not only an exploration of console graphics and procedural animation but also serves as a stepping stone for other interactive programs or music visualizations.
