Welcome to SimWorld's documentation!
====================================

**SimWorld** is a novel Unreal Engine-based simulator designed
to generate unlimited, diverse urban environments for embodied AI tasks.

Existing embodied simulators typically focus on indoor scenes.
There have been urban simulators, but they either lack realism or are
limited to autonomous driving. Critically, most of them do not allow users to
flexibly generate new scenes or define new embodied AI tasks. In contrast,
SimWorld provides a user-friendly Python API and diverse 3D assets that enable
users to procedurally generate realistic and dynamic city-scale environments
to support various Embodied AI research tasks. Our simulator can also be connected
with large language models (LLMs) to drive the behavior of different types of
agents (humans, vehicles, and robots) in the environments. The simulator features
infinite procedural scene generation, multi-agent interactions, and dynamic
environmental elements. It also supports photorealism rendering and physics
simulation powered by Unreal Engine 5.

.. note::

   This project is under active development.

Contents
--------

.. toctree::

   usage
   api
   traffic_system
   a2a
   procedural_generation