# 3.5D Animation Skin Packs
---

## Overview

This repository documents the **3.5D animation method** for Minecraft Bedrock Skins. The method works by **explicitly binding existing mob animations to player animation channels** through `Skins.json`.

This approach does **not** modify the player geometry, but rather moves and resizes the players limbs.

The term *3.5D* is used to describe the method as a "middle man" between proper vanilla and 4D skins.

---

## Key Characteristics/Limitations

* Uses **existing Mojang player animation assets**
* No Molang queries or conditionals
* No script or controller animations work with the skins.json file
* No custom animation files (Unless pairing the skin-pack with a resource-pack)

---

## Installation/Getting Started

1. Download `Base.mcpack` from this repository.
2. Open the pack contents and locate the `Skins.json` file. This is where you'll be spending most of your time.
3. Read the rest of this document and then have fun making skins!

---

## `Skins.json` Example

```json
{
    "format_version": "1.10.0",
    "serialize_name": "name",
    "localization_name": "name",
    "skins": [
        {
            "localization_name": "name",
            "geometry": "geometry.humanoid.custom",
            "texture": "skin.png",
            "cape": "cape.png",
            "animations": {
                "humanoid_base_pose": "animation.humanoid.base_pose",
                "look_at_target": "controller.animation.humanoid.look_at_target",
                "cape": "animation.player.cape",
                "move.arms": "animation.player.move.arms",
                "sneaking": "animation.player.sneak",
                "move.legs": "animation.player.move.legs",
                "holding": "animation.player.holding",
                "attack.positions": "animation.player.attack.positions",
                "attack.rotations": "animation.player.attack.rotations",
                "bob": "animation.player.bob"
            },
            "type": "free",
            "enable_attachables": true
        }
    ]
}
```

## Geometry Usage

```json
"geometry": "geometry.humanoid.custom"
```

In 3.5D skin packs, geometry **does not define new models**. Its role is limited to selecting **classic (thick) or slim arm** variants

---

## Animation Bindings - The good stuff

The `animations` object is the core of this method.

Each entry maps a **skin animation slot** to an **existing player animation asset** that already exists in Bedrock.

Example:

```json
"move.arms": "animation.react_idle"
```

This does **not** define a new animation. It simply instructs minecraft to bind that animation directly to the skin instead of the defualt animation.

---

## Common Animation Channels

| Channel              | Description                                |
| -------------------- | ------------------------------------------ |
| `humanoid_base_pose` | Base bind pose used for animation layering |
| `move.arms`          | Arm motion while walking                   |
| `move.legs`          | Leg motion while walking                   |
| `sneaking`           | Legs when sneaking                         |
| `holding`            | Item holding offsets                       |
| `attack.positions`   | Arm positioning during attacks             |
| `attack.rotations`   | Swing rotation motion                      |
| `bob`                | Breathing-styled motion                    |
| `cape`               | Cape physics                               |
| `look_at_target`     | Head rotation                              |

- Please note almost every animation channel in the ``player.entity.json`` file can be used inside the ``skins.json`` file. The list above only shows the most commonly used animation in this method of skin modifications. 

---

## How to Hide Armor

```json
"enable_attachables": false
"hide_armor": true
```
* Please note, "enable attachables" also hides tridents or anything geometry based.
---


## Other key Points

* Custom animations do not render unless you are using a resource pack in addition with the skinpack, however this is only clientsided to those who have the resource pack enabled
* Bones/Limbs cannot be added, only removed
* Some animations work differently when targeted to a different channel
* Channels 'cape' and 'look_at_target_ui' are primarily UI based, 'cape' can have effects in game however its way more useful to use this channel to make your skin look less buggy in the user's interface

---

## Pointers
These are the main/primary animations used to move the skin around to get a desired shape/effect 

| Animation              | What It Does                              |
| -------------------- | ------------------------------------------ |
| `animation.witch.general` | Stops any/all orignal animations|
| `animation.evoker.general`   | Removes arms/torso area |
| `animation.parrot.sitting`    | Moves torso area down by roughly 2 pixels |
| `animation.axolotl.idle_floor_underwater`       | Moves torso area up by roughly 2 pixels |
| `animation.fireworks_rocket.move`    | Scales the players torso area to about 0.6, causes the torso to move with the players head |
| `animation.arrow.move`   | Same thing as the fireworks animations, but the head gets stretched |
| `animation.humanoid.big_headv1.0`   | Scales both the head and outler skin layers to two different sizes |
| `animation.enderman.scary_face`   | Moves the head higher than the outer skin layer, causing weird movement |
| `animation.tripod_camera.neutral`  | Moves the torso area to the floor  |
| `animation.elytra.default`      | Scales the torso area up by 1 pixel  |
| `animation.player.base_pose.upside_down`     | Makes the torso area of the skin upside-down  |
| `animation.strider.look_at_target.default`   | Fixes issues with 'animation.enderman.scary_face', 'animation.fireworks_rocket.move' and 'animation.arrow.move'  |
| `animation.goat.look_at_target` | Limits the players head movement slightly |

