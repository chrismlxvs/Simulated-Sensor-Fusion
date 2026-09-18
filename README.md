# CompVisProject

CompVisProject is a simulated mobile-robot perception stack for experimenting with LiDAR, camera sensing, odometry, mapping, and sensor fusion. The project uses PyBullet to simulate a four-wheel skid-steer robot moving through a configurable room with obstacles.

## Features

- Real-time PyBullet simulation with keyboard teleoperation
- Configurable 3D LiDAR sensor with multi-channel scanning
- Configurable RGB camera sensor
- LiDAR odometry using ICP scan registration
- Global point-cloud mapping with voxel downsampling
- LiDAR-to-camera projection and visualization
- Ground-truth trajectory comparison for odometry evaluation

## Requirements

- Python 3.10 or newer
- A desktop environment capable of opening PyBullet, OpenCV, Matplotlib, and Open3D windows
- PyBullet 3.2.5 or newer

## Quick Start

From the repository root, activate the virtual environment and start the interactive simulation:

```powershell
python scripts\run_simulation.py
```

Use the arrow keys to drive the robot:

- Up arrow: drive forward
- Down arrow: drive backward
- Left arrow: turn left
- Right arrow: turn right
- `Ctrl+C`: stop the simulation

## Workflows

### Basic simulation

```powershell
python scripts\run_simulation.py
```

Starts the PyBullet environment and robot simulation. This is the simplest way to inspect the simulated scene and sensor behavior.

### LiDAR odometry

```powershell
python scripts\run_lidar_odometry.py
```

Builds an ICP-based estimated trajectory while the robot is driven. Press `Ctrl+C` to stop and display a plot comparing estimated motion with ground truth.

### Global LiDAR mapping

```powershell
python scripts\build_lidar_map.py
```

Accumulates LiDAR scans in the world frame and opens an Open3D point-cloud visualization when the program is stopped with `Ctrl+C`.

### Camera-LiDAR sensor fusion

```powershell
python scripts\visualize_sensor_fusion.py
```

Projects visible LiDAR points into the camera image and displays the overlaid result in an OpenCV window. Drive the robot with the arrow keys and stop with `Ctrl+C`.

## Configuration

All workflows load their settings from `config/`:

| File | Purpose |
| --- | --- |
| `simulation.yaml` | Simulation timestep, gravity, room size, wall height, and obstacle count |
| `robot.yaml` | Robot dimensions, mass, starting pose, and motion limits |
| `lidar.yaml` | LiDAR frequency, range, channels, field of view, resolution, and mounting offset |
| `camera.yaml` | Camera resolution, field of view, frame rate, and mounting offset |
| `mapping.yaml` | Point-cloud voxel size, maximum point count, and live visualization settings |

For example, the default simulation runs at 100 Hz, scans with a 16-channel LiDAR at 10 Hz, and uses a 640 x 480 camera at 10 FPS.

## Project Structure

```text
config/          Sensor, robot, simulation, and mapping parameters
scripts/         Executable simulation and perception workflows
src/geometry/    Rigid transforms and rotation utilities
src/mapping/     Global point-cloud map construction
src/odometry/    LiDAR odometry
src/perception/  ICP registration and camera-LiDAR projection
src/simulation/  PyBullet world, robot, and sensor simulation
```

## Notes

- Run commands from the repository root so the scripts resolve `config/` and `src/` correctly.
- The default configuration enables the PyBullet GUI. The mapping, odometry, and sensor-fusion workflows are interactive and require a windowed desktop session.
- The scripts use ground-truth robot poses for map placement and odometry evaluation; this is intended for simulation and benchmarking rather than deployment on physical hardware.
- There is currently no automated test suite included.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for the full text.