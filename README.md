# Project Overview

The game is a 3D Endless Runner web project (inspired by popular racing and obstacle-avoidance games), built entirely for smooth and efficient web browsing, with a focus on lightweight design and full responsiveness across various screen sizes.

# Stack and Technologies

* **JavaScript (ES6+):** The core programming language for building the game's logic, animating elements, and calculating scores.
* **Three.js (r128):** The core library used for creating and rendering 3D graphics and controlling lighting, camera, and objects using WebGL.
* **Tailwind CSS v4:** A utility-first framework used to design 2D user interfaces (UI overlays) such as the splash screen, game over screen, and score counter, in a flexible and responsive manner.
* **HTML5:** The basic structure and container in which the game environment is rendered.

# Software Architecture and Code Components

## 3D Environment Setup (`init`)
* **Scene:** The background color is set to a warm, pale pink, and the Three.js Fog feature is enabled to blend the horizon and give the game a comfortable visual depth.
* **Lighting:** Ambient Light is combined to prevent harsh shadows, and Directional Light with Shadows enabled to highlight the three-dimensionality of objects and donuts on the bakery floor.
* **Renderer:** `WebGLRenderer` is used with antialiasing enabled to improve graphics quality.

## Responsive Camera System
A dynamically adjusted Perspective Camera is used to address the issue of tall screens (phones):
* **On PCs:** The field of view (FOV) is set to 60 degrees to provide a balanced horizontal view.
* **On Smartphones:** The code automatically checks if the height is greater than the width and dynamically expands the viewing angle to 85° to ensure all three tracks are fully visible and objects don't disappear at the edges.

These values are updated instantly via the `onWindowResize()` function when the device or window is resized.

## Game Logic & Controls

* **Game Loop:** Relies on `requestAnimationFrame` to update the position of objects and calculate collisions at a smooth frame rate that matches the user's screen.
* **Movement and Navigation:** The environment is divided into three fixed virtual tracks along the $X$ axis. The player moves between tracks using keyboard events (arrow keys / WASD) or **Touch Swipes** on mobile screens.
* **Procedural Generation:** Decorative elements (lollipops, bushes), obstacles (coffee cups, milk cartons, giant chocolate donuts), and golden coins are randomly and continuously generated at the horizon and move towards the camera along the $Z$ axis to simulate endless running.

## Collisions & Scoring System
Bounding Box Collision Detection: The volumetric distance between the player's object (the main donut) and obstacles/rewards is continuously calculated in every frame:
* **Upon collision with an obstacle:** The game loop is paused, the `gameOver()` function is activated, and the loss interface is displayed, comparing the current score to the local high score.
* **Upon collecting coins:** The player gains a massive score bonus (+500 points), and the coin is safely removed from the scene.
* **Continuous Score:** The counter dynamically increases the longer the player survives, updating the DOM interface immediately.

# Exceptional Performance Features

* **Reliance on External CDN Links:** Libraries (Three.js and Tailwind) are loaded directly from fast servers, reducing the project file size and enabling it to open instantly.
* **Memory Management (Object Disposal):** Objects that extend beyond the camera's position ($Z > 10$) are automatically removed from the scene and array storage to maintain a stable frame rate (FPS) and prevent memory leaks during extended gameplay.


# Play Live Instantly
No installation required! You can play the game directly in your browser via GitHub Pages:
 **[Play Donut Rush Live Here](https://adamafroukh.github.io/donut-rush/)**

