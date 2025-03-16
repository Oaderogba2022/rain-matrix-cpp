# Problem Solving

While creating the Digital Rain effect, I had encountered several issues that required creative problem solving and debugging. The most significant issues I've faced in implementing them, along with their solutions, are mentioned below.

## Raindrop Spawning & Movement
The primary objective of the raindrop simulation was to ensure that the drops spawned at uneven time intervals and shifted smoothly across the screen. In the beginning, the raindrops were not being rendered correctly and were lost along the way before they could descend down the screen.

## Solution ##
To address this, I implemented a prime-number-based interval for spawning. Besides adding variation in the raindrop timing, this approach also caused the raindrops to spawn randomly at any interval, making it feel more natural. I also improved the movement logic by causing the drops to fall at a greater speed, making them always visible and moving smoothly on the screen.

## Background Music Playback Issues
The second major issue was with the background music, specifically when trying to sync the raindrops falling to the Super Mario theme song. I originally tried using the beep.h function to create the tones for each note in the song. When writing down the notes and frequencies for each note, though, I was running into issues where some of the notes weren't playing correctly.

## Problem ##
When attempting to assign a particular frequency to every note, some of the notes did not generate the right sound output, and a broken or distorted melody was produced. The song was also not played smoothly as there were sudden changes in frequency, and some of the notes were skipped.

## Solution ##
After some tries using the beep.h function, I realized that the note frequency resolution was not sensitive enough to provide the precision in timings needed by the melody. Some of the notes were missing because the timing precision was lacking, and the frequencies were not precise as they needed to be.

To overcome this, I moved to the PlaySound function of the Windows API, which allowed me to load and play the entire song as a WAV file in an asynchronous mode. It plays the music continuously in the background and synchronized nicely with the raindrop simulation. Now, instead of trying to encode the notes manually, the sound file provided me with a seamless audio experience.

## Raindrop Deletion & Performance Improvement
The initial issue that I was experiencing issues with was the performance of the program, especially when there were more raindrops being shown. At times, the screen would flicker or lag, especially when numerous raindrops were being displayed at the same time on the screen. The issue was compounded by inefficient use of memory because raindrops already out of the screen were not being removed in a timely manner.

## Solution ##
To work around this, I included an efficient raindrop removal system using std::remove_if() to rapidly eliminate drops that had moved off-screen. By removing unnecessary raindrops before the next update, I reduced memory usage and improved the performance in general to make the program run smoother even with a high number of drops on screen.

## Console Window Size & Resolution
The second issue that I faced in development was console window size. The console window was fixed in a default size that was too small to accommodate the raindrops well, and the output text would overflow or get truncated.

## Solution ##
I corrected this by adjusting the console buffer and window size programmatically with the InitializeConsole() function. This made the screen resize dynamically based on the needs of the program so that all the raindrops could be seen and the screen was not cluttered.

## Synchronization Between Raindrops & Music
One of the main objectives was to synchronize the raindrops with the background music in such a way that they were natural and interesting. At first, however, music and raindrops were not synchronized well enough, and the raindrops falling seemed completely unrelated to the melody.

## Solution ##
In order to do so, I utilized the interval system based on prime numbers to generate the raindrops randomly at time intervals that coordinated with the beat of the background music. This served to provide a more realistic pattern, wherein the raindrops were dropping in a rhythm synchronizing with the underlying melody, further enhancing the illusion that the raindrops were notes being played on the piano.
