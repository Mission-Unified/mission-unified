# Mission Unified

One vehicle that drives and flies. A quadcopter sits bolted to a two-wheel chassis, and the
chassis doubles as the landing pad, so nothing folds out and nothing docks. While it moves,
it detects objects in its camera feed, holds an identity on each one from frame to frame,
and works out where each sits on the ground as a latitude and longitude.

Built as a B.Eng final-year project in the Department of Aerospace Engineering, Faculty of
Air Engineering, Air Force Institute of Technology, Kaduna.

![The platform driving across the floor on its wheels, propellers still](images/driving.gif)

Same airframe, wheels turning. Lift off and the wheels come with it.

![The platform: quadcopter and ground chassis as one airframe](images/platform-outdoor.jpg)

## The documentary

We filmed the build. Unboxing, soldering, assembly, the first flights, the defence.

[![MISSION UNIFIED | Chapter 1: The Mission Begins](https://img.youtube.com/vi/DgTH5Ho2aX0/maxresdefault.jpg)](https://youtu.be/DgTH5Ho2aX0)

**[Chapter 1: The Mission Begins](https://youtu.be/DgTH5Ho2aX0)** ·
[full playlist](https://www.youtube.com/playlist?list=PLYnxBdsCVqNE)

## How it works

![System architecture](images/system-architecture.png)

The platform carries the camera, the flight controller and the sensors. A wireless link
sends video and telemetry to a ground station with a GPU in it. On the ground:

1. Telemetry arrives over a serial link (position, altitude, attitude, battery, link
   quality), gets parsed, and is lined up against the video frames.
2. Every frame goes through object detection, then a tracker that holds an identity on a
   target across frames instead of treating each frame as new.
3. Each detection's pixel position is projected onto the ground using the camera
   calibration, the camera's mounting angles and the platform's attitude. That gives a
   coordinate.
4. A dashboard shows the telemetry, the annotated video and the vehicle state, and sends
   commands back.

All four steps are the software in
[mission-unified-software](https://github.com/Mission-Unified/mission-unified-software).

![The dashboard reading live ultrasonic distances, vehicle on the bench behind](images/dashboard-live.gif)

Obstacle distances updating as the vehicle moves, with the vehicle itself sitting behind
the laptop.

| Telemetry | Command overview | Vision |
|---|---|---|
| ![](images/dashboard-telemetry.png) | ![](images/dashboard-command.jpg) | ![](images/dashboard-vision.jpg) |

## Where a target actually is

Turning a pixel into a coordinate is geometry, and the geometry is unforgiving: a small
attitude error multiplies by altitude before it reaches the ground. The maths got worked
out on a whiteboard before it went into code.

![Whiteboard working: camera angle, slant range and the ground triangle](images/geometry-sketch.jpg)

Then the camera has to be calibrated, because the projection is only as good as the lens
model behind it. A printed checkerboard, several dozen captures, and the matrix that comes
out of it ends up in `config/geolocation.py`.

![Calibrating the camera with a printed checkerboard](images/camera-calibration.jpg)

## Design

The wheel axle sits under the arms and the landing feet are the ground contact. One
airframe, no docking mechanism, no transformation sequence to go wrong mid-mission.

| | |
|---|---|
| ![](images/cad-views-1.jpg) | ![](images/cad-views-2.jpg) |

![Isometric view](images/cad-isometric.jpg)

## Building it

It started as a breadboard, a 2WD chassis and a lot of jumper wire.

| | |
|---|---|
| ![Bench wiring: motors, drivers, sensors](images/bench-wiring.jpg) | ![Reviewing the drawings](images/design-review.jpg) |
| ![The flight controller](images/flight-controller.jpg) | ![The sensor head: twin ultrasonics and the camera mount](images/sensor-head.jpg) |

| | |
|---|---|
| ![The finished platform from above](images/platform-top.jpg) | ![Out on the grass](images/platform-field.jpg) |

## Repositories

| Repository | Contents | Licence |
|---|---|---|
| [mission-unified](https://github.com/Mission-Unified/mission-unified) | This one: overview, photographs, system description, documentary | CC BY 4.0 |
| [mission-unified-software](https://github.com/Mission-Unified/mission-unified-software) | Ground station: telemetry, detection, tracking, geolocation, dashboard | MIT |

CAD, drawings and build files get their own home later.

## The team

| | | |
|---|---|---|
| ![](images/platform-indoor.jpg) | ![](images/presentation-3.jpg) | ![](images/team.jpg) |

John Obaloluwa Ayodele designed and built the system and wrote the software. Engr
Rexcharles Enyinna Donatus supervised the project.

The documentary, the CAD work and the build were a team effort. Everyone involved is
credited here as they join the organization.

## Licence

Text, photographs, video stills and diagrams here are under
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Use them anywhere, including
commercially, as long as you credit Mission Unified. Software carries its own licence in
its own repository.
