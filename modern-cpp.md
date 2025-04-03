# Modern C++  
 
The **Digital Rain** project takes full advantage of **Modern C++ (C++11 and beyond)** to enhance efficiency, readability, and maintainability. Key features utilised include:  

### Smart Initialisation with Constructor Initialiser Lists
My project relies on constructor initialiser lists since they represent modern C++ functionality which appeared in C++11 standards to enable direct member variable setup during initialisation while bypassing extra assignments. The RainDrop constructor includes initialisation of member variables inside its initialiser list as RainDrop::RainDrop(int x, int speed, int length) : xPos_(x), yPos_(-length), speed_(speed), length_(length). This method places raindrops above the screen at yPos_(-length). The modern initialisation technique within the constructor produces superior performance than previous assignment techniques.
 

### Random Number Generation with <random>  
The project uses C++11 <random> library features together with new random number generation capability to replace the deprecated rand() function. The SpawnRainDrop() method establishes a Mersenne Twister generator through static std::mt19937 rng(std::random_device{}()) and joins the generator with std::uniform_int_distribution<> speedDist(1, 3) for speed selection and lengthDist(3, 7) and xDist(0, width_ - 1) for length and x-position selection. Static taxation of the generator maintains persistent consistency during multiple calls which enables the generation of varied raindrops effectively. 

### Containers and Emplace Construction
The raindrop management section of my project uses modern features including emplace_back method from C++11 standard library and the vector container RainDrop drops_. This appears in drops_.emplace_back(xDist(rng), speedDist(rng), lengthDist(rng)) within SpawnRainDrop(). The inserts directly into vector memory through construction of each RainDrop eliminate the need for object copies that would occur when using push_back. Modern C++’s emphasis on efficiency is supported by the fast addition of raindrops through this approach.  

### Chrono Library for Precise Timing  
My project employs C++11 <chrono> library for precise measurements because it ensures proper control over frame rates and spawn intervals. The DigitalRain::Run() function uses std::chrono::steady_clock::now() to obtain time points for measuring elapsed time through std::chrono::duration_cast<std::chrono::milliseconds>(currentTime - lastFrameTime).count() every 33 milliseconds (~30 FPS). The tracking of lastSpawnTime_ takes place in Update() which eliminates previous imprecise timing approaches through accurate timing management.

### Multithreading with <thread>
My project uses C++11’s std::thread to execute the Mario theme sound during the simulation execution uninterrupted. The DigitalRain::Run() method creates the musicThread using std::thread with the arguments &DigitalRain::PlayMarioTheme and this to start the separate thread for audio playback outside of the animation loop framework. detach() allows thread maintenance while running so multi-threading becomes simpler than using legacy Win32 techniques.

### Lambda Expressions in Algorithms
My program utilises C++11 lambda expressions to enhance the garbage collection efficiency inside DigitalRain::Update(). The erase method of drops_.erase removes elements from the vector between drops_.begin() and drops_.end() utilising std::remove_if. It uses a lambda expression to check off-screen status through drop.IsOffScreen(height_). A lambda expression in C++11 simplifies and streamlines the erase-remove idiom for better readability than previous function objects did.

### Auto Keyword for Type Deduction
The auto keyword from C++11 provides variable declaration simplification by allowing compilers to determine variable types in my project. The DigitalRain::Run() function contains auto declarations for lastFrameTime and deltaTime variables which use std::chrono::steady_clock::now() together with std::chrono::duration_cast<std::chrono::milliseconds>(currentTime - lastFrameTime).count() to simplify problematic chrono object manipulations. The code becomes more efficient and safe without compromising type security due to this approach.


### Range-Based For Loops
I use C++11 range-based for loops for simple container traversal in DigitalRain::Update as well as DigitalRain::Render through the lines for (auto& drop : drops_) { drop.Update(); } and for (auto& drop : drops_) { drop.Render(hConsole_); }. The drops_ container undergoes a clean update and render process through its individual elements with the use of range-based for loops that modern C++ code advocates.
