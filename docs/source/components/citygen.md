# Layout Generation

The **Layout Generation** module is a key component of the SimWorld simulator, responsible for generating realistic city layouts from simple input specifications. This module provides a flexible and extensible framework for creating diverse urban environments that can be used for various embodied AI tasks.

## Data Structure

A city layout contains many different types of elements. While it's impractical to catalog every possible item in a city, we can simplify our understanding by grouping all items into **4** main categories:

| **Road**    | Highway          | Normal way  | Small roads | ... |
|-------------|------------------|-------------|-------------|-----|
| **Building**| Hospital         | Landmark    | School      | ... |
| **Detail**  | Tree             | Bone        | Parking cars| ... |
| **Actor**   | Cars on the road | Pedestrian  | Agent       | ... |

## Procedural Generation

Procedural generation is a fundamental method for creating city layouts that resemble the real world. Using this approach, all items in the generated world follow specific rules and constraints. These constraints control how different items are distributed, ensuring the city layout appears organized rather than random. 

### Code Structure

```{image} ../assets/clpg_arc.png
:width: 400px
:align: center
:alt: Layout Generation Overview
```

The city generator includes three managers: Road, Building, and Detail. Each manager contains list and quadtree data structures to store item information. QuadTree provides fast methods for searching space-related information, such as nearby objects. Lists offer a convenient way to iterate through items. 

Generators contain various algorithms for generating and sampling candidate positions for items while handling overlapping situations. They offer constraints and rules of generation.

The Road manager serves as the foundation for the city, followed by the Building manager. The Detail manager generates content based on data from the Road and Building managers through the generator.

### Generation Process

There are 4 stages of generation process: road generation, building generation, detail generation and data generation

#### Road

Road generation consists of two sub-stages: initiation and road-tree growth.

##### Initiation

In the initiation stage, the program reads the config file, focusing on the road length and initial road count. It then spawns the first one or two roads on the map, which by default have a constant length as specified in the config and a 0-degree angle with the x-axis.

##### Road-Tree growth

Using the initial road(s) as a foundation, we generate additional roads through a tree-like growth structure.

```{image} ../assets/clpg_road_1.png
:width: 400px
:align: center
:alt: Road Generation
```

To balance the road tree's depth and branch numbers, we use a Priority Queue instead of simple DFS or BFS iteration algorithms. The Priority Queue, implemented as a tree structure, helps select growth nodes from the generated road tree. This approach creates a road map with balanced branches and depth, better resembling real city or town road layouts.

During generation, we handle two special cases: closely spaced road endpoints and intersecting road segments.

##### Road end attachment

During generation, when a newly generated road endpoint is very close to an existing node, it creates an unsightly gap. In such cases, we attach the new node to the existing one, eliminating gaps while creating more diverse road lengths.

```{image} ../assets/clpg_road_2.png
:width: 400px
:align: center
:alt: Road Attachment
```

##### Cross check

Despite the attachment mechanism, road intersections can still occur. We perform additional intersection checks during generation. If any roads intersect, we remove the most recently generated one.

#### Building

Building generation is based on the generated road maps. From a list of roads, we select one road segment and generate buildings along both sides. For each side, the generation process has two stages: normal generation and final building placement. The main goal is to create a uniform distribution of different building types while maximizing space utilization on the map.

##### Normal generation

A pointer tracks the current position for candidate buildings. During generation, the pointer's position updates based on the building size and road angle. The pseudo code for pointer updates is shown as follows:

```python
pointer_position = road_start * side * offset + margin_distance
while pointer_position < road_end * side * offset - margin_distance:
   pointer_position += building_size * angle
```

In each iteration, we randomly select a building type from the building database and check if it can be placed at the current position without overlapping with roads or other buildings.

```{image} ../assets/clpg_building.png
:width: 400px
:align: center
:alt: Building Generation
```

##### The last building on the road

When the pointer approaches the road's end, most candidate buildings may not fit the remaining space. To fill this gap efficiently, we greedily select buildings from largest to smallest until one fits. After placement, we update the pointer's position and continue to the next iteration. Only when no building can fit in the remaining road space do we move to the other side of the road or the next road segment.

#### Details

Details refer to the smaller objects in a city, including trees, road cones, chairs, tables, scooters, and other items. These objects are distributed throughout every corner of the city. To simplify their generation process, we use two different approaches: details surrounding buildings and details along roads. Note that we don't consider collisions between details and other objects—we only check if positions are accessible. This is a practical trade-off between computational efficiency and visual effect, given the large number of details.

##### Details surround building
    
For each building, we sample a constant number of detail positions within a suitable range. We then check whether these candidate positions are available, since some may be in the middle of roads or inside other buildings. The sampling area consists of two rectangular zones, excluding the side closest to the road.

```{image} ../assets/clpg_detail_1.png
:width: 400px
:align: center
:alt: Element Generation
```
    
##### Details spline road
    
Along the roads, we divide the sidewalk area into different functional parts: vegetation, random objects, and parking areas. We generate different types of detail items according to each area. The density of items varies by area, offering greater customization and creating a cleaner, more suitable sidewalk appearance. Three functional parts are divided by distance from the road's middle line:

```{image} ../assets/clpg_detail_2.png
:width: 400px
:align: center
:alt: Element Generation
```
    