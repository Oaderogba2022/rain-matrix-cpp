# Algorithm

## Overview  

The **Digital Rain** algorithm is designed to simulate falling symbols in a cascading effect while synchronizing with the **Super Mario Bros. theme song**. It achieves this using **multi-threading**, **randomized raindrop generation**, and **frame-based animation**. The algorithm ensures that the rain effect appears smooth, dynamic, and responsive to the music playing in the background.

Digital Rain algorithm is intended to simulate cascading falling symbols and synchronize itself with the music of **Super Mario Bros**. It achieves this with **multi-threading**, **random creation of raindrops**, and **animation based on the frame**. The algorithm creates a smooth, dynamic, and background music-responsive look for the rain effect.

## Step-by-Step Breakdown  

### 1. Initialization  

At the start of the program, the following steps are performed:  

1. **Console Configuration:**  
   The Windows console is set up to use **buffered output** to prevent flickering. The console size is adjusted to fit the animation, and the cursor is hidden to enhance visual clarity.  

2. **Random Seed Setup:**  
   A random seed is initialized using the system clock to ensure that raindrop positions and speeds vary each time the program runs.  

3. **Multi-Threading Initialization:**  
   - The **first thread** is dedicated to running the animation loop, continuously updating the screen with falling symbols.  
   - The **second thread** is responsible for playing the **Super Mario Bros. theme song** using `PlaySound()`, ensuring that music plays in the background without affecting animation speed.  

---

### 2. Raindrop Generation  

1. **Spawn New Raindrops:**  
   - Every few frames, new raindrops are randomly generated across the screen.  
   - Each raindrop is assigned:  
     - A random **starting position (x-coordinate)**.  
     - A random **length**, defining how many characters trail behind.  
     - A random **falling speed**, determining how frequently it updates its position.  
     - A random **color** to add visual diversity.  

2. **Prime-Number-Based Timing:**  
   - The raindrop spawning intervals are determined using **prime numbers**.  
   - This ensures that new drops appear at irregular but structured intervals, creating a **natural rhythm** that complements the music.  

---

### 3. Animation Loop  

The main animation loop continues to update the raindrop locations in order to accomplish the falling action. Every time through the loop does the following:

1. **Clear Previous Frame:**
- The console buffer is cleared before the new frame is drawn to prevent character overlap.

2. **Update Raindrop Positions:**
- Each raindrop that is in motion is displaced **one row down** based on its velocity.
- The **front character** is drawn in a light color, and the back characters are made smaller as they drop.

3. **Take Off-Screen Raindrops:**

- Once a raindrop has passed the console bottom, it is deleted from memory to prevent excessive use of resources. 4. **Control Frame Rate:** - The program manages frame rate using `std::chrono::steady_clock` so that updating occurs at a constant **30 frames per second**.

---

### 4. Music Synchronization  

1. **Super Mario Bros. Theme Playback:**  
   - A separate thread plays the **Super Mario Bros. theme song** in the background using `PlaySound()`.  
   - This allows the animation and the music to run **independently** without interfering with each other.  

2. **Raindrop Timing & Music Synchronization:**  
   - Since raindrops are spawned at prime-number intervals, their appearance naturally aligns with the tempo of the music.  
   - This creates the illusion that **the raindrops are playing the notes of the song** as they fall, adding an interactive musical effect.  

---

### 5. Program Termination  

1. **User Input Handling:**  
   - The program continuously checks for user input (e.g., pressing a key) to allow for manual termination.  

2. **Clean-Up:**  
   - When the program exits, it resets the console settings, ensuring that the cursor reappears and the buffer is cleared.  

---

## Algorithm Complexity  

- **Raindrop Updates:** O(n) per frame, where **n** is the number of active raindrops.
- **Rendering:** O(n) frame by frame, as each raindrop needs to be rendered on the screen.
- **Music Playback:** O(1), as music is played in a different thread and does not affect animation performance.
- **Overall Performance:** The application maintains a steady **30 FPS**, even in the midst of heavy raindrops, for optimal performance. 

---

## Conclusion  

The **Digital Rain** program is a successful blend of **procedural animation, multi-threading, and music synchronization** that creates a thought-provoking visual and audio experience. **Prime-number-based timing** provides realism, and **multi-threading ensures seamless execution** without pauses or delays. The final product is an interactive and dynamic program that offers a **new synthesis of music and animation** to the console.
