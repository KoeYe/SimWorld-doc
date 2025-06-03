# Traffic System

## Overview

```{todo}
need a figure here
```

The **Traffic System** is a core component of our simulator, responsible for simulating dynamic road usage by both vehicles and pedestrians. It enables the representation of realistic traffic flow, including vehicle generation, path planning, intersection control, and pedestrian behavior. By managing road interactions and traffic signals, this system supports complex urban scenarios such as congestion, pedestrian crossings, and traffic light coordination, providing a critical foundation for evaluating urban infrastructure and mobility policies.

## Architecture

```{image} ../assets/traffic_arc.png
:width: 800px
:align: center
:alt: Traffic System Architecture
```

The traffic system adopts a modular architecture centered around a top-level `TrafficController`, which coordinates the behavior of three specialized managers: `VehicleManager`, `IntersectionManager`, and `PedestrianManager`.

To enable real-time simulation, the system integrates with Unreal Engine through the `Communicator` module, which provides bidirectional communication between the traffic logic and the simulation environment. This allows the system to send control signals and receive state updates from virtual actors within the engine.

The traffic system is composed of several modular components that collectively simulate realistic urban mobility. The system is initialized based on a **Road Network**, which provides the geometric and topological structure of the city. 

- **Traffic Network Generator**: This module constructs the simulation-ready traffic network from the road layout. It generates essential components including **Traffic Lanes** for vehicles, **Sidewalks** for pedestrians, and **Crosswalks** for pedestrian-vehicle interactions at intersections.
- **Traffic Controller**: Acting as the central coordinator, this module manages the initialization and runtime orchestration of all traffic-related components. It interfaces with the **Communicator** to synchronize with the Unreal Engine, enabling real-time bidirectional updates.
- **Vehicle Manager**: This component samples spawn points along the traffic lanes to instantiate and manage **Vehicles**. It governs routing, movement, and state updates in coordination with the traffic controller and PID logic.
- **Pedestrian Manager**: Responsible for spawning **Pedestrians** on sidewalks and controlling their navigation, especially when interacting with crosswalks and intersection logic.
- **Intersection Manager**: Identifies and manages **Intersections** in the traffic network. It places and controls **Traffic Signals** to regulate vehicle and pedestrian flow based on predefined or adaptive timing schemes.
- **PID Controller**: A low-level control module responsible for computing continuous control signals (e.g., turning) for vehicles, ensuring smooth movement and realistic behavior along generated paths.