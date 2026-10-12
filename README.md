# Differential Drive Robot — Webots

A custom two-wheel robot built in Webots with a Python controller that repeatedly drives straight and performs approximately 90-degree turns, aiming to trace a square path.

## Current features

- Cylindrical robot body with two independently driven wheels.
- Collision geometry and physics for the body and wheels.
- Two decorative eyes on the front (+Y in the robot's local coordinates); these are not sensors.
- Time-based straight motion and in-place turns.

## Requirements

- Webots R2025a (the world file's declared version).
- Python 3 configured in Webots.
- Access to the referenced Webots PROTO assets, either cached or downloadable.

The controller imports Webots' bundled `controller` module. No additional Python packages are required by the current code.

## Run

1. Download or clone this repository, keeping the folder structure intact.
2. Open `worlds/empty.wbt` in Webots.
3. Confirm that the Robot controller field is `drive_my_robot`.
4. Start the simulation. Reset the simulation to restart the route.

Edit `controllers/drive_my_robot/drive_my_robot.py` to change the motion parameters, save it, and reset the simulation.

## Project files

| Path | Purpose |
| --- | --- |
| `worlds/empty.wbt` | Arena, custom robot geometry, joints, motors and physics |
| `controllers/drive_my_robot/drive_my_robot.py` | Python motion controller |
| `.gitignore` | Excludes generated and local workspace files |

The robot is defined directly in the world file; there is currently no separate custom PROTO file.

## Motion parameters

| Parameter | Current value |
| --- | --- |
| Wheel radius | 0.025 m |
| Wheel separation | 0.090 m |
| Commanded wheel angular speed | 6.28 rad/s |
| Target straight segment length | 0.25 m |
| Turn angle | Approximately 90 degrees |
| Controller timestep | 64 ms |

Straight duration is calculated from `length / (wheel_radius * angular_speed)`. Turn duration uses the ideal differential-drive rotation rate. Both wheel joint axes are `-1 0 0`; equal positive wheel speeds are intended to move toward the decorative eyes.

## Limitations

The controller is open-loop: it does not measure wheel position, robot position or obstacles. Simulation timestep, wheel slip and physical contacts can cause the actual path to differ from an exact square. It repeats indefinitely rather than stopping after four sides. The controller timestep must be compatible with the world's basic timestep.

## Next steps

- [ ] Add actual distance sensors and inspect their readings.
- [ ] Implement obstacle avoidance.
- [ ] Add wheel encoders and compare commanded versus measured motion.
- [ ] Add a simulation screenshot or short demonstration.

## Development history

This initial snapshot contains the current robot model and timed square-path controller. Record future working improvements as separate commits; update this README as behavior changes.
