# Design and Test

The Digital Rain project is functioned as a C console based animation that simulates Matrix digital rain effects to music while randomly producing symbols for rain as a visual from the Super Mario Bros. theme. The primary focus throughout the development was to create an animated simulation utilizing console resource even with achieving great performance while employing interactive animations with highly visual impact.

### Key Features
The following features marked my project design for achieving an immersive experience:

- A Dynamic Falling Effect that displayed numbers/symbols, such as L'█' moving in descent at various speeds. The amounts of rain were just right and design randomization together with smooth frame updates for animation was key to maintaining its spell-binding characteristic to the viewer as it rendered to program.
  
- The Super Mario Bros soundtrack was synchronised with the rain drops through some loose music timing a combination that hinted that the raindrops produced notes from the June of this theme song. I produced two threads of execution of the application to separate the animation functions from the audio functions, in turn achieving visual performance that was unencumbered.

- I implemented prime numbers; 2, 3, and 5 as spawn criteria to create a sequence of drops for prolonged visual effect, while eliminating sequences, and repeating patterns. - Each raindrop had its on height, of 1-3 units per frame.

## System Components

### RainDrop Class
I used the RainDrop class to organise the individual raindrop behavior and established it as an autonomous simulation component.

The RainDrop::RainDrop(int x, int speed, int length) constructor generates a random xPos_ coordinate while speed_ varies from 1 to 3 and length_ falls between 3 and 7 (the function originates from SpawnRainDrop()). YPos_ received an initial value of -length that launched drops above the display screen gently. The simulation generated unique drop trajectories by using random numbers produced through a combination of std::mt19937 and std::uniform_int_distribution.

The GenerateRandomColor() component uses std::uniform_int_distribution<>() with colorDist(1, 15) to generate random console text colors which are integrated into the render function through SetConsoleTextAttribute. The code produced an active and dynamic color scheme which maintained the mood of the Matrix aesthetic.

Each character of the array was assigned random values between digits and blocks (0-9 and L'█') through the expression characters_[i] = binaryDis(gen) ? L'0' + digitDis(gen) : L'█'. L'0' + digitDis(gen) : L'█'. The execution algorithm (50/50 via binaryDis(0, 1)) between numbers and symbols maintained a balanced combination of numeric expressions with symbolic elements thus making the visual display more sophisticated.

### 2. DigitalRain Class
I designed the DigitalRain class to act as the core controller for the simulation, overseeing all system components and their interactions.

**Frame Rate Control (~30 FPS)** – In the Run() method, I utilized std::chrono to maintain a 33ms update cycle with an if condition checking (deltaTime >= 33). This approach helped achieve smooth animations by keeping both Update() and Render() synchronized at approximately 30 frames per second, balancing responsiveness with CPU usage.

**Console Buffer Management** – Within InitialiseConsole(), I invoked SetConsoleScreenBufferSize(hConsole_, { static_cast(width_), static_cast(height_) }) along with SetConsoleWindowInfo to dynamically adjust console size. This optimization enhanced display area utilization, ensuring raindrops weren’t clipped at the edges or bottom of the interface.

**Multi-Threading Implementation** – I created a separate thread in Run() using std::thread musicThread(&DigitalRain::PlayMarioTheme, this) for audio processing via PlaySound. By detaching this thread, it runs independently from the main thread focused on visuals, thereby preventing any performance slowdowns.

**Memory Management Optimization** – To manage memory efficiently, I employed drops_.erase(std::remove_if(...)) within Update() to remove off-screen raindrops where (yPos_ >= height_). This strategy effectively reduced memory usage and sustained performance during continuous simulation operation.

## Multi-Threading for Animation & Audio
The program utilises two running threads that work simultaneously for an integrated multimedia presentation:

The main thread executed the animation loop inside Run by calling both Update and Render functions while running system("cls") before each draw. System("cls") served to clear the screen while the program displayed every drop in its updated location.

This thread played the continuous Super Mario WAV file through the PlaySound(...SND_ASYNC | SND_LOOP) command. The audio playback ran through asynchronous execution to prevent interruptions of the main thread timing.

I adjusted Update() spawn intervals using primes[primeIndex_] * 5 to achieve a slight musical timing match between falling symbols and the song’s beat patterns.

---

## Testing

### 1. Visual Rendering Tests
I tested the design thoroughly to confirm its performance quality through multiple assessments of visual sharpness and system speed and synchronization with audio alongside checking software cooperation. The following section specifies the intense procedures I applied to guarantee project success.

Testing the raindrop visuals involved verification of both Matrix aesthetic standards and operational reliability.

I tested SpawnRainDrop() while it populated the screen with drops at different xDist values between 0 and width_ - 1 and speed values between 1 and 3. The function displayed a range of slow to fast drop speeds. I tested early versions of the program by checking random distribution algorithms to verify the distribution of random drops at xPos_ equal to zero.

I confirmed the simulation performed updates at standard frame rates of approximately 30 FPS by using std::chrono logs to measure deltaTime in Run(). The updates consistently maintained a 33ms interval. Sleep(1) experienced adjustments which optimised CPU performance until the application surpassed 10 minutes runtime without any stuttering.

The brightness of each initial symbol character stood out because of new random color selection in each frame yet the remaining drop tail symbols faded with time according to Render() output. My modifications to lengthDist(3, 7) allowed tails to appear while keeping them from becoming excessively long until the effect was optimal.

### 2. Performance Optimisation
The simulation received optimised performance under load through solutions designed to fix possible performance obstacles.

The drops_.size() was monitored through debug prints to verify drops_.erase(std::remove_if(...)) function in Update() maintained a drops_.size() below 50-60 even after long execution durations. The Visual Studio memory profiler showed that memory leaks did not occur throughout the simulation. System("cls") in Render() received testing to ensure no console flicker appeared during playback on the 120x25 console display. I stabilised console transitions between frames by making sure every SetConsoleCursorPosition command executed with precision whenever jitters appeared. By multiplying the default spawn rates with a value of 5 I adjusted them properly to prevent overload of the render loop which maintained a smooth performance with 20-30 active drops.

### 3. Music Synchronisation
To achieve a natural syncing of the sound of raindrops to the music, I needed to test the audio-visual synchronisation of events.In the development stage I was using primes[] intervals between 10ms-95ms while I listened to the WAV file and repeated the spawn timing until I got the music to sync with the Mario theme at about 120 BPM. The sound delivery of the raid produced a pulsating effect, and it seemed to naturally sync with the musical key beats to the initial memorable notes. I also checked that musicThread.detach() function seemed to work to let the music continue in the background while the program animation ran fluidly, even in the absence of a WAV file which PlaySound would silence. I ran two min tests, and I was confident of natural rhythms occurring throughout when elapsedMs was greater than primes[primeIndex_] * 5 during the music playback. This definitely gave the rain effects a more naturally occurring flow and rhythm compared to the mechanical feel while still retaining the rain effect.

### 4. Console Compatibility
The program proved its ability to function with multiple setup configurations to prevent specific platform restrictions.

The InitialiseConsole() function operated while changing the width_ from 80 to height_ from 25 and width_ from 120 to height_ from 40 which confirmed SetConsoleScreenBufferSize provided accurate display size adjustments. The xDist(0, width_ - 1) range received adjustments to prevent edge overflow when dealing with larger width dimensions.
The executable functioned on Windows 10 and Windows 11 systems with multiple administrative privilege options while confirming audio and console functionality across all configurations. I conducted tests inside VMs to identify any sound problems caused by drivers.
The program withstood 100+ minute performance tests through interval adjustments and displayed constant operation and absence of display disturbances.

---

## Final Outcome

The **Digital Rain** program builds an attractive synchronised audio-visual experience which successfully blends software-based music performance with visual animations. The combination of console-based animation techniques with music playback allowed the project to produce a splendid interactive outcome through the fusion of complex technology and artistic creativity.
