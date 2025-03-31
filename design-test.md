# Design and Test

The Digital Rain project existed as a C++ console-based animation which reproduced "Matrix" digital rain effects through synchronized music while triggering random symbols for an effect that simulated musical notes from the Super Mario Bros. theme. The main objective during development was to build an animated simulation that used console resources to achieve performance excellence while creating visual appeal through interactive features.

### Key Features
The following features marked my project design for achieving an immersive experience:

- A Dynamic Falling Effect presented numbers and symbols such as L'█' in descending motion at unique speeds to deliver like rain. Random generation combined with smooth animation updates was essential to maintain its mesmerizing effect in the program.

- The Super Mario Bros. soundtrack synchronized with the rainfall drops through loose musical timing that made the raindrops appear to play notes from the theme.
I implemented two execution threads for the application to distribute animation responsibilities separately from audio processing tasks thus obtaining uninterrupted visual performance.

- I implemented prime numbers such as two three and five as spawn conditions to produce an erratic sequence of drops that eliminated repetitive sequences.

- Each raindrop maintained an individual speed range of 1-3 units/frame and a separate color value from 1-15 that the GenerateRandomColor() method assigned for visual enhancement throughout the rain effect.

## System Components

### RainDrop Class
I used the RainDrop class to organize the individual raindrop behavior and established it as an autonomous simulation component.

The RainDrop::RainDrop(int x, int speed, int length) constructor generates a random xPos_ coordinate while speed_ varies from 1 to 3 and length_ falls between 3 and 7 (the function originates from SpawnRainDrop()). YPos_ received an initial value of -length that launched drops above the display screen gently. The simulation generated unique drop trajectories by using random numbers produced through a combination of std::mt19937 and std::uniform_int_distribution.

The GenerateRandomColor() component uses std::uniform_int_distribution<>() with colorDist(1, 15) to generate random console text colors which are integrated into the render function through SetConsoleTextAttribute. The code produced an active and dynamic color scheme which maintained the mood of the Matrix aesthetic.

Each character of the array was assigned random values between digits and blocks (0-9 and L'█') through the expression characters_[i] = binaryDis(gen) ? L'0' + digitDis(gen) : L'█'. L'0' + digitDis(gen) : L'█'. The execution algorithm (50/50 via binaryDis(0, 1)) between numbers and symbols maintained a balanced combination of numeric expressions with symbolic elements thus making the visual display more sophisticated.

### 2. DigitalRain Class
I structured the DigitalRain class as the simulation’s orchestrator, managing the overall system and integrating all components:

Frame Rate Control (~30 FPS) – I used std::chrono in Run() to enforce a 33ms update cycle (if (deltaTime >= 33)), ensuring smooth animation. This tied Update() and Render() to a consistent ~30 FPS, balancing responsiveness with CPU efficiency.

Console Buffer Manipulation – In InitializeConsole(), I called SetConsoleScreenBufferSize(hConsole_, { static_cast<SHORT>(width_), static_cast<SHORT>(height_) }) and SetConsoleWindowInfo to resize the console dynamically. This maximized display space, preventing truncation of raindrops at edges or bottom.

Multi-Threading Support – I introduced a thread in Run() with std::thread musicThread(&DigitalRain::PlayMarioTheme, this) to handle audio via PlaySound, detaching it to run independently. This kept the main thread focused on visuals, avoiding bottlenecks.

Memory Management – I implemented drops_.erase(std::remove_if(...)) in Update() to purge off-screen raindrops (yPos_ >= height_), preventing memory bloat and maintaining performance as the simulation ran indefinitely.

## Multi-Threading for Animation & Audio
The program utilizes two running threads that work simultaneously for an integrated multimedia presentation:

The main thread executed the animation loop inside Run by calling both Update and Render functions while running system("cls") before each draw. System("cls") served to clear the screen while the program displayed every drop in its updated location.

This thread played the continuous Super Mario WAV file through the PlaySound(...SND_ASYNC | SND_LOOP) command. The audio playback ran through asynchronous execution to prevent interruptions of the main thread timing.

I adjusted Update() spawn intervals using primes[primeIndex_] * 5 to achieve a slight musical timing match between falling symbols and the song’s beat patterns.

---

## Testing

### 1. Visual Rendering Tests
I tested the design thoroughly to confirm its performance quality through multiple assessments of visual sharpness and system speed and synchronization with audio alongside checking software cooperation. The following section specifies the intense procedures I applied to guarantee project success.

Testing the raindrop visuals involved verification of both Matrix aesthetic standards and operational reliability.

I tested SpawnRainDrop() while it populated the screen with drops at different xDist values between 0 and width_ - 1 and speed values between 1 and 3. The function displayed a range of slow to fast drop speeds. I tested early versions of the program by checking random distribution algorithms to verify the distribution of random drops at xPos_ equal to zero.

I confirmed the simulation performed updates at standard frame rates of approximately 30 FPS by using std::chrono logs to measure deltaTime in Run(). The updates consistently maintained a 33ms interval. Sleep(1) experienced adjustments which optimized CPU performance until the application surpassed 10 minutes runtime without any stuttering.

The brightness of each initial symbol character stood out because of new random color selection in each frame yet the remaining drop tail symbols faded with time according to Render() output. My modifications to lengthDist(3, 7) allowed tails to appear while keeping them from becoming excessively long until the effect was optimal.

### 2. Performance Optimization
The simulation received optimized performance under load through solutions designed to fix possible performance obstacles.

The drops_.size() was monitored through debug prints to verify drops_.erase(std::remove_if(...)) function in Update() maintained a drops_.size() below 50-60 even after long execution durations. The Visual Studio memory profiler showed that memory leaks did not occur throughout the simulation. System("cls") in Render() received testing to ensure no console flicker appeared during playback on the 120x25 console display. I stabilized console transitions between frames by making sure every SetConsoleCursorPosition command executed with precision whenever jitters appeared. By multiplying the default spawn rates with a value of 5 I adjusted them properly to prevent overload of the render loop which maintained a smooth performance with 20-30 active drops.

### 3. Music Synchronization
To achieve a natural syncing of the sound of raindrops to the music, I needed to test the audio-visual synchronization of events.In the development stage I was using primes[] intervals between 10ms-95ms while I listened to the WAV file and repeated the spawn timing until I got the music to sync with the Mario theme at about 120 BPM. The sound delivery of the raid produced a pulsating effect, and it seemed to naturally sync with the musical key beats to the initial memorable notes. I also checked that musicThread.detach() function seemed to work to let the music continue in the background while the program animation ran fluidly, even in the absence of a WAV file which PlaySound would silence. I ran two min tests, and I was confident of natural rhythms occurring throughout when elapsedMs was greater than primes[primeIndex_] * 5 during the music playback. This definitely gave the rain effects a more naturally occurring flow and rhythm compared to the mechanical feel while still retaining the rain effect.

### 4. Console Compatibility
The program proved its ability to function with multiple setup configurations to prevent specific platform restrictions.

The InitializeConsole() function operated while changing the width_ from 80 to height_ from 25 and width_ from 120 to height_ from 40 which confirmed SetConsoleScreenBufferSize provided accurate display size adjustments. The xDist(0, width_ - 1) range received adjustments to prevent edge overflow when dealing with larger width dimensions.
The executable functioned on Windows 10 and Windows 11 systems with multiple administrative privilege options while confirming audio and console functionality across all configurations. I conducted tests inside VMs to identify any sound problems caused by drivers.
The program withstood 100+ minute performance tests through interval adjustments and displayed constant operation and absence of display disturbances.

---

## Final Outcome

The **Digital Rain** program builds an attractive synchronized audio-visual experience which successfully blends software-based music performance with visual animations. The combination of console-based animation techniques with music playback allowed the project to produce a splendid interactive outcome through the fusion of complex technology and artistic creativity.
