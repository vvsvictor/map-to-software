# Robotics

**Problem:** go from a task (*"pick up the ball and bring it back"*) to a robot that does it: describe the robot, simulate it, and write the software that controls it.

← Back to the [main README](../README.md)

---

## Recommended tool

| | |
|---|---|
| **DSL** | Robot description: [**URDF**](https://docs.ros.org/en/rolling/Tutorials/Intermediate/URDF/URDF-Main.html) or [**MJCF**](https://mujoco.readthedocs.io/en/stable/XMLreference.html) (XML) · Control: [**ROS 2**](https://docs.ros.org/) in Python (`rclpy`) |
| **Engine** | Simulation: [MuJoCo](https://mujoco.org/) or [Gazebo](https://gazebosim.org/) · Runtime: ROS 2 on the real robot |
| **Output** | A simulated and real robot executing the task |
| **Leaderboard** | None public yet (see Benchmarks) |

**Why:**

- **URDF** is the standard robot description in ROS; **MJCF** is MuJoCo's native format, with more accurate physics. Both are plain text.
- **ROS 2** is the most widely used robotics framework, with Python support and a huge ecosystem of drivers.
- **Simulation first**: the agent can test in MuJoCo or Gazebo before touching hardware, which makes the feedback loop fast and safe.

---

## Alternatives

| Tool | When to use it |
|---|---|
| Vendor SDKs (for example the Unitree SDK) | Controlling a specific commercial robot directly. |
| [NVIDIA Isaac Sim / Isaac Lab](https://developer.nvidia.com/isaac) | GPU simulation and reinforcement learning at scale. |
| [PyBullet](https://pybullet.org/) | Lightweight simulation and prototyping. |
| [SDF](http://sdformat.org/) | Gazebo's world and robot format, richer than URDF for full scenes. |

---

## Benchmarks

**Best model right now:** robotics has no public leaderboard for code generation yet. The benchmarks below report their results in their papers.

| Benchmark | What it measures | Results |
|---|---|---|
| RoboScript | Code generation for manipulation tasks with ROS and Gazebo. | No public leaderboard · [Paper](https://arxiv.org/abs/2402.14623) |
| RoboEval (CodeBotler) | Programs for service mobile robots. | No public leaderboard · [Paper](https://arxiv.org/abs/2311.11183) |
| RoboCoder | 80 tasks across 7 kinds of robot, including humanoids. | No public leaderboard · [Paper](https://arxiv.org/abs/2406.03757) |

---

## Used in practice

- [Project Fetch, phase one](https://www.anthropic.com/research/project-fetch-robot-dog) and [phase two](https://www.anthropic.com/research/project-fetch-phase-two) (Anthropic).
