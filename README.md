# Mission Unified

A quadcopter bolted directly to a two-wheel ground chassis, so one vehicle both drives and
flies. No folding, no docking, no reconfiguring: the chassis is the drone's landing pad,
and the platform switches between rolling and flying as the mission needs. While it moves,
it detects objects in its camera feed, keeps track of them from frame to frame, and works
out where each one sits on the ground as a latitude and longitude.

Built as a B.Eng final-year project in the Department of Aerospace Engineering, Faculty of
Air Engineering, Air Force Institute of Technology, Kaduna.

![The platform: quadcopter and ground chassis as one airframe](images/platform-outdoor.jpg)

## The documentary

The whole build, from unboxing and soldering to assembly, flight and defence, was filmed:

**[MISSION UNIFIED | The Engineering Documentary](https://www.youtube.com/playlist?list=PLYnxBdsCVqNE)**

## How it works

![System architecture](images/system-architecture.png)

The platform carries the camera, the flight controller and the sensors. A wireless link
sends video and telemetry down to a ground station with a GPU on it. On the ground:

1. Telemetry arrives over a serial link — position, altitude, attitude, battery, link
   quality — and is parsed and timestamped against the video.
2. Each frame goes through object detection, then a tracker that holds an identity on a
   target across frames rather than treating every frame as new.
3. For each detection, the pixel position is projected onto the ground, using the camera
   calibration, the camera's mounting angles and the platform's attitude, to give a ground
   coordinate.
4. A dashboard shows telemetry, the annotated video and the vehicle state, and sends
   commands back to the platform.

Steps 1 to 4 are the software in
**[mission-unified-software](https://github.com/Mission-Unified/mission-unified-software)**.

| Telemetry | Command overview | Vision |
|---|---|---|
| ![](images/dashboard-telemetry.png) | ![](images/dashboard-command.jpg) | ![](images/dashboard-vision.jpg) |

## Design

The chassis was designed as a single airframe rather than two vehicles that meet. The wheel
axle sits under the arms, and the landing feet double as the ground contact.

| | |
|---|---|
| ![](images/cad-views-1.jpg) | ![](images/cad-views-2.jpg) |

![Isometric view](images/cad-isometric.jpg)

## Repositories

| Repository | Contents | Licence |
|---|---|---|
| [mission-unified](https://github.com/Mission-Unified/mission-unified) | This one: overview, photographs, system description, documentary | CC BY 4.0 |
| [mission-unified-software](https://github.com/Mission-Unified/mission-unified-software) | Ground station: telemetry, detection, tracking, geolocation, dashboard | MIT |
| mission-unified-hardware | CAD, drawings, bill of materials, assembly notes | CC BY 4.0 |

The hardware repository is not published yet.

## The build

| | | |
|---|---|---|
| ![](images/platform-indoor.jpg) | ![](images/presentation-3.jpg) | ![](images/team.jpg) |

## Team

John Obaloluwa Ayodele designed and built the system and wrote the software.
Supervised by Engr Rexcharles Enyinna Donatus.

The documentary, the CAD work and the build were a team effort, and the people involved are
credited as they join this organization.

## Licence

Text, photographs and diagrams in this repository are licensed
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/): use them anywhere, including
commercially, as long as you credit Mission Unified. Software is licensed separately in its
own repository.
