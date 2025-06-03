# Waypoint System

## Overview
To facilitate robust agent navigation and path planning within the simulated environment, SimWorld incorporates a customizable waypoint system that serves as the foundational representation of navigable space. This system is initially constructed using a coarse-grained waypoint skeleton derived from the output of the **Layout Generation** pipeline. Specifically, the pipeline produces high-level geometric features of the environment, such as road centerlines and intersection points, which are then used to define the topological structure of the navigation graph.

## Granularity
The granularity of waypoint system is customized. User can specify the number of waypoints and the distance between waypoints.

**Related class: `map.py`**

To initialize a map:
```python
map = Map(config)
map.initialize_map_from_file(roads_file, sidewalk_offset, fine_grained, num_waypoints_normal, waypoints_distance, waypoints_normal_distance)
```
+ `roads_file`: generated from Layout Generation.
+ `sidewalk_offset`: distance between road centerline and sidewalk centerline.
+ `fine_grained`: whether to enable interpolation to build a fine-grained map.
+ `num_waypoints_normal`: number of waypoints in normal direction of the sidewalk.
+ `waypoints_distance`: distance between waypoints in radical direction.
+ `waypoints_normal_distance`: number of waypoints in normal direction.

```{todo}
figure here
```