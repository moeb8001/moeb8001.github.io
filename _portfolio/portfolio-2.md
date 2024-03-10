
---
title: "Minor Project - Physics Informed Neural Networks"
excerpt: "As Part of the AI minor at TU Delft, students spend the very last 3 weeks of their minor working full time on a project given by a Prof/Phd stuent from diff faculties. <br/>

collection: portfolio
---


As Part of the AI minor at TU Delft, students spend the last 3 weeks of the minor working full time on a project given by a Prof/Phd stuent from diff faculties. Students pick the projects and work in groups. For our project we worked on training a model with Unet architecture using CFD simulation results for a specific case, with constant boundary conditions.

One normal simulation, using OpenFoam, would take around an hour. Right now they have a ton of simulation results laying around. The aim was to use these to train a model (a UNET) to learn from these simulation results. This way the model can be used instead off using a CFD solver every single time a small thing changes in the input. With our trained model, one simulation takes less than a millisecond. Using a CFD solver it takes more than an hour, needing a lot more computational power.

Introduction:


https://github.com/moeb8001/moeb8001.github.io/assets/112695184/0e1ee0f4-06b8-47fd-9866-be1510b0dd7b



Dataset + Pre-processing:


![ezgif-4-06c7f1f7dd](https://github.com/moeb8001/moeb8001.github.io/assets/112695184/c10d641b-ae1c-4d68-9c54-d680d13dbe5c)
