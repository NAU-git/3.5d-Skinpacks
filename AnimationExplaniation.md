# Minecraft Bedrock Player Animation Reference
## Vanilla Resource Pack v26.0.0 - Complete Re-Scan

---

## Player Limb Hierarchy

```
root
├── waist
│   ├── body
│   │   ├── head
│   │   │   └── hat
│   │   ├── cape
│   │   ├── jacket
│   │   ├── leftArm
│   │   │   ├── leftSleeve
│   │   │   └── leftItem
│   │   └── rightArm
│   │       ├── rightSleeve
│   │       └── rightItem
├── leftLeg
│   └── leftPants
└── rightLeg
    └── rightPants
```

### Bone Reference Table

| Bone | Parent | Description |
|------|--------|-------------|
| `root` | — | Top-level transform for the entire entity |
| `waist` | root | Hip/waist joint |
| `body` | waist | Torso/chest |
| `head` | body | Head |
| `hat` | head | Hat layer (overlay) |
| `cape` | body | Cape/back accessory |
| `jacket` | body | Jacket layer (overlay) |
| `leftArm` | body | Left arm |
| `leftSleeve` | leftArm | Left arm sleeve (overlay) |
| `leftItem` | leftArm | Item held in left hand |
| `rightArm` | body | Right arm |
| `rightSleeve` | rightArm | Right arm sleeve (overlay) |
| `rightItem` | rightArm | Item held in right hand |
| `leftLeg` | root | Left leg |
| `leftPants` | leftLeg | Left leg pants (overlay) |
| `rightLeg` | root | Right leg |
| `rightPants` | rightLeg | Right leg pants (overlay) |

---

## Scan Statistics

**Total: 218 animations across 69 files** affect player bone names.

### Bones by Frequency

| Bone | Animation Count | Notes |
|------|----------------|-------|
| `body` | 136 | Most commonly affected bone |
| `head` | 128 | Second most common |
| `rightitem` | 18 | Armor stand poses, bow/crossbow |
| `leftarm` (lowercase) | 39 | Mob-specific (enderman, piglin, etc.) |
| `rightarm` (lowercase) | 37 | Mob-specific (enderman, piglin, etc.) |
| `leftleg` (lowercase) | 17 | Armor stand, enderman |
| `rightleg` (lowercase) | 17 | Armor stand, enderman |
| `leftArm` (camelCase) | 7 | Player-compatible (agent, armor) |
| `rightArm` (camelCase) | 8 | Player-compatible (agent, armor) |
| `leftLeg` (camelCase) | 6 | Player-compatible (agent, armor) |
| `rightLeg` (camelCase) | 6 | Player-compatible (agent, armor) |
| `leftItem` | 2 | Vex, vindicator |
| `rightItem` | 7 | Allay, copper golem, vex, vindicator |
| `hat` | 2 | Enderman only |
| `root` | 2 | Camel, ender dragon |

**IMPORTANT**: Many mob animations use lowercase bone names (`leftarm`, `rightarm`, `leftleg`, `rightleg`, `rightitem`) which do NOT match player bone names (`leftArm`, `rightArm`, `leftLeg`, `rightLeg`, `rightItem`). Only animations using camelCase player bone names will affect the player model.

---

## BABY MOB ANIMATIONS (Head Affecting)

These animations are designed for baby mobs but use the `head` bone, which means they WILL affect the player's head if applied.

| File | Animation | Bones | Transform Details |
|------|-----------|-------|-------------------|
| `cat.animation.json` | `animation.cat.baby_transform` | head | **scale=uniform 1.5** |
| `chicken.animation.json` | `animation.chicken.baby_transform` | head | **scale=uniform 2.0** |
| `cow.animation.json` | `animation.cow.baby_transform` | head | position=[0, 4, 4] \| scale=uniform 2.0 |
| `fox.animation.json` | `animation.fox.baby_transform` | head | scale=uniform 1.5 |
| `goat.animation.json` | `animation.goat.baby_scaling` | head | scale=uniform 1.0-1.5 (varies) |
| `hoglin.animation.json` | `animation.hoglin.baby_scaling` | head | scale=uniform 1.0-1.5 (varies) |
| `horse_v1.animation.json` | `animation.horse.baby_transform` | body, head | body: position + scale \| head: scale=uniform 2.0 |
| `horse_v2.animation.json` | `animation.horse.v2.baby_transform` | body, head | body: position + scale \| head: scale=uniform 2.0 |
| `horse_v3.animation.json` | `animation.horse.v3.baby_transform` | body, head | body: position + scale \| head: scale=uniform 2.0 |
| `llama.animation.json` | `animation.llama.baby_transform` | body, head | body: position + scale \| head: scale=uniform 1.5 |
| `mooshroom.animation.json` | `animation.mooshroom.baby_transform` | head | position=[0, 4, 4] \| **scale=uniform 2.0** |
| `npc.animation.json` | `animation.npc.baby_transform` | head | **scale=uniform 1.5** |
| `ocelot.animation.json` | `animation.ocelot.baby_transform` | head | **scale=uniform 1.5** |
| `panda.animation.json` | `animation.panda.baby_transform` | body, head | body: position + scale=[1.15, 1.15, 1.0] \| head: position + **scale=uniform 1.8** |
| `pig.animation.json` | `animation.pig.baby_transform` | head | position=[0, 4, 4] \| **scale=uniform 2.0** |
| `polar_bear.animation.json` | `animation.polarbear.baby_transform` | head | position=[0, -1, 3] \| **scale=uniform 1.25** |
| `rabbit.animation.json` | `animation.rabbit.baby_transform` | head | position=[0, -1, 1] \| **scale=uniform 1.5** |
| `sheep.animation.json` | `animation.sheep.baby_transform` | head | position=[0, 4, 4] \| **scale=uniform 2.0** |
| `sniffer.animation.json` | `animation.sniffer.baby_transform` | head | position=[0, 1, 1] \| **scale=uniform 1.2** |
| `villager.animation.json` | `animation.villager.baby_transform` | head | **scale=uniform 1.5** |

---

## CAT ANIMATIONS (Torso/Body Affecting)

These animations use the `body` bone, which affects the player's torso.

| File | Animation | Bones | Transform Details |
|------|-----------|-------|-------------------|
| `cat.animation.json` | `animation.cat.lie_down` | body, head | body: position=[0, -4.5*liedownamount + lieonplayer*(4.5+is_baby*6), 0] \| rotation=[0, 0, lerprotate(0, 90, liedownamount)] \| head: position=[-0.1, 0, -0.5] \| rotation=[-10, lerprotate(this, 75.81, liedownamount), 0] |
| `cat.animation.json` | `animation.cat.sit` | body, head | body: position=[0, -1, 0] \| **rotation=[-45, 0, 0]** \| head: position=[0, -1.25, 0] |
| `cat.animation.json` | `animation.cat.sneak` | body, head | body: position=[0, -1, 0] \| head: position=[0, -1, 0] |
| `cat.animation.json` | `animation.cat.baby_transform` | head | **scale=uniform 1.5** |

---

## FIREWORK AND ARROW ANIMATIONS (Player Scaling)

These animations scale the player model.

### Firework Rocket
| File | Animation | Bones | Transform Details |
|------|-----------|-------|-------------------|
| `fireworks_rocket.animation.json` | `animation.fireworks_rocket.move` | body | rotation=[variable.shake_power - query.target_x_rotation, -query.target_y_rotation, 0] \| **scale=[0.6, 0.6, 0.8]** |

### Arrow
| File | Animation | Bones | Transform Details |
|------|-----------|-------|-------------------|
| `arrow.animation.json` | `animation.arrow.move` | body | rotation=[variable.shake_power - query.target_x_rotation, -query.target_y_rotation, 0] \| **scale=[0.7, 0.7, 0.9]** |

---

## ELYTRA ANIMATIONS (Body Scale)

| File | Animation | Bones | Transform Details |
|------|-----------|-------|-------------------|
| `elytra.animation.json` | `animation.elytra.default` | body | **scale=[1.0, 1.0, 1.0]** |
| `elytra.animation.json` | `animation.elytra.gliding` | body | **scale=[1.0, 1.0, 1.0]** |
| `elytra.animation.json` | `animation.elytra.sleeping` | body | **scale=[1.0, 1.0, 1.0]** |
| `elytra.animation.json` | `animation.elytra.sneaking` | body | **scale=[1.0, 1.0, 1.0]** |
| `elytra.animation.json` | `animation.elytra.swimming` | body | **scale=[1.0, 1.0, 1.0]** |

---

## COMPLETE MOB ANIMATIONS BY FILE

### agent.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.agent.move` | body, leftArm, leftLeg, rightArm, rightLeg | body: position=[0, bounce, 0] \| leftArm: rotation with arm swing \| leftLeg: rotation with leg swing \| rightArm: rotation with arm swing \| rightLeg: rotation with leg swing |
| `animation.agent.shrug` | head, leftArm, rightArm | head: position + rotation keyframes \| leftArm: position + rotation keyframes \| rightArm: position + rotation keyframes |
| `animation.agent.swing_arms` | rightArm | rightArm: rotation with swing animation |

### allay.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.allay.dance` | body, head | body: rotation keyframes \| head: rotation keyframes |
| `animation.allay.fly` | body, head | body: position + rotation keyframes \| head: position + rotation keyframes |
| `animation.allay.hold_item` | rightItem | rightItem: position, rotation, **scale=0.7** |
| `animation.allay.hold_item_fly` | rightItem | rightItem: position, rotation, **scale=0.7** |
| `animation.allay.idle` | body, head | body: position + rotation keyframes \| head: position keyframes |

### armor.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.armor.boots.offset` | leftLeg, rightLeg | leftLeg: position offset \| rightLeg: position offset |
| `animation.armor.chestplate.offset` | body, leftArm, rightArm | body: position offset \| leftArm: position offset \| rightArm: position offset |
| `animation.armor.helmet.offset` | head | head: position offset |
| `animation.armor.leggings.offset` | body, leftLeg, rightLeg | body: position offset \| leftLeg: position offset \| rightLeg: position offset |

### armor_stand.animation.json
All armor stand poses affect: body, head, leftarm, leftleg, rightarm, rightitem, rightleg

| Animation | Purpose |
|-----------|---------|
| `animation.armor_stand.athena_pose` | Athena pose |
| `animation.armor_stand.brandish_pose` | Brandish pose |
| `animation.armor_stand.cancan_a_pose` | Can-can pose A |
| `animation.armor_stand.cancan_b_pose` | Can-can pose B |
| `animation.armor_stand.default_pose` | Default pose |
| `animation.armor_stand.entertain_pose` | Entertain pose |
| `animation.armor_stand.hero_pose` | Hero pose |
| `animation.armor_stand.honor_pose` | Honor pose |
| `animation.armor_stand.no_pose` | No pose |
| `animation.armor_stand.riposte_pose` | Riposte pose |
| `animation.armor_stand.salute_pose` | Salute pose |
| `animation.armor_stand.solemn_pose` | Solemn pose |
| `animation.armor_stand.zombie_pose` | Zombie pose |
| `animation.armor_stand.holding_heavy_core` | Heavy core offset (rightItem only) |

### axolotl.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.axolotl.idle_floor` | body, head | body: rotation keyframes \| head: rotation keyframes |
| `animation.axolotl.idle_floor_underwater` | body | body: position + rotation keyframes |
| `animation.axolotl.idle_underwater` | body, head | body: position + rotation keyframes \| head: rotation keyframes |
| `animation.axolotl.play_dead` | body, head | body: rotation=[0, 0, 45] \| head: rotation=[0, 0, 45] |
| `animation.axolotl.swim` | body, head | body: position + rotation keyframes \| head: rotation keyframes |
| `animation.axolotl.swim_angle` | body | body: rotation=[pitch, 0, 0] |
| `animation.axolotl.walk_floor` | body, head | body: rotation keyframes \| head: rotation keyframes |
| `animation.axolotl.walk_floor_underwater` | body, head | body: position + rotation keyframes \| head: rotation keyframes |

### bat.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.bat.flying` | Head, body | Head: position + rotation keyframes \| body: position + rotation keyframes |
| `animation.bat.resting` | Head, body | Head: position=[0, 0.3, 0] \| rotation=[target_x, 180-target_y, 180] \| body: position=[0, 0.3, 0] \| rotation=[180, 0, 0] |

### bow.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.bow.wield` | rightItem | rightItem: position + rotation (first/third person variants) |
| `animation.bow.wield_first_person_pull` | rightItem | rightItem: position with shake + rotation |

### breeze.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.breeze.idle` | head | head: position keyframes |
| `animation.breeze.jump` | body, head | body: position keyframes \| head: rotation keyframes |
| `animation.breeze.shoot` | body, head | body: position + rotation keyframes \| head: position + rotation keyframes |
| `animation.breeze.slide` | body | body: position keyframes |

### camel.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.camel.dash` | body, head | body: rotation keyframes \| head: rotation keyframes |
| `animation.camel.idle` | head | head: rotation=[xHeadRot, yHeadRot, 0] |
| `animation.camel.sit` | body | body: position=[0, -19.9, 0] |
| `animation.camel.sit_down` | body, head | body: position + rotation keyframes \| head: rotation keyframes |
| `animation.camel.stand_up` | body, head | body: position + rotation keyframes \| head: rotation keyframes |
| `animation.camel.walk` | head, root | head: rotation keyframes \| root: rotation keyframes |

### cat.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.cat.baby_transform` | head | **scale=uniform 1.5** |
| `animation.cat.lie_down` | body, head | body: position + rotation with lie down amount \| head: position + rotation |
| `animation.cat.sit` | body, head | body: position=[0, -1, 0] \| **rotation=[-45, 0, 0]** \| head: position=[0, -1.25, 0] |
| `animation.cat.sneak` | body, head | body: position=[0, -1, 0] \| head: position=[0, -1, 0] |

### chicken.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.chicken.baby_transform` | head | **scale=uniform 2.0** |
| `animation.chicken.general` | body | body: rotation=[-this, 0, 0] |
| `animation.chicken.general.v1.0` | body | body: rotation=[90-this, 0, 0] |

### cod.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.cod.flop` | body, head | body: rotation with flop animation \| head: rotation with flop |
| `animation.cod.swim` | body, head | body: rotation with swim animation \| head: rotation with swim |

### copper_golem.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.copper_golem.chest_interaction.put_item` | body, head, rightItem | body: position + rotation keyframes \| head: position + rotation keyframes \| rightItem: position, rotation, **scale=0.6** |
| `animation.copper_golem.chest_interaction.put_item_fail` | body, head, rightItem | body: position + rotation keyframes \| head: position + rotation keyframes \| rightItem: position, rotation, **scale=0.6** |
| `animation.copper_golem.chest_interaction.take_item` | body, head, rightItem | body: position + rotation keyframes \| head: position + rotation keyframes \| rightItem: position, rotation, **scale=0.6** |
| `animation.copper_golem.chest_interaction.take_item_fail` | body, head, rightItem | body: position + rotation keyframes \| head: position + rotation keyframes \| rightItem: position, rotation, **scale=0.6** |
| `animation.copper_golem.spin` | body, head | body: rotation keyframes \| head: rotation keyframes |
| `animation.copper_golem.spin.oxidized` | body, head | body: rotation keyframes \| head: rotation keyframes |
| `animation.copper_golem.spin.weathered` | body, head | body: rotation keyframes \| head: rotation keyframes |
| `animation.copper_golem.walk` | body, head | body: position + rotation keyframes \| head: rotation keyframes |
| `animation.copper_golem.walk_holding_item` | body, head | body: position + rotation keyframes \| head: rotation keyframes |
| `animation.copper_golem.hold_item` | rightItem | rightItem: position, rotation, **scale=0.6** |

### cow.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.cow.baby_transform` | head | position=[0, 4, 4] \| **scale=uniform 2.0** |
| `animation.cow.setup` | body | body: rotation=[-this, 0, 0] |
| `animation.cow.setup.v1.0` | body | body: rotation=[90-this, 0, 0] |

### creaking.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.creaking.attack` | head, leftArm, leftLeg, rightArm, rightLeg | Multiple rotation keyframes for attack animation |
| `animation.creaking.look_at_target` | head | head: rotation with look-at |
| `animation.creaking.sway` | leftArm, rightArm | Arm sway animation |
| `animation.creaking.twitch` | head, leftArm, rightArm | Twitch animation |
| `animation.creaking.walk` | head, leftArm, leftLeg, rightArm, rightLeg | Walk animation |

### creeper.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.creeper.swelling` | body, head | body: scale animation \| head: scale animation |

### dolphin.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.dolphin.move` | body | body: position + rotation keyframes |

### drowned.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.drowned.attack.rotations` | body, leftarm, rightarm | Attack rotation animations |

### elytra.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.elytra.default` | body | **scale=[1.0, 1.0, 1.0]** |
| `animation.elytra.gliding` | body | **scale=[1.0, 1.0, 1.0]** |
| `animation.elytra.sleeping` | body | **scale=[1.0, 1.0, 1.0]** |
| `animation.elytra.sneaking` | body | **scale=[1.0, 1.0, 1.0]** |
| `animation.elytra.swimming` | body | **scale=[1.0, 1.0, 1.0]** |

### ender_dragon.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.ender_dragon.neck_head_movement` | head | Complex neck/head rotation |
| `animation.ender_dragon.setup` | root | Root setup transformation |

### enderman.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.enderman.arms_legs` | leftarm, leftleg, rightarm, rightleg | Arm and leg animations |
| `animation.enderman.base_pose` | body, head, leftarm, leftleg, rightarm, rightitem, rightleg, hat | Base pose with hat layer |
| `animation.enderman.carrying` | leftarm, rightarm | Carrying animation |
| `animation.enderman.scary_face` | head, hat | Scary face animation |

### evoker.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.evoker.casting` | leftarm, rightarm | Casting spell animation |
| `animation.evoker.casting.v1.0` | leftarm, rightarm | Casting spell animation v1 |
| `animation.evoker.general` | leftarm, rightarm | General evoker animation |
| `animation.evoker.move` | leftLeg, rightLeg | Walking animation |

### fox.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.fox.baby_transform` | head | **scale=uniform 1.5** |
| `animation.fox.crouch` | body, head | Crouch animation |
| `animation.fox.pounce` | body, head | Pounce animation |
| `animation.fox.setup` | body | Setup animation |
| `animation.fox.sit` | body, head | Sit animation |
| `animation.fox.sleep` | body, head | Sleep animation |
| `animation.fox.stuck` | body | Stuck animation |
| `animation.fox.wiggle` | body, head | Wiggle animation |

### fireworks_rocket.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.fireworks_rocket.move` | body | rotation=[shake_power - target_x, -target_y, 0] \| **scale=[0.6, 0.6, 0.8]** |

### frog.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.frog.idle.water` | body | Water idle animation |
| `animation.frog.jump` | body | Jump animation |
| `animation.frog.swim` | body | Swim animation |
| `animation.frog.tongue` | head | Tongue animation |
| `animation.frog.walk` | body | Walk animation |

### goat.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.goat.attack` | head | Attack animation |
| `animation.goat.baby_scaling` | head | **scale=uniform 1.0-1.5** |
| `animation.goat.look_at_target` | head | Look-at animation |
| `animation.goat.ram_attack` | head | Ram attack animation |

### happy_ghast.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.happy_ghast.scale` | body | **scale animation** |

### hoglin.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.hoglin.attack` | head | Attack animation |
| `animation.hoglin.baby_scaling` | head | **scale=uniform 1.0-1.5** |
| `animation.hoglin.look_at_target` | head | Look-at animation |

### horse_v1.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.horse.baby_transform` | body, head | body: position + scale \| head: **scale=uniform 2.0** |
| `animation.horse.eat` | head | Eat animation |
| `animation.horse.look_at_player` | head | Look-at animation |
| `animation.horse.setup` | head | Setup animation |
| `animation.horse.stand` | body, head | Stand animation |
| `animation.horse.walk` | head | Walk animation |

### horse_v2.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.horse.v2.baby_transform` | body, head | body: position + scale \| head: **scale=uniform 2.0** |
| `animation.horse.v2.setup` | body, head | Setup animation |
| `animation.horse.v2.stand` | body, head | Stand animation |

### horse_v3.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.horse.v3.baby_transform` | body, head | body: position + scale \| head: **scale=uniform 2.0** |
| `animation.horse.v3.rear` | body, head | Rear animation |

### iron_golem.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.iron_golem.walk` | body, head | Walk animation |
| `animation.iron_golem.walk_to_target` | body, head | Walk to target animation |

### llama.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.llama.baby_transform` | body, head | body: position + scale \| head: **scale=uniform 1.5** |
| `animation.llama.baby_transform.v1.0` | body, head | body: position + scale \| head: **scale=uniform 1.5** |
| `animation.llama.setup` | body | Setup animation |
| `animation.llama.setup.v1.0` | body | Setup animation v1 |

### llama_spit.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.llama_spit.setup` | body | body: position=[0, -15, 0] \| rotation with target tracking |

### look_at_target.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.common.look_at_target` | head | head: rotation=[target_x - this, target_y - this, 0] |

### mooshroom.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.mooshroom.baby_transform` | head | position=[0, 4, 4] \| **scale=uniform 2.0** |
| `animation.mooshroom.setup` | body | body: rotation=[-this, 0, 0] |
| `animation.mooshroom.setup.v1.0` | body | body: rotation=[90-this, 0, 0] |

### nautilus.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.nautilus.breathe` | body | body: scale keyframes |
| `animation.nautilus.look_at_target` | body, head | body: rotation \| head: rotation |
| `animation.nautilus.swim` | head | head: position keyframes |

### npc.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.npc.baby_transform` | head | **scale=uniform 1.5** |
| `animation.npc.get_in_bed` | body | body: position=[0, 1, -15] \| rotation=[-90, 0, 0] |

### ocelot.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.ocelot.baby_transform` | head | **scale=uniform 1.5** |
| `animation.ocelot.sit` | body, head | body: rotation=[-45, 0, 0] \| head: position=[0, -2, 0] |
| `animation.ocelot.sneak` | body, head | body: position=[0, -1, 0] \| head: position=[0, -1, 0] |

### panda.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.panda.baby_transform` | body, head | body: position + **scale=[1.15, 1.15, 1.0]** \| head: position + **scale=uniform 1.8** |
| `animation.panda.lying` | body, head | Lying animation with roll |
| `animation.panda.rolling` | body, head | Rolling animation |
| `animation.panda.sitting` | body, head | Sitting animation |
| `animation.panda.sneezing` | head | Sneezing animation |
| `animation.panda.unhappy` | head | Unhappy animation |

### parrot.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.parrot.base` | body, head | body: position + rotation \| head: position + rotation |
| `animation.parrot.dance` | body, head | body: position \| head: rotation |
| `animation.parrot.moving` | body | body: position with wing flap |
| `animation.parrot.sitting` | body | body: position=[0, -1.9, 0] |

### phantom.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.phantom.base_pose` | body | body: position=[0, -20, 0] \| rotation=[-target_x, 0, 0] |

### pig.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.pig.baby_transform` | head | position=[0, 4, 4] \| **scale=uniform 2.0** |
| `animation.pig.setup` | body | body: rotation=[-this, 0, 0] |
| `animation.pig.setup.v1.0` | body | body: rotation=[90-this, 0, 0] |

### piglin.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.piglin.admire` | head, leftarm | head: rotation=[30, 0, 0] \| leftarm: rotation=[320, 25, 0] |
| `animation.piglin.celebrate_hunt_special` | body, head, leftarm, rightarm | Celebrate animation |
| `animation.piglin.crossbow.charge` | leftarm, rightarm | Crossbow charge animation |
| `animation.piglin.crossbow.hold` | leftarm, rightarm | Crossbow hold animation |
| `animation.piglin.hand.attack` | leftarm, rightarm | Hand attack animation |
| `animation.piglin.move` | leftarm, leftleg, rightarm, rightleg | Walk animation |
| `animation.piglin.sword.attack` | leftarm, rightarm | Sword attack animation |

### pillager.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.pillager.crossbow.charge` | leftarm, rightarm | Crossbow charge animation |
| `animation.pillager.crossbow.hold` | leftarm, rightarm | Crossbow hold animation |

### polar_bear.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.polarbear.baby_transform` | head | position=[0, -1, 3] \| **scale=uniform 1.25** |
| `animation.polarbear.move` | body | body: position + rotation with standing scale |

### pufferfish.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.pufferfish.flop` | body | body: rotation with flop animation |

### rabbit.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.rabbit.baby_transform` | head | position=[0, -1, 1] \| **scale=uniform 1.5** |

### sheep.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.sheep.baby_transform` | head | position=[0, 4, 4] \| **scale=uniform 2.0** |
| `animation.sheep.grazing` | head | head: position + rotation keyframes |
| `animation.sheep.setup` | body, head | body: rotation \| head: position |

### shulker.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.shulker.move` | head | head: position with shulker facing |

### shulker_bullet.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.shulker_bullet.move` | body | body: rotation with life time |

### skeleton.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.skeleton.attack` | leftarm, rightarm | Attack animation |

### sniffer.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.sniffer.baby_transform` | head | position=[0, 1, 1] \| **scale=uniform 1.2** |
| `animation.sniffer.dig` | body, head | Dig animation with keyframes |
| `animation.sniffer.feeling_happy` | head | Happy animation |
| `animation.sniffer.longsniff` | head | Long sniff animation |
| `animation.sniffer.search` | body, head | Search animation |
| `animation.sniffer.stand_up` | body, head | Stand up animation |
| `animation.sniffer.walk` | body, head | Walk animation |

### spider.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.spider.look_at_target` | head | head: rotation with target tracking |

### squid.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.squid.move` | body | body: position=[0, 7.2/7.5, 1.8] |
| `animation.squid.rotate` | body | body: rotation with swim rotation |

### strider.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.strider.look_at_target.default` | body | body: rotation with target tracking |
| `animation.strider.walk` | body | body: position + rotation with walk |

### tripod_camera.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.tripod_camera.neutral` | body | body: position=[0, -this, 0] |

### tropicalfish.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.tropicalfish.flop` | body | body: rotation with flop animation |

### turtle.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.turtle.general` | body | body: position + rotation |

### vex.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.vex.charge` | leftarm, rightarm | Charge animation |
| `animation.vex.idle` | leftItem, leftarm, rightItem, rightarm | Idle animation with **scale=0.7** on items |

### villager.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.villager.baby_transform` | head | **scale=uniform 1.5** |
| `animation.villager.get_in_bed` | body | body: position=[0, 1, -15] \| rotation=[-90, 0, 0] |

### vindicator.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.vindicator.attack` | leftarm, rightarm | Attack animation |
| `animation.vindicator.base` | leftItem, leftarm, rightItem, rightarm | Base animation with **scale expression** on items |
| `animation.vindicator.hand_attack` | leftarm, rightarm | Hand attack animation |
| `animation.vindicator.riding.arms` | leftarm | Riding animation |

### warden.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.warden.attack` | body, head | Attack animation |
| `animation.warden.bob` | body, head | Bob animation |
| `animation.warden.dig` | body, head | Dig animation |
| `animation.warden.emerge` | body, head | Emerge animation |
| `animation.warden.look_at_target.default` | head | Look-at animation |
| `animation.warden.move` | body, head | Move animation |
| `animation.warden.roar` | body, head | Roar animation |
| `animation.warden.sniff` | body, head | Sniff animation |
| `animation.warden.sonic_boom` | body, head | Sonic boom animation |

### wither_skeleton.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.wither_skeleton.attack` | leftarm, rightarm | Attack animation |

### wither_skull.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.wither_skull.move` | head | head: rotation=[0, -target_y, 0] |

### zombie.animation.json
| Animation | Bones | Transform Details |
|-----------|-------|-------------------|
| `animation.zombie.attack_bare_hand` | leftarm, rightarm | Attack animation |
| `animation.zombie.swimming` | body, leftarm, leftleg, rightarm, rightleg | Swimming animation |

---

## Bones NOT Animated by Any Vanilla Animation

The following player bones have NO dedicated vanilla animations:
- **`hat`** — Only used by enderman (base_pose, scary_face)
- **`leftSleeve`** — No animation (follows leftArm automatically)
- **`rightSleeve`** — No animation (follows rightArm automatically)
- **`jacket`** — No animation (follows body automatically)
- **`leftPants`** — No animation (follows leftLeg automatically)
- **`rightPants`** — No animation (follows rightLeg automatically)

---

## Key Findings

### 1. Baby Mob Animations Affect Head
All baby mob animations use `scale` on the `head` bone, typically ranging from 1.2x to 2.0x. If applied to a player, these will scale the player's head.

### 2. Cat Animations Affect Torso
The `cat.sit` animation applies a **-45 degree X rotation** to the body, while `cat.lie_down` applies a **90 degree Z rotation** when fully lying down.

### 3. Firework and Arrow Scale Player
- `fireworks_rocket.move`: Scales body to **[0.6, 0.6, 0.8]**
- `arrow.move`: Scales body to **[0.7, 0.7, 0.9]**

### 4. Case Sensitivity Matters
Many mob animations use lowercase bone names (`leftarm`, `rightarm`, etc.) which do NOT match player bone names (`leftArm`, `rightArm`, etc.). Only animations using camelCase player bone names will affect the player model.

### 5. Scale Animations
The following animations apply scale transforms that would affect the player:
- Baby transforms: 1.2x to 2.0x head scale
- Firework: 0.6x body scale
- Arrow: 0.7x body scale
- Vex items: 0.7x scale
- Copper golem items: 0.6x scale
- Happy ghast: body scale animation

---
