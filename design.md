---
layout: default
title: Design
permalink: /design/
---

# 2. Design

## (a) What design criteria must your project meet? What is the desired functionality?
- Accurate Perception: The system must reliably detect the Word Hunt board, estimate its pose, and recognize the letters within the board.
- Correct Planning: The system must compute valid word paths under the constraints of the Word Hunt game and convert these discrete paths into physically feasible paths for the robot to trace.
- Precise Movement: The robot must trace the words accurately and precisely on a flat surface, as the slightest deviations can cause damage to the tablet or lead to incorrect selection of letters within the board.

**Desired Functionality:**  
The desired functionality of the project is for the robot to, given a Word Hunt game board positioned relative to an ArUco tag, autonomously detect and interpret the board, plan its actions, and play the Word Hunt game end to end and score as high as possible.

## (b) Describe the design you chose.

We chose to position an ArUco tag on the table in front of the UR7e and place the iPad at a known fixed offset relative to that tag. Using a RealSense camera, we simultaneously observe both the table-mounted ArUco tag and the ArUco tag located at the base of the UR7e. We use ``aruco_node`` to detect the positions and IDs of these tags, which allows us to compute the iPad’s position in the robot’s frame. The iPad position is defined as a point slightly above the screen, corresponding to the top-left square of the Word Hunt board.

This iPad reference point is published as a topic, and a processor node transforms it into the robot’s ``base_link`` frame. This transformed point is then used to move the UR7e end effector to the iPad location. Once positioned, we provide an optional command-line loop that allows for small manual adjustments to the end-effector pose. This is primarily used to account for minor localization error and to ensure the robot does not apply excessive force to the iPad with the Apple Pencil. In practice, once the iPad offset relative to the ArUco tag is calibrated, these adjustments are rarely needed.

After positioning, the Word Hunt game is opened on the iPad. The main node then subscribes to the camera image topic and, using the known offsets relative to the table ArUco tag, extracts the four corner points of the Word Hunt grid. A homography is computed to rectify the image, producing a flat, top-down view of the board. This rectified image is sent to a Qwen API inference LLM with prompting to return the 16 letters on the board.

The detected letters are converted into a 4×4 2D array and passed into our Word Hunt solver, which uses depth-first search with backtracking to find all valid word paths. Each word’s path is stored in a dictionary, and the words are sorted by length to prioritize higher-scoring words. The paths, originally represented as grid indices (e.g., (0,1)), are then converted into continuous (x, y) positions in the ``base_link`` frame. The robot iterates through these word paths, tracing them sequentially until the game timer expires, at which point the system automatically stops after 80 seconds, matching the Word Hunt game duration.

## (c) What design choices did you make when you formulated your design? What trade-offs did you have to make?



## (d) How do these design choices impact robustness, durability, and efficiency?

> Place diagrams and photos here.