---
layout: default
title: Conclusion
permalink: /conclusion/
---

# 5. Conclusion

## (a) Discuss your results. How well did your finished solution meet your design criteria?

Ultimately, we were able to fully implement end-to-end our criteria. We were able to accurately and consistently detect the ArUco tags, the Word Hunt board, and the letters within the board. The project also included correct and effective implementation of the Word Hunt finding algorithm. Finally, the robot was able to precisely move to all the paths and draw out all the word paths as needed. Overall, the project was a success and met all of our initial criteria.

## (b) Did you encounter any particular difficulties?

We encountered a few difficulties during the project. One major issue we noticed was that when outputting the `ipad_point_base` position, the values would often fluctuate by around a centimeter each time the robot was commanded to move to that point. In principle, each time we ran the main script, the robot was supposed to move to a position just above the top-left tile of the Word Hunt board. In practice, however, the robot would consistently be offset by about a centimeter, which made completing the project infeasible.

To address this issue, we modified the ipad_publisher to publish a running average of the iPad’s base position. This running average was computed by multiplying the previous average by 0.99 and adding 0.01 times the newly computed point. As a result, older measurements gradually lost influence while newer measurements were still incorporated, leading to significantly more stable position estimates. After this change, each time we ran the script the robot moved to a much more consistent and precise offset position.

We also encountered additional precision issues during small end-effector movements. When commanding slight movements in the x-direction, the arm would sometimes unintentionally move in the y- or z-directions as well. This behavior made precise tracing difficult and again threatened the feasibility of the project. We ultimately resolved this by adjusting the `tolerance_above` and `tolerance_below` parameters in the `JointConstraints` within `ik.py`. By decreasing these values from `0.01` to `0.001`, the robot was able to execute motions with significantly improved precision and reduced unintended axis coupling.

One final challenge involved how to physically hold the pencil or stylus using the robot. Initially, we relied on the UR7e’s gripper to directly hold the pen. While this approach worked in simple cases, even small variations in the z-axis would cause the pen to either lose contact with the drawing surface or press down with excessive force. This required constant supervision and frequent use of the emergency stop, which was not a sustainable solution.

To solve this, we designed and built a custom pencil holder that could apply a roughly constant downward pressure while still allowing for tolerance in the z-direction. The holder used grooves and rubber bands positioned behind the stylus to ensure that the tip consistently pressed against the screen with approximately the same force. At the same time, the design allowed the pencil to move upward by a few centimeters when additional force was applied, preventing excessive pressure. This amount of tolerance was sufficient for our level of precision, and the resulting pencil holder proved to be a reliable and effective solution.

## (c) Does your solution have any flaws or hacks? What improvements would you make with more time?

Our solution does include a few hacky parts that we used to make the system reliable within the project constraints and timeline.

One major hack in our system is that we rely on a known offset from the table-mounted ArUco tag to the iPad board location, rather than detecting the board directly in a more general and self-contained way. This approach works well as long as the iPad is placed very precisely relative to the ArUco tag, but it reduces generality and requires recalibration whenever the setup changes. With more time, we could make the system automatically detect the four corners of the Word Hunt grid directly from the camera image and compute the board pose relative to the ArUco tag on the fly. Additionally, since the physical size of the Word Hunt board is known, we could potentially eliminate the table-mounted ArUco tag altogether and run the system using only the iPad as the visual reference.

Another hack we relied on was using an LLM API for letter recognition. This approach was convenient and worked well in many cases, but it occasionally returned incorrect or improperly formatted outputs. With more time, we would replace this with an on-device vision model or a lightweight OCR/classifier specifically trained on the Word Hunt font, making letter recognition faster, deterministic, and usable offline. We did attempt more traditional vision-based approaches during development, but they were not reliable enough within the project timeline, so we ultimately proceeded with the LLM-based solution.

Finally, our solution still relies on a few manual and heuristic choices. In particular, we use a manual adjustment loop and hardcoded z-offsets when touching the screen to compensate for remaining precision issues. While this approach worked in practice, it is not fully autonomous and requires some user intervention.

With more time, we could implement contact sensing so that stylus pressure is controlled automatically. This would allow the system to detect when the stylus makes contact with the screen and dynamically determine the appropriate z-offset, rather than relying on fixed values. We could also incorporate an automatic visual alignment or feedback controller, where the camera is used to verify whether the end effector is correctly positioned over the target location and iteratively adjust the pose until it is aligned.