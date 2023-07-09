---
layout: post
title:  Google Summer of Code - Journal
date: 2023-07-09
description: GSoC 2023 adventures
tags: life
---


MoveIt is a prevalent open-source library in the robotic manipulation world, and it is the default choice for robotic manipulation with ROS2.
There were many projects to choose from; however, the one I found interesting was the Servo refactoring project, and discussions with the potential project mentors (Sebastain and Andy, super helpful and very cool people) revealed that it would be a welcome contribution. 

I spent some time understanding how to navigate the MoveIt codebase and the workflow. My first contribution was a small but beneficial performance optimization for the Rukig trajectory smoothing. This process gave me an overview of the contribution and review process for Moveit. Moreover, it gave me a sense of what to expect from the community.

The next step was to understand the Servo and its usage. An initial pass-through made it clear that the intended use case had evolved; the rigidity of the original design was noticeable. At this point, I stopped looking at the code and started looking through the issues and discussions to find any information regarding Servo, and it led me to a GitHub discussion written by a maintainer of MoveIt, regarding the design issues existing in MoveIt, which provided insight into the design goals that MoveIt was striving for. Now armed with the knowledge of Servo's current limitations, the expected results for the project, and a set of design goals to guide the new design, I went back to the Servo codebase for a detailed study.

The second analysis identified and isolated the core functionalities, use cases, and the data flow within MoveIt Servo. Based on the data gathered from this and the previous research, I prepared a design draft for the new implementation and presented it to the mentors. We finalized a design after a couple of iterations. 

At this point, the application period had started; I submitted my application which contained the proposed design, a rough timeline, and some relevant information about me. I had done everything as diligently as possible till then; the rest was up to the process. However, my motivation for participating in GSoC is to make meaningful open-source contributions, so I set out to find more issues to solve within MoveIt.

While going through the issues, I came across one that suggested changing a hardcoded parameter in the Butterworth filter plugin to a more configurable ROS 2 parameter using the generate_parameter_library. I found this issue interesting because one of the things that the proposal iterations added is the migration of Servo to generate_parameter_library, which is PickNik's solution to standardize the use of ROS2 parameters within MoveIt, as a stretch goal for the project. So I got to work figuring out how to integrate generate_parameter_library into the online_trajectory_smoothing package, which contained the Butterworth plugin; this exercise equipped me with the understanding necessary to finish the stretch goal easily, and I also ended up making another useful contribution.

The results are still half a month away, but I decided to tackle the stretch goal; if I ended up getting selected, I would have less work to do and could focus on more interesting elements of the project,  and if I did not get selected I would still have made progress on my original goal of creating more open-source contributions, with that decided, I mapped out the changes necessary to migrate Servo to use generate_parameter_library; even though the changes propagated throughout the codebase, they were not very involved, after one week of work, I had Servo migrated to generate_parameter_library, which was a significant contribution. As a bonus, I became more accustomed to the inner workings of Servo.

The GSoC selections came in on the 4th of May; MoveIt had two contributor slots, and I was one among them. It was a joyous moment; my dedication had paid off, and now I would get paid to do cool stuff. After a discussion with my mentors the next day, the official GSoC work started, May is for community bonding; however, there was already good communication between the mentors and me. In addition, I got introduced to the MoveIt maintainer meeting and met more of the people who kept MoveIt running. 

I immediately started experimenting with the new design for C++ APIs, as that was the main focus of this refactor; this was a significantly involved process as it required understanding not only the language constructs necessary to implement the design but also the robotics concepts and the significance of the mathematical operations used within Servo in addition to the MoveIt components. One month later, I had all the required C++ APIs working, along with a demo for each of those APIs.

Now came the part I knew would consume a major chunk of my time, writing the tests, mainly because I had limited exposure to testing and needed to learn how to set up tests when using ROS. The process took half a month, understanding the testing framework, figuring out the best way to test the APIs, and fixing any bugs found along the way. There was also a good refactoring of the inner logic of Servo to make it more test friendly and adhere to the design goals of MoveIt. The cause for this was that I followed the original implementation to some extent without questioning the validity of the signatures of some of the functions during my analysis, which introduced unnecessary dependencies that I could have identified in the design stage and avoided.

It was time for mentor reviews, and we evaluated the APIs, applied the necessary changes, and gave it a good round of testing. The foundation of the new Servo was ready now, and I proceeded to implement the ROS APIs. Due to the time invested in establishing a good design, getting the ROS APIs done was easy.


To be continued...