---
layout: default
title: Additional Materials
permalink: /additional-materials/
---

# 7. Additional Materials

## (a) Code, URDFs, and launch files you wrote

| File | Description |
| :--- | :--- |
| `/src/planning/planning/ar_extraction.py` | Crops out the Word Hunt board and rectifies it into a top-down view |
| `/src/planning/planning/llm_inference.py` | Sends the rectified board image to Qwen API and returns the 16 letters in the board. |
| `/src/planning/planning/main.py` | The core logic of the program: moving to start position, running the perception pipeline, executing the game actions. |
| `/src/planning/planning/transform_ipad_pose.py` | Transforms the `ipad_point` into `ipad_point_base` which is just the point but in `base_link` |
| `/src/planning/planning/wordhunt.py` | The DFS + backtracking algorithm that takes in the letters in the grid and returns the found words and paths. |
| `/src/planning/planning/wordhunt.py` | The DFS + backtracking algorithm that takes in the letters in the grid and returns the found words and paths. |
| `/src/perception/perception/process_pointcloud.py` | Takes in `aruco_markers` and outputs `ipad_point` which is the point right above the ipad relative to the table ArUco tag. |

Code found here: [https://github.com/bbokycom/ur7e_plays_word_hunt](https://github.com/bbokycom/ur7e_plays_word_hunt).

## (b) CAD models for any hardware you designed

<a href="assets/downloads/UR7e%20Apple%20Pencil%20Holder.stl" download>
  Download Apple pencil holder STL
</a>

## (c) Data sheets for components used in your system

## (d) Any additional videos, images, or data from your finished solution

<iframe width="100%" height="400" src="https://www.youtube.com/embed/i3llYZd1tus" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


> Add files into subfolders like `code/`, `cad/`, `datasheets/`, and `media/` and link them here.
