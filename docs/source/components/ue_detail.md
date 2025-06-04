# Unreal Engine Integration

## Assets

Our simulator provides a rich collection of city-scale assets, designed to support realistic and diverse urban simulations. These assets include buildings, trees, street furniture, vehicles, pedestrians, and robots. All assets are sourced from the Unreal Engine Marketplace to ensure high visual fidelity and performance.

In addition to the curated asset library, we also offer an **Asset Generation Pipeline** that enables users to create `.uasset` files directly from natural language descriptions. This tool streamlines the content creation process by converting user prompts into usable Unreal Engine assets, significantly lowering the barrier for customizing city environments.

### Collected Assets

Below is a selection of the assets currently available in our simulator:

* **Buildings**: A variety of architectural styles, including residential, commercial, and industrial structures.
* **Trees**: Multiple tree species with seasonal variations to enhance environmental realism.
* **Street Furniture**: Items such as benches, streetlights, boxes, and trash bins to add detail and immersion.
* **Vehicles**: A range of vehicles including cars, buses, trucks, and scooters, each with accurate scale and animations.
* **Pedestrians**: Human characters with diverse appearances and animations to simulate crowd behavior.
* **Robots**: Different types of mobile robots for testing autonomous navigation and interaction, such as humanoid and robot dog.

These assets collectively enable the creation of complex, dynamic, and realistic city scenes for simulation, visualization, and research purposes.

```{image} ../assets/assets.png
:width: 800px
:align: center
:alt: A Subset of Collected Assets
```

### Asset Generation Pipeline

Our **Asset Generation Pipeline** enables the automatic generation of 3D assets from natural language descriptions. This tool is currently designed for developers and is intended to be used within the Unreal Engine Editor. By translating descriptive text into `.uasset` files, this pipeline significantly accelerates asset creation, making it easier to populate large-scale environments with customized elements.

```{warning}
**Asset Generation Pipeline** can only be used in editor mode.
```

## Actions

To enhance realism and interactivity in the simulation, we provide a comprehensive set of **Action Space**, with a strong focus on animations for pedestrians and robots. These actions are essential for simulating lifelike behaviors such as walking, running, waving, interacting with objects, and more. All actions are sourced from the Unreal Engine Marketplace to ensure quality and compatibility.

Here are some examples of actions included in the simulator:

```{todo}
Add a table here
```

## Sensors


## Synchronous and Asynchronous mode