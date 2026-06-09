---
sort: 16
---

# Level Dioramas

A level diorama is a self-contained 3D replica of a level that can be viewed without FEZEditor or the original game assets.

The editor includes a tool named **Phil** for creating these dioramas.

## Usage

1. Open the level in Eddy.
2. Open the tool via `Editor > Eddy > Export Level as Diorama...` in the menu bar.
3. Select a save path for the resulting `.glb` file.
4. Wait for the export to complete.

## What is a GLTF?

GLTF is a standard format for exchanging 3D scenes and models. It can store meshes, materials, textures, and scene hierarchy in a form supported by many 3D tools and viewers.

The editor exports dioramas as binary GLTF (`.glb`) files. A GLB packages the scene data and embedded resources into a single portable file.

## Viewing

Open the exported GLB file in a compatible 3D viewer. Here is an example of a level opened in [Babylon.js Sandbox](https://sandbox.babylonjs.com/):

![](/wiki/assets/images/editor/eddy_diorama.png)

## Purpose

This feature was originally created for ripping levels for [The Models Resource](https://models.spriters-resource.com/pc_computer/fez/). Although, another custom solution was made, the exporter was kept for future reference.

Think about this feature also as a small tribute to [Michael Romero](https://github.com/halogenica) and his inspirational [FezViewer](https://halogenica.net/tools/fez-viewer/) tool.
