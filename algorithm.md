# Algorithm

The algorithm behind the **Digital Rain** effect simulates falling raindrops while synchronizing with background music. The key elements include **randomized raindrop properties**, **timed updates**, and **prime-number-based intervals** for drop spawning.

## 1. Raindrop Initialization  
Each **RainDrop** object represents an individual raindrop with properties:  
- **Position (x, y)**: The x-coordinate is randomly chosen within the screen width, and the y-coordinate starts off-screen.  
- **Speed**: Randomly chosen between `1` and `3`.  
- **Length**: Ranges between `3` and `7` characters.  
- **Character Composition**: A mix of `0`-`9` digits and `█` block characters to create a digital rain effect.  

## 2. Raindrop Movement  
The **Update()** function:  
- Moves the raindrop downward by increasing its **yPos_** by its speed.  
- Calls the **Render()** method to display the raindrop at the updated position.  

## 3. Rendering & Color Randomization  
The **Render()** function:  
- Moves the console cursor to each raindrop’s (x, y) position.  
- Assigns random colors using `GenerateRandomColor()`.  

## 4. Prime-Number-Based Raindrop Spawning  
To create variation in raindrop appearance, the **SpawnRainDrop()** function is triggered using a **prime-number timer**:  
- A timer checks elapsed time using **std::chrono**.  
- A **prime sequence** (2, 3, 5, 7, 11, 13, 17, 19) determines when new raindrops spawn.  
- Each prime-numbered interval spawns a new raindrop, creating an organic pattern of emergence.  

## 5. Removal of Off-Screen Raindrops  
- Raindrops that exceed the screen height are removed using `std::remove_if()`.  
- This prevents memory overflow and ensures efficient rendering.  

## 6. Audio Playback Synchronization  
- The **Super Mario Theme** is played in a separate thread using `PlaySound()`.  
- The falling raindrops visually align with the background music, **simulating musical notes being played**.  

## 7. Main Loop Execution  
The **Run()** method:  
- Sets the console window size and starts music playback.  
- Spawns raindrops at random intervals, using prime numbers for varied speed.  
- Updates and renders raindrops at **30 FPS (every 33ms)** for smooth animation.  
- Removes off-screen raindrops and loops continuously until terminated.  

---

This approach creates a visually engaging effect where **falling raindrops appear as musical notes**, bringing together randomization, prime-based timing, and music synchronization.
