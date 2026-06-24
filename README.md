# a workflow from Figma URL to Unity uGUI prefab

If you want to use AI to improve the efficiency of creating Unity uGUI prefabs based on Figma, this workflow can be used as a reference.

## Overview

This workflow consists of three main parts:

1. Use an AI model to understand a specific Figma page design and generate a JSON file that describes the Unity prefab hierarchy.
2. In the Unity Editor, convert the hierarchy description from step 1 into an actual prefab asset.
3. Review and adjust the generated prefab.

These three steps currently require some manual handoff. In real production usage, you can connect step 1 and step 2 with additional automation, such as MCP.

## Setup

### 0. Create or Open a Unity Project

Create a new Unity project, or use an existing one.

### 1. Install Figma to uGUI Hierarchy

Install [Figma to uGUI Hierarchy](https://github.com/beddup/FigmaToUGUIHierarchy.git) in your Unity project or workflow environment.

This package contains the skills, subagents, scripts, and workflow instructions used to generate the Unity prefab hierarchy description file.

Invoke `figma_to_ugui_hierarchy` in Claude Code or Codex, and provide a Figma URL that contains a `node-id`.

Example:

```text
Use skill figma_to_ugui_hierarchy to process:
https://www.figma.com/design/<file-key>/<name>?node-id=123-456
```

The workflow will generate a JSON file under `Assets/FigmaAssets`. Its structure looks like this:

```json
{
  "figma_url": "figma url",
  "file_key": "file key parsed from figma url",
  "api_token": "figma api token",
  "node_id": "root node id parsed from figma url",
  "node_name": "root node name",
  "working_dir_path": "path for intermediate files",
  "raw_content_path": "raw Figma data for the Figma URL",
  "content_screen_path": "screenshot of the Figma node",
  "prefab_hierarchy_path": "Unity prefab hierarchy description file"
}
```

### 2. Install Figma uGUI Prefab Builder

Install [Figma uGUI Prefab Builder](https://github.com/beddup/FigmaUGUIPrefabBuilder.git).

This module uses the result generated in the previous step to create the actual Unity prefab asset.

It depends on the following two packages:

- [Figma TMP Styler](https://github.com/beddup/FigmaTMPStyler.git), used to create TextMeshPro font materials.
- [Simple Figma Client](https://github.com/beddup/figmaclient.git), used to export Figma images.

### 3. Install Unity Canvas Device Preview (Optional)

Install [Unity Canvas Device Preview](https://github.com/beddup/UnityCanvasDevicePreview.git) if you want a faster way to review how the generated uGUI Canvas appears on different devices.

