# Vantage

Vantage is a small Defold camera controller for quickly adding mouse, keyboard,
and touch-driven 3D camera movement to a project.

The extension includes a ready-to-use camera component, a sample input binding
file, and a minimal example scene. It is intended for prototypes, 3D samples,
debug cameras, level viewers, and other projects that need a simple camera
without building the input handling from scratch.

## Features

- WASD-style first-person camera movement.
- Mouse-look rotation.
- Q/E vertical movement.
- Optional orbital camera mode.
- Basic two-zone touch controls on mobile devices.
- Runtime properties for movement speed, rotation speed, zoom, and camera mode.
- Example project showing how to switch camera modes at runtime.

## Installation

Add Vantage as a dependency in your `game.project` file:

```ini
[project]
dependencies = https://github.com/Jhonnyg/defold-vantage/archive/refs/heads/master.zip
```

Then fetch libraries from the Defold editor.

## Setup

1. Add a camera component to a game object.
2. Add `/vantage/vantage_component.script` to the same game object.
3. Add the Vantage input actions to your project's input binding, or use the
   included `/vantage/vantage.input_binding` file.
4. Make sure the camera game object is included in the collection you want to
   control.

The component acquires input focus automatically during `init()`.

## Input Actions

Vantage listens for the following action names:

| Action | Default binding | Description |
| --- | --- | --- |
| `VANTAGE_W` | W | Move forward |
| `VANTAGE_S` | S | Move backward |
| `VANTAGE_A` | A | Strafe left |
| `VANTAGE_D` | D | Strafe right |
| `VANTAGE_Q` | Q | Move down |
| `VANTAGE_E` | E | Move up |
| `VANTAGE_MOUSE_1` | Left mouse button | Rotate the camera with mouse movement |
| `VANTAGE_WHEEL_UP` | Mouse wheel up | Zoom in orbital mode |
| `VANTAGE_WHEEL_DOWN` | Mouse wheel down | Zoom out orbital mode |
| `VANTAGE_TOUCH_MULTI` | Multi-touch | Touch movement and rotation on mobile |

The sample binding also includes `EXAMPLE_1` and `EXAMPLE_2`, which are used by
the example scene to switch between first-person and orbital camera modes.

## Component Properties

The `vantage_component.script` exposes these properties in the editor:

| Property | Type | Default | Description |
| --- | --- | --- | --- |
| `orbital_camera` | Boolean | `false` | Switches between first-person and orbital camera behavior. |
| `movement_speed` | Number | `20` | Camera movement speed. In orbital mode this also controls wheel zoom steps. |
| `rotation_speed` | Number | `0.25` | Mouse and touch rotation sensitivity. |
| `zoom` | Number | `5` | Base distance used by orbital camera mode. |

You can also change these properties at runtime:

```lua
local camera = "/camera#vantage_component"

go.set(camera, "movement_speed", 5)
go.set(camera, "rotation_speed", 0.2)
go.set(camera, "orbital_camera", true)
go.set(camera, "zoom", 8)
```

## Example Project

The included sample project contains a simple 3D scene with a Vantage-controlled
camera.

- Press `1` to use first-person camera mode.
- Press `2` to use orbital camera mode.
- Use W/A/S/D/Q/E and the mouse to move around.

## Mobile Touch Controls

On Android and iOS, Vantage enables touch controls automatically:

- Touches on the left half of the screen move the camera.
- Touches on the right half of the screen rotate the camera.

The touch controls are intentionally minimal and are best treated as a starting
point for project-specific mobile camera controls.

## Notes

- Vantage assumes the input action names listed above. If you merge the input
  actions into an existing binding file, keep the action names unchanged.
- The first-person camera mode is the primary supported mode.
- Orbital camera mode is included for experimentation and may need project
  specific adjustments before use in production.
