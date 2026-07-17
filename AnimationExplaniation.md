# Minecraft Bedrock Player Animation Reference
## Vanilla Resource Pack v26.0.0 Analysis

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

### Accessible Bones

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

## Animation Files Overview

| File | Animations | Purpose |
|------|-----------|---------|
| `player.animation.json` | 42 | Primary player animations |
| `humanoid.animation.json` | 28 | Shared humanoid animations (used by NPCs, zombies, etc.) |
| `player_firstperson.animation.json` | 18 | First-person camera animations |
| `look_at_target.animation.json` | 1 | Head tracking |
| `elytra.animation.json` | 5 | Elytra/gliding scale |
| `armor_stand.animation.json` | 15 | Armor stand poses |
| `bow.animation.json` | 2 | Bow item animations |
| `crossbow.animation.json` | 2 | Crossbow item animations |
| `shield.animation.json` | 2 | Shield item animations |
| `spear.animation.json` | 2 | Spear item animations |
| `spyglass.animation.json` | 2 | Spyglass item animations |

---

## Detailed Animation Reference

### player.animation.json

---

#### animation.player.attack.positions
- **Loop:** Yes
- **Bones Affected:** `head`
- **Properties:** rotation (static: [0,0,0])
- **Purpose:** Resets head rotation during attack

---

#### animation.player.attack.rotations
- **Loop:** Yes
- **Bones Affected:** `body`, `leftArm`, `rightArm`
- **Properties:**
  - `body` → rotation (Molang: `variable.attack_body_rot_y`)
  - `leftArm` → rotation (Molang: `variable.attack_time` based sine wave)
  - `rightArm` → rotation (Molang: `variable.attack_time` based, 30° swing)
- **Purpose:** Main attack animation — swings arms during melee combat

---

#### animation.player.base_pose.upside_down
- **Loop:** Yes
- **Bones Affected:** `waist`
- **Properties:**
  - `waist` → position [0, 8, 0], rotation [0, 0, 180°]
- **Purpose:** Flips player upside down (used by commands)

---

#### animation.player.bob
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - `leftArm` → rotation (Molang: cosine wave using `query.life_time`)
  - `rightArm` → rotation (Molang: opposite cosine wave)
- **Purpose:** Idle arm bobbing while walking

---

#### animation.player.bob.stationary
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:** Same as bob
- **Purpose:** Idle arm bobbing while standing still

---

#### animation.player.bow_equipped
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`, `rightItem`
- **Properties:**
  - `leftArm` → rotation (Molang: target rotation + sneaking offset)
  - `rightArm` → rotation (Molang: target rotation)
  - `rightItem` → rotation [0, -10, 0] (static)
- **Purpose:** Bow aiming pose — arms follow look direction

---

#### animation.player.cape
- **Loop:** Yes
- **Bones Affected:** `cape`
- **Properties:**
  - `cape` → position (Molang: armor offset), rotation (Molang: `query.cape_flap_amount`)
- **Purpose:** Cape physics/flap animation

---

#### animation.player.crossbow_equipped
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - `leftArm` → position [0, 0, 0.5], rotation (Molang)
  - `rightArm` → rotation (Molang)
- **Purpose:** Crossbow aiming pose

---

#### animation.player.crossbow_hold
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - `leftArm` → rotation (Molang: swimming check, target rotation)
  - `rightArm` → rotation (Molang: swimming check, target rotation)
- **Purpose:** Holding crossbow ready

---

#### animation.player.melee_spear_attack
- **Loop:** Yes
- **Bones Affected:** `body`, `rightArm`, `rightItem`
- **Properties:**
  - `body` → rotation (Molang: attack body rotation)
  - `rightArm` → rotation (Molang: spear attack motion)
  - `rightItem` → position [0, -1.5, -1.5], rotation (Molang)
- **Purpose:** Spear thrust attack animation

---

#### animation.player.glide
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`, `leftLeg`, `rightLeg`
- **Properties:**
  - Arms → rotation (Molang: spread out)
  - Legs → rotation (Molang: slight angle)
- **Purpose:** Elytra gliding pose — limbs spread

---

#### animation.player.holding
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation (Molang: holding position)
- **Purpose:** Default holding items pose

---

#### animation.player.holding_heavy_core
- **Loop:** Yes
- **Bones Affected:** `rightItem`
- **Properties:**
  - `rightItem` → position [-1, 0, -2]
- **Purpose:** Offset for heavy core item

---

#### animation.player.holding.zombie
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation [0, 0, 0] (static)
- **Purpose:** Zombie holding pose (arms forward)

---

#### animation.player.look_at_target.inverted
- **Loop:** Yes
- **Bones Affected:** `head`
- **Properties:**
  - `head` → rotation (Molang: inverted look-at)
- **Purpose:** Head tracking when upside down

---

#### animation.player.look_at_target.ui
- **Loop:** Yes
- **Bones Affected:** `head`
- **Properties:**
  - `head` → rotation (Molang: UI look direction)
- **Purpose:** Head tracking in UI screens

---

#### animation.player.move.arms
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation (Molang: walk cycle)
- **Purpose:** Arm swing while walking

---

#### animation.player.move.arms.single
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation (Molang: one-armed walk)
- **Purpose:** Single-arm swing variant

---

#### animation.player.move.arms.stationary
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation [0, 0, 0] (static)
- **Purpose:** No arm movement (standing still)

---

#### animation.player.move.arms.statue_of_liberty
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - `leftArm` → rotation (Molang: raised up)
  - `rightArm` → rotation (Molang: normal)
- **Purpose:** One arm raised pose

---

#### animation.player.move.arms.zombie
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation [-90, 0, 0] (static, arms forward)
- **Purpose:** Zombie arms forward pose

---

#### animation.player.move.legs
- **Loop:** Yes
- **Bones Affected:** `leftLeg`, `rightLeg`
- **Properties:**
  - `leftLeg` → rotation (Molang: walk cycle, slight angle)
  - `rightLeg` → rotation (Molang: walk cycle, opposite phase)
- **Purpose:** Leg animation while walking

---

#### animation.player.move.legs.inverted
- **Loop:** Yes
- **Bones Affected:** `leftLeg`, `rightLeg`
- **Properties:**
  - Both legs → position [0, 8, 0], rotation (Molang: inverted angles)
- **Purpose:** Inverted walking (upside down)

---

#### animation.player.move.legs.single
- **Loop:** Yes
- **Bones Affected:** `leftLeg`, `rightLeg`
- **Properties:**
  - Both legs → rotation (Molang: walk cycle)
- **Purpose:** Single-leg walk variant

---

#### animation.player.move.legs.stationary
- **Loop:** Yes
- **Bones Affected:** `leftLeg`, `rightLeg`
- **Properties:**
  - `leftLeg` → rotation [0, -0.1, -0.1] (static)
  - `rightLeg` → rotation [0, 0.1, 0.1] (static)
- **Purpose:** No leg movement (standing still)

---

#### animation.player.riding.root
- **Loop:** Yes
- **Bones Affected:** `root`
- **Properties:**
  - `root` → position (Molang: riding offset)
- **Purpose:** Base position while riding

---

#### animation.player.riding.arms
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation [-36, 0, 0] (static)
- **Purpose:** Arms resting while riding

---

#### animation.player.riding.arms.zombie
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation [45, 0, 0] (static)
- **Purpose:** Zombie arms while riding

---

#### animation.player.riding.legs
- **Loop:** Yes
- **Bones Affected:** `leftLeg`, `rightLeg`
- **Properties:**
  - Both legs → rotation (Molang: sitting pose)
- **Purpose:** Legs while riding

---

#### animation.player.shield_block_main_hand
- **Loop:** Yes
- **Bones Affected:** `rightArm`, `rightItem`
- **Properties:**
  - `rightArm` → rotation [-20, -30, -25] (static)
  - `rightItem` → position [-1, -3, 0], rotation [0, -60, -45] (static)
- **Purpose:** Shield blocking with main hand

---

#### animation.player.shield_block_off_hand
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `leftItem`
- **Properties:**
  - `leftArm` → rotation [-20, 20, 20] (static)
  - `leftItem` → position (Molang), rotation (Molang)
- **Purpose:** Shield blocking with off hand

---

#### animation.player.sleeping
- **Loop:** Yes
- **Bones Affected:** `head`, `root`
- **Properties:**
  - `head` → rotation (Molang)
  - `root` → position (Molang), rotation [-90, 0, 0] (lying down)
- **Purpose:** Sleeping pose — player lies horizontal

---

#### animation.player.sneaking
- **Loop:** Yes
- **Bones Affected:** `body`, `head`, `leftArm`, `rightArm`, `leftLeg`, `rightLeg`, `root`
- **Properties:**
  - `body` → position [0, -2, 0] (static, lowered)
  - `head` → position [0, -1, 0] (static, lowered)
  - `leftArm` → rotation [-5.7, 0, 0] (static, arms down)
  - `rightArm` → rotation [-5.7, 0, 0] (static, arms down)
  - `leftLeg` → rotation [-28, -0.1, -0.1] (static, bent)
  - `rightLeg` → rotation [-28, 0.1, 0.1] (static, bent)
  - `root` → position [0, 1.25, 9], rotation (Molang)
- **Purpose:** Sneaking/crouching pose — entire body lowered

---

#### animation.player.sneaking.inverted
- **Loop:** Yes
- **Bones Affected:** `body`, `head`, `leftArm`, `rightArm`, `leftLeg`, `rightLeg`, `root`
- **Properties:** Same as sneaking but inverted angles
- **Purpose:** Sneaking while upside down

---

#### animation.player.swim
- **Loop:** Yes | **Length:** 1.3s
- **Bones Affected:** `leftArm`, `rightArm`, `root`
- **Properties:**
  - `leftArm` → rotation (4 keyframes — swim stroke)
  - `rightArm` → rotation (4 keyframes — swim stroke)
  - `root` → position (Molang), rotation (Molang: horizontal)
- **Purpose:** Swimming arm stroke animation

---

#### animation.player.swim.no_right_arm
- **Loop:** Yes | **Length:** 1.3s
- **Bones Affected:** `leftArm`, `root`
- **Properties:** Same as swim but only left arm
- **Purpose:** Swimming with only left arm (right arm occupied)

---

#### animation.player.swim.legs
- **Loop:** Yes
- **Bones Affected:** `leftLeg`, `rightLeg`
- **Properties:**
  - Both legs → rotation (Molang: kick cycle)
- **Purpose:** Swimming leg kick animation

---

#### animation.player.swim.legs.single
- **Loop:** Yes
- **Bones Affected:** `leftLeg`, `rightLeg`
- **Properties:** Same as swim.legs
- **Purpose:** Single-leg kick variant

---

#### animation.player.swim.legs.stationary
- **Loop:** Yes
- **Bones Affected:** `leftLeg`, `rightLeg`
- **Properties:**
  - `leftLeg` → rotation [0, -0.1, -0.1] (static)
  - `rightLeg` → rotation [0, 0.1, 0.1] (static)
- **Purpose:** No leg kick (standing still in water)

---

#### animation.player.crawl
- **Loop:** Yes | **Length:** 1.3s
- **Bones Affected:** `leftArm`, `rightArm`, `root`
- **Properties:**
  - `leftArm` → rotation (4 keyframes — crawl stroke)
  - `rightArm` → rotation (4 keyframes — crawl stroke)
  - `root` → position (Molang), rotation (Molang: horizontal)
- **Purpose:** Crawling arm animation

---

#### animation.player.crawl.no_right_arm
- **Loop:** Yes | **Length:** 1.3s
- **Bones Affected:** `leftArm`, `root`
- **Properties:** Same as crawl but only left arm
- **Purpose:** Crawling with only left arm

---

#### animation.player.crawl.legs
- **Loop:** Yes
- **Bones Affected:** `leftLeg`, `rightLeg`
- **Properties:**
  - Both legs → rotation (Molang: crawl leg movement)
- **Purpose:** Crawling leg animation

---

### humanoid.animation.json

---

#### animation.humanoid.attack.rotations
- **Loop:** Yes
- **Bones Affected:** `body`, `leftArm`, `rightArm`
- **Properties:**
  - `body` → rotation (Molang: body twist)
  - `leftArm` → rotation (Molang: arm swing)
  - `rightArm` → rotation (Molang: attack swing)
- **Purpose:** Shared attack animation for humanoids

---

#### animation.humanoid.base_pose
- **Loop:** Yes
- **Bones Affected:** `waist`
- **Properties:**
  - `waist` → rotation [0, 0, 0] (static)
- **Purpose:** Default waist rotation (neutral)

---

#### animation.humanoid.big_head
- **Loop:** Yes
- **Bones Affected:** `head`
- **Properties:**
  - `head` → scale (dynamic)
- **Purpose:** Enlarges head (for special effects)

---

#### animation.humanoid.bob
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation (Molang: cosine wave)
- **Purpose:** Shared idle arm bob

---

#### animation.humanoid.bow_and_arrow
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation (Molang: bow pose)
- **Purpose:** Shared bow aiming pose

---

#### animation.humanoid.brandish_spear
- **Loop:** Yes
- **Bones Affected:** `rightArm`
- **Properties:**
  - `rightArm` → rotation (Molang: spear raise)
- **Purpose:** Spear brandish/throw pose

---

#### animation.humanoid.holding_spyglass
- **Loop:** Yes
- **Bones Affected:** `rightArm`
- **Properties:**
  - `rightArm` → rotation (Molang: spyglass hold + 5°)
- **Purpose:** Holding spyglass up to eye

---

#### animation.humanoid.tooting_goat_horn
- **Loop:** Yes
- **Bones Affected:** `rightArm`, `rightItem`
- **Properties:**
  - `rightArm` → rotation (Molang + 5°)
  - `rightItem` → position [4, 0, 1], rotation [15, 0, 100] (static)
- **Purpose:** Blowing goat horn

---

#### animation.humanoid.holding_brush
- **Loop:** Yes
- **Bones Affected:** `rightItem`
- **Properties:**
  - `rightItem` → position (1 keyframe), rotation (1 keyframe)
- **Purpose:** Brush item default position

---

#### animation.humanoid.brushing
- **Loop:** Yes
- **Bones Affected:** `rightArm`, `rightItem`
- **Properties:**
  - `rightArm` → rotation (Molang + 5°)
  - `rightItem` → position (6 keyframes), rotation (6 keyframes)
- **Purpose:** Brushing animation (suspicious sand/gravel)

---

#### animation.humanoid.celebrating
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - `leftArm` → rotation (Molang + [180, -135])
  - `rightArm` → rotation (Molang + [180, 153])
- **Purpose:** Victory celebration — arms raised

---

#### animation.humanoid.charging
- **Loop:** Yes
- **Bones Affected:** `rightArm`
- **Properties:**
  - `rightArm` → rotation (Molang + 5°)
- **Purpose:** Charging attack pose

---

#### animation.humanoid.damage_nearby_mobs
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`, `leftLeg`, `rightLeg`
- **Properties:**
  - All four limbs → rotation (Molang: knockback)
- **Purpose:** Iron golem smash animation

---

#### animation.humanoid.holding
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation (Molang + [0, 0])
- **Purpose:** Default item holding pose

---

#### animation.humanoid.look_at_target.default
- **Loop:** Yes
- **Bones Affected:** `head`
- **Properties:**
  - `head` → rotation (Molang: look-at + 0°)
- **Purpose:** Default head tracking

---

#### animation.humanoid.look_at_target.gliding
- **Loop:** Yes
- **Bones Affected:** `head`
- **Properties:**
  - `head` → rotation (Molang: look-at + [-45, 0])
- **Purpose:** Head tracking while gliding

---

#### animation.humanoid.look_at_target.swimming
- **Loop:** Yes
- **Bones Affected:** `head`
- **Properties:**
  - `head` → rotation (Molang: look-at + 0°)
- **Purpose:** Head tracking while swimming

---

#### animation.humanoid.move
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`, `leftLeg`, `rightLeg`
- **Properties:**
  - Arms → rotation (Molang: walk cycle)
  - Legs → rotation (Molang: walk cycle, slight angle)
- **Purpose:** Full body walk animation

---

#### animation.humanoid.riding.body
- **Loop:** Yes
- **Bones Affected:** `body`
- **Properties:**
  - `body` → position (Molang: riding offset)
- **Purpose:** Body position while riding

---

#### animation.humanoid.riding.arms
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation [-36, 0, 0] (static)
- **Purpose:** Arms while riding

---

#### animation.humanoid.riding.legs
- **Loop:** Yes
- **Bones Affected:** `leftLeg`, `rightLeg`
- **Properties:**
  - Both legs → rotation (Molang: sitting)
- **Purpose:** Legs while riding

---

#### animation.humanoid.sneaking
- **Loop:** Yes
- **Bones Affected:** `body`, `head`, `leftArm`, `rightArm`, `leftLeg`, `rightLeg`
- **Properties:**
  - `body` → rotation (Molang)
  - `head` → position [0, 1, 0] (static, raised slightly)
  - `leftArm` → rotation [72, 0, 0] (static, arms forward-down)
  - `rightArm` → rotation [72, 0, 0] (static, arms forward-down)
  - `leftLeg` → position [0, -3.1, 3.9] (static, bent forward)
  - `rightLeg` → position [0, -2.9, 4.1] (static, bent forward)
- **Purpose:** Humanoid sneak pose (different from player)

---

#### animation.humanoid.swimming
- **Loop:** Yes | **Length:** 1.3s
- **Bones Affected:** `leftArm`, `rightArm`, `leftLeg`, `rightLeg`
- **Properties:**
  - Arms → rotation (3 keyframes — swim stroke)
  - Legs → rotation (Molang: kick)
- **Purpose:** Full body swimming animation

---

#### animation.humanoid.use_item_progress
- **Loop:** Yes
- **Bones Affected:** `rightArm`
- **Properties:**
  - `rightArm` → rotation (Molang: item use motion)
- **Purpose:** Using/eating animation

---

#### animation.humanoid.melee_spear_hold
- **Loop:** Yes
- **Bones Affected:** `rightArm`, `rightItem`
- **Properties:**
  - `rightArm` → rotation (Molang + 0°)
  - `rightItem` → position [0, -1.5, -1.5] (static)
- **Purpose:** Holding spear ready

---

#### animation.humanoid.melee_spear_use
- **Loop:** Yes
- **Bones Affected:** `rightArm`, `rightItem`
- **Properties:**
  - `rightArm` → rotation (Molang: thrust)
  - `rightItem` → position [0, -1.5, -1.5], rotation (Molang)
- **Purpose:** Spear thrust attack

---

#### animation.zombie.melee_spear_hold
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`, `rightItem`
- **Properties:**
  - Both arms → rotation (Molang + 0°)
  - `rightItem` → position [0, -1.5, -1.5] (static)
- **Purpose:** Zombie spear hold

---

#### animation.zombie.melee_spear_use
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`, `rightItem`
- **Properties:**
  - Both arms → rotation (Molang)
  - `rightItem` → position [0, -1.5, -1.5], rotation (Molang)
- **Purpose:** Zombie spear attack

---

### player_firstperson.animation.json

---

#### animation.player.first_person.attack_rotation
- **Loop:** Yes
- **Bones Affected:** `rightArm`
- **Properties:**
  - `rightArm` → position, rotation (dynamic)
- **Purpose:** First-person attack swing

---

#### animation.player.first_person.attack_rotation_item
- **Loop:** Yes
- **Bones Affected:** `rightItem`
- **Properties:**
  - `rightItem` → position, rotation (dynamic)
- **Purpose:** First-person item attack

---

#### animation.player.first_person.base_pose
- **Loop:** Yes
- **Bones Affected:** `body`, `head`
- **Properties:**
  - `body` → rotation
  - `head` → rotation
- **Purpose:** First-person base camera pose

---

#### animation.player.first_person.crossbow_equipped
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightItem`
- **Properties:**
  - `leftArm` → position, rotation, scale
  - `rightItem` → position, rotation, scale
- **Purpose:** First-person crossbow aiming

---

#### animation.player.first_person.crossbow_hold
- **Loop:** Yes
- **Bones Affected:** `rightItem`
- **Properties:**
  - `rightItem` → position
- **Purpose:** First-person crossbow hold

---

#### animation.player.first_person.melee_spear_hold
- **Loop:** Yes
- **Bones Affected:** `rightItem`
- **Properties:**
  - `rightItem` → position, rotation
- **Purpose:** First-person spear hold

---

#### animation.player.first_person.melee_spear_use
- **Loop:** Yes
- **Bones Affected:** `rightItem`
- **Properties:**
  - `rightItem` → position, rotation
- **Purpose:** First-person spear use

---

#### animation.player.first_person.melee_spear_attack
- **Loop:** Yes
- **Bones Affected:** `rightItem`
- **Properties:**
  - `rightItem` → position, rotation
- **Purpose:** First-person spear attack

---

#### animation.player.first_person.breathing_bob
- **Loop:** Yes
- **Bones Affected:** `rightItem`
- **Properties:**
  - `rightItem` → position
- **Purpose:** Idle item bob

---

#### animation.player.first_person.empty_hand
- **Loop:** Yes
- **Bones Affected:** `rightArm`, `rightItem`, `leftItem`
- **Properties:**
  - `rightArm` → position, rotation
  - `rightItem` → position
  - `leftItem` → position
- **Purpose:** Empty hand first-person pose

---

#### animation.player.first_person.map_hold
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - `leftArm` → position, rotation, scale
  - `rightArm` → position, rotation
- **Purpose:** Holding map with both hands

---

#### animation.player.first_person.map_hold_attack
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - `leftArm` → position, rotation
  - `rightArm` → position, rotation
- **Purpose:** Using map item

---

#### animation.player.first_person.map_hold_main_hand
- **Loop:** Yes
- **Bones Affected:** `rightArm`
- **Properties:**
  - `rightArm` → position, rotation, scale
- **Purpose:** Map in main hand

---

#### animation.player.first_person.map_hold_off_hand
- **Loop:** Yes
- **Bones Affected:** `leftArm`
- **Properties:**
  - `leftArm` → position, rotation, scale
- **Purpose:** Map in off hand

---

#### animation.player.first_person.swap_item
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - `leftArm` → position
  - `rightArm` → position
- **Purpose:** Item swap animation

---

#### animation.player.first_person.shield_block
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - `leftArm` → position
  - `rightArm` → position
- **Purpose:** First-person shield block

---

#### animation.player.first_person.vr_attack_rotation
- **Loop:** Yes
- **Bones Affected:** `rightArm`
- **Properties:**
  - `rightArm` → position, rotation
- **Purpose:** VR attack swing

---

#### animation.player.first_person.walk
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - `leftArm` → position
  - `rightArm` → position
- **Purpose:** First-person walk bob

---

### look_at_target.animation.json

---

#### animation.common.look_at_target
- **Loop:** Yes
- **Bones Affected:** `head`
- **Properties:**
  - `head` → rotation (dynamic)
- **Purpose:** Generic head look-at target

---

### elytra.animation.json

---

#### animation.elytra.default
- **Loop:** Yes
- **Bones Affected:** `body`
- **Properties:**
  - `body` → scale (static)
- **Purpose:** Elytra default scale

---

#### animation.elytra.gliding
- **Loop:** Yes
- **Bones Affected:** `body`
- **Properties:**
  - `body` → scale (static)
- **Purpose:** Elytra gliding scale

---

#### animation.elytra.sneaking
- **Loop:** Yes
- **Bones Affected:** `body`
- **Properties:**
  - `body` → scale (static)
- **Purpose:** Elytra sneaking scale

---

#### animation.elytra.sleeping
- **Loop:** Yes
- **Bones Affected:** `body`
- **Properties:**
  - `body` → scale (static)
- **Purpose:** Elytra sleeping scale

---

#### animation.elytra.swimming
- **Loop:** Yes
- **Bones Affected:** `body`
- **Properties:**
  - `body` → scale (static)
- **Purpose:** Elytra swimming scale

---

### armor_stand.animation.json

All armor stand poses affect: `body`, `head`, `leftArm`, `rightArm`, `leftLeg`, `rightLeg`, `rightItem`

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
| `animation.armor_stand.wiggle` | Wiggle animation (baseplate only) |
| `animation.armor_stand.holding_heavy_core` | Heavy core offset (rightItem only) |

---

### Item Animations

#### bow.animation.json
| Animation | Bones | Purpose |
|-----------|-------|---------|
| `animation.bow.wield` | `rightItem` | Bow holding pose |
| `animation.bow.wield_first_person_pull` | `rightItem` | Bow pull in first person |

#### crossbow.animation.json
| Animation | Bones | Purpose |
|-----------|-------|---------|
| `animation.crossbow.wield` | `rightItem` | Crossbow holding pose |
| `animation.crossbow.wield_first_person_pull` | `rightItem` | Crossbow pull in first person |

---

## Quick Reference: Bones by Animation Category

### Walking/Movement
- `animation.player.move.arms` → leftArm, rightArm
- `animation.player.move.legs` → leftLeg, rightLeg
- `animation.player.bob` → leftArm, rightArm
- `animation.humanoid.move` → leftArm, rightArm, leftLeg, rightLeg

### Combat
- `animation.player.attack.rotations` → body, leftArm, rightArm
- `animation.player.bow_equipped` → leftArm, rightArm, rightItem
- `animation.player.crossbow_equipped` → leftArm, rightArm
- `animation.player.melee_spear_attack` → body, rightArm, rightItem

### Sneaking
- `animation.player.sneaking` → body, head, leftArm, rightArm, leftLeg, rightLeg, root
- `animation.humanoid.sneaking` → body, head, leftArm, rightArm, leftLeg, rightLeg

### Swimming/Crawling
- `animation.player.swim` → leftArm, rightArm, root
- `animation.player.swim.legs` → leftLeg, rightLeg
- `animation.player.crawl` → leftArm, rightArm, root
- `animation.player.crawl.legs` → leftLeg, rightLeg

### Riding
- `animation.player.riding.root` → root
- `animation.player.riding.arms` → leftArm, rightArm
- `animation.player.riding.legs` → leftLeg, rightLeg

### Sleeping
- `animation.player.sleeping` → head, root

### Elytra/Gliding
- `animation.player.glide` → leftArm, rightArm, leftLeg, rightLeg
- `animation.elytra.*` → body (scale only)

### Look-At
- `animation.common.look_at_target` → head
- `animation.humanoid.look_at_target.*` → head

### Shield
- `animation.player.shield_block_main_hand` → rightArm, rightItem
- `animation.player.shield_block_off_hand` → leftArm, leftItem

### First Person
- `animation.player.first_person.*` → rightArm, leftArm, rightItem, leftItem, body, head

---

## Bones NOT Animated by Any Vanilla Animation

The following player bones have NO dedicated vanilla animations:
- **`hat`** — No animation (follows head automatically via bone hierarchy)
- **`leftSleeve`** — No animation (follows leftArm automatically)
- **`rightSleeve`** — No animation (follows rightArm automatically)
- **`jacket`** — No animation (follows body automatically)
- **`leftPants`** — No animation (follows leftLeg automatically)
- **`rightPants`** — No animation (follows rightLeg automatically)

These "overlay" bones are designed to follow their parent bone without separate animation data.

---

## Molang Variables Reference

Many animations use Molang expressions. Key variables used in player animations:

| Variable | Description |
|----------|-------------|
| `query.life_time` | Time since entity spawned |
| `query.target_x_rotation` | Look target X rotation |
| `query.target_y_rotation` | Look target Y rotation |
| `variable.attack_time` | Current attack progress (0-1) |
| `variable.attack_body_rot_y` | Body rotation during attack |
| `query.cape_flap_amount` | Cape flap intensity |
| `query.is_sneaking` | Whether player is sneaking (0 or 1) |
| `query.is_swimming` | Whether player is swimming (0 or 1) |
| `variable.item_use_normalized` | Item use progress |

---

## Complete Cross-File Scan: All Animations Affecting Player Bones

**Total: 386 animations across 68 files** affect player bone names.

Many mob animations use the same bone names as the player (body, head, leftarm, rightarm, etc.) — these are listed below for completeness.

---

### agent.animation.json (3 animations)

| Animation | Bones |
|-----------|-------|
| `animation.agent.move` | body, leftArm, leftLeg, rightArm, rightLeg |
| `animation.agent.swing_arms` | rightArm |
| `animation.agent.shrug` | head, leftArm, rightArm |

---

### allay.animation.json (5 animations)

| Animation | Bones |
|-----------|-------|
| `animation.allay.idle` | body, head |
| `animation.allay.fly` | body, head |
| `animation.allay.hold_item` | rightItem |
| `animation.allay.hold_item_fly` | rightItem |
| `animation.allay.dance` | body, head |

---

### armadillo.animation.json (7 animations)

| Animation | Bones |
|-----------|-------|
| `animation.armadillo.look_at_target` | head |
| `animation.armadillo.walk` | body |
| `animation.armadillo.roll_up` | body, head |
| `animation.armadillo.rolled_up` | body, head |
| `animation.armadillo.peek` | head |
| `animation.armadillo.unroll` | body, head |
| `animation.armadillo.unroll_fast` | body, head |

---

### armor_stand.animation.json (15 animations)

| Animation | Bones |
|-----------|-------|
| `animation.armor_stand.athena_pose` | body, head, leftArm, leftLeg, rightArm, rightItem, rightLeg |
| `animation.armor_stand.brandish_pose` | body, head, leftArm, leftLeg, rightArm, rightItem, rightLeg |
| `animation.armor_stand.cancan_a_pose` | body, head, leftArm, leftLeg, rightArm, rightItem, rightLeg |
| `animation.armor_stand.cancan_b_pose` | body, head, leftArm, leftLeg, rightArm, rightItem, rightLeg |
| `animation.armor_stand.default_pose` | body, head, leftArm, leftLeg, rightArm, rightItem, rightLeg |
| `animation.armor_stand.entertain_pose` | body, head, leftArm, leftLeg, rightArm, rightItem, rightLeg |
| `animation.armor_stand.hero_pose` | body, head, leftArm, leftLeg, rightArm, rightItem, rightLeg |
| `animation.armor_stand.honor_pose` | body, head, leftArm, leftLeg, rightArm, rightItem, rightLeg |
| `animation.armor_stand.no_pose` | body, head, leftArm, leftLeg, rightArm, rightItem, rightLeg |
| `animation.armor_stand.riposte_pose` | body, head, leftArm, leftLeg, rightArm, rightItem, rightLeg |
| `animation.armor_stand.salute_pose` | body, head, leftArm, leftLeg, rightArm, rightItem, rightLeg |
| `animation.armor_stand.solemn_pose` | body, head, leftArm, leftLeg, rightArm, rightItem, rightLeg |
| `animation.armor_stand.zombie_pose` | body, head, leftArm, leftLeg, rightArm, rightItem, rightLeg |
| `animation.armor_stand.wiggle` | baseplate (no player bones) |
| `animation.armor_stand.holding_heavy_core` | rightitem |

---

### bat.animation.json

| Animation | Bones |
|-----------|-------|
| (check source — bat uses wing bones, not player bones) | — |

---

### bow.animation.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.bow.wield` | rightItem |
| `animation.bow.wield_first_person_pull` | rightItem |

---

### crossbow.animation.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.crossbow.wield` | rightItem |
| `animation.crossbow.wield_first_person_pull` | rightItem |

---

### drowned.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.drowned.attack.rotations` | body, leftarm, rightarm |

---

### drowned.animation.v1.0.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.drowned.attack.rotations.v1.0` | body, leftarm, rightarm |
| `animation.drowned.swimming.v1.0` | leftarm, leftleg, rightarm, rightleg, root |

---

### elytra.animation.json (5 animations)

| Animation | Bones |
|-----------|-------|
| `animation.elytra.default` | body (scale) |
| `animation.elytra.gliding` | body (scale) |
| `animation.elytra.sneaking` | body (scale) |
| `animation.elytra.sleeping` | body (scale) |
| `animation.elytra.swimming` | body (scale) |

---

### ender_dragon.animation.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.ender_dragon.setup` | root |
| `animation.ender_dragon.neck_head_movement` | head |

---

### enderman.animation.json (4 animations)

| Animation | Bones |
|-----------|-------|
| `animation.enderman.arms_legs` | leftarm, leftleg, rightarm, rightleg |
| `animation.enderman.base_pose` | body, hat, head, leftarm, leftleg, rightarm, rightleg |
| `animation.enderman.carrying` | leftarm, rightarm |
| `animation.enderman.scary_face` | hat, head |

---

### enderman.animation.v1.0.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.enderman.base_pose_v1.0` | body, hat, head, leftarm, leftleg, rightarm, rightleg |
| `animation.enderman.scary_face_v1.0` | hat, head |

---

### evoker.animation.json (4 animations)

| Animation | Bones |
|-----------|-------|
| `animation.evoker.casting` | leftarm, rightarm |
| `animation.evoker.casting.v1.0` | leftarm, rightarm |
| `animation.evoker.general` | leftarm, rightarm |
| `animation.evoker.move` | leftLeg, rightLeg |

---

### fireworks_rocket.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.fireworks_rocket.move` | body |

---

### fox.animation.json (8 animations)

| Animation | Bones |
|-----------|-------|
| `animation.fox.baby_transform` | head |
| `animation.fox.crouch` | body, head |
| `animation.fox.pounce` | body, head |
| `animation.fox.setup` | body |
| `animation.fox.sit` | body, head |
| `animation.fox.sleep` | body, head |
| `animation.fox.stuck` | body |
| `animation.fox.wiggle` | body, head |

---

### frog.animation.json (5 animations)

| Animation | Bones |
|-----------|-------|
| `animation.frog.walk` | body |
| `animation.frog.jump` | body |
| `animation.frog.tongue` | head |
| `animation.frog.swim` | body |
| `animation.frog.idle.water` | body |

---

### goat.animation.json (4 animations)

| Animation | Bones |
|-----------|-------|
| `animation.goat.baby_scaling` | head |
| `animation.goat.look_at_target` | head |
| `animation.goat.attack` | head |
| `animation.goat.ram_attack` | head |

---

### happy_ghast.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.happy_ghast.scale` | body |

---

### hoglin.animation.json (3 animations)

| Animation | Bones |
|-----------|-------|
| `animation.hoglin.baby_scaling` | head |
| `animation.hoglin.look_at_target` | head |
| `animation.hoglin.attack` | head |

---

### horse_v1.animation.json (6 animations)

| Animation | Bones |
|-----------|-------|
| `animation.horse.baby_transform` | body, head |
| `animation.horse.eat` | head |
| `animation.horse.look_at_player` | head |
| `animation.horse.setup` | head |
| `animation.horse.stand` | body, head |
| `animation.horse.walk` | head |

---

### horse_v2.animation.json (3 animations)

| Animation | Bones |
|-----------|-------|
| `animation.horse.v2.baby_transform` | body, head |
| `animation.horse.v2.setup` | body, head |
| `animation.horse.v2.stand` | body |

---

### horse_v3.animation.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.horse.v3.baby_transform` | body, head |
| `animation.horse.v3.rear` | body |

---

### humanoid.animation.json (28 animations)

| Animation | Bones |
|-----------|-------|
| `animation.humanoid.attack.rotations` | body, leftarm, rightarm |
| `animation.humanoid.base_pose` | waist |
| `animation.humanoid.big_head` | head (scale) |
| `animation.humanoid.bob` | leftarm, rightarm |
| `animation.humanoid.bow_and_arrow` | leftarm, rightarm |
| `animation.humanoid.brandish_spear` | rightarm |
| `animation.humanoid.holding_spyglass` | rightarm |
| `animation.humanoid.tooting_goat_horn` | rightarm, rightitem |
| `animation.humanoid.holding_brush` | rightitem |
| `animation.humanoid.brushing` | rightarm, rightitem |
| `animation.humanoid.celebrating` | leftarm, rightarm |
| `animation.humanoid.charging` | rightarm |
| `animation.humanoid.damage_nearby_mobs` | leftarm, leftleg, rightarm, rightleg |
| `animation.humanoid.holding` | leftarm, rightarm |
| `animation.humanoid.look_at_target.default` | head |
| `animation.humanoid.look_at_target.gliding` | head |
| `animation.humanoid.look_at_target.swimming` | head |
| `animation.humanoid.move` | leftarm, leftleg, rightarm, rightleg |
| `animation.humanoid.riding.body` | body |
| `animation.humanoid.riding.arms` | leftarm, rightarm |
| `animation.humanoid.riding.legs` | leftleg, rightleg |
| `animation.humanoid.sneaking` | body, head, leftarm, leftleg, rightarm, rightleg |
| `animation.humanoid.swimming` | leftarm, leftleg, rightarm, rightleg |
| `animation.humanoid.use_item_progress` | rightarm |
| `animation.humanoid.melee_spear_hold` | rightarm, rightitem |
| `animation.zombie.melee_spear_hold` | leftarm, rightarm, rightitem |
| `animation.humanoid.melee_spear_use` | rightarm, rightitem |
| `animation.zombie.melee_spear_use` | leftarm, rightarm, rightitem |

---

### iron_golem.animation.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.iron_golem.walk` | body, head |
| `animation.iron_golem.walk_to_target` | body, head |

---

### llama.animation.json (4 animations)

| Animation | Bones |
|-----------|-------|
| `animation.llama.baby_transform` | body, head |
| `animation.llama.baby_transform.v1.0` | body, head |
| `animation.llama.setup` | body |
| `animation.llama.setup.v1.0` | body |

---

### llama_spit.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.llama_spit.setup` | body |

---

### look_at_target.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.common.look_at_target` | head |

---

### minecart.animation.v1.0.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.minecart.move.v1.0` | root |

---

### mooshroom.animation.json (3 animations)

| Animation | Bones |
|-----------|-------|
| `animation.mooshroom.baby_transform` | head |
| `animation.mooshroom.setup` | body |
| `animation.mooshroom.setup.v1.0` | body |

---

### nautilus.animation.json (3 animations)

| Animation | Bones |
|-----------|-------|
| `animation.nautilus.breathe` | body |
| `animation.nautilus.swim` | head |
| `animation.nautilus.look_at_target` | body, head |

---

### npc.animation.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.npc.baby_transform` | head |
| `animation.npc.get_in_bed` | body |

---

### ocelot.animation.json (3 animations)

| Animation | Bones |
|-----------|-------|
| `animation.ocelot.baby_transform` | head |
| `animation.ocelot.sit` | body, head |
| `animation.ocelot.sneak` | body, head |

---

### ocelot.animations.v1.0.json (4 animations)

| Animation | Bones |
|-----------|-------|
| `animation.ocelot_v1.0.baby_transform` | head |
| `animation.ocelot_v1.0.setup` | body, head |
| `animation.ocelot_v1.0.sit` | body, head |
| `animation.ocelot_v1.0.sneak` | body, head |

---

### panda.animation.json (6 animations)

| Animation | Bones |
|-----------|-------|
| `animation.panda.baby_transform` | body, head |
| `animation.panda.lying` | body, head |
| `animation.panda.rolling` | body, head |
| `animation.panda.sitting` | body, head |
| `animation.panda.sneezing` | head |
| `animation.panda.unhappy` | head |

---

### parrot.animation.json (4 animations)

| Animation | Bones |
|-----------|-------|
| `animation.parrot.base` | body, head |
| `animation.parrot.dance` | body, head |
| `animation.parrot.moving` | body |
| `animation.parrot.sitting` | body |

---

### phantom.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.phantom.base_pose` | body |

---

### pig.animation.json (3 animations)

| Animation | Bones |
|-----------|-------|
| `animation.pig.baby_transform` | head |
| `animation.pig.setup` | body |
| `animation.pig.setup.v1.0` | body |

---

### piglin.animation.json (7 animations)

| Animation | Bones |
|-----------|-------|
| `animation.piglin.crossbow.charge` | leftarm, rightarm |
| `animation.piglin.crossbow.hold` | leftarm, rightarm |
| `animation.piglin.sword.attack` | leftarm, rightarm |
| `animation.piglin.hand.attack` | leftarm, rightarm |
| `animation.piglin.move` | leftarm, leftleg, rightarm, rightleg |
| `animation.piglin.admire` | head, leftarm |
| `animation.piglin.celebrate_hunt_special` | body, head, leftarm, rightarm |

---

### pillager.animation.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.pillager.crossbow.charge` | leftarm, rightarm |
| `animation.pillager.crossbow.hold` | leftarm, rightarm |

---

### player.animation.json (42 animations)

See detailed section above.

---

### player_firstperson.animation.json (18 animations)

See detailed section above.

---

### polar_bear.animation.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.polarbear.baby_transform` | head |
| `animation.polarbear.move` | body |

---

### pufferfish.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.pufferfish.flop` | body |

---

### rabbit.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.rabbit.baby_transform` | head |

---

### sheep.animation.json (3 animations)

| Animation | Bones |
|-----------|-------|
| `animation.sheep.baby_transform` | head |
| `animation.sheep.grazing` | head |
| `animation.sheep.setup` | body, head |

---

### shulker.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.shulker.move` | head |

---

### shulker.animations.v1.0.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.shulker.move.v1.0` | head |

---

### shulker_bullet.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.shulker_bullet.move` | body |

---

### skeleton.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.skeleton.attack` | leftarm, rightarm |

---

### skeleton.animations.v1.0.json (19 animations)

| Animation | Bones |
|-----------|-------|
| `animation.humanoid.attack.rotations.v1.0` | body, leftarm, rightarm |
| `animation.humanoid.base_pose.v1.0` | head, leftarm, leftleg, rightarm, rightleg, waist |
| `animation.humanoid.big_head.v1.0` | hat, head |
| `animation.humanoid.bob.v1.0` | leftarm, rightarm |
| `animation.humanoid.bow_and_arrow.v1.0` | leftarm, rightarm |
| `animation.humanoid.brandish_spear.v1.0` | rightarm |
| `animation.humanoid.charging.v1.0` | rightarm |
| `animation.humanoid.damage_nearby_mobs.v1.0` | leftarm, leftleg, rightarm, rightleg |
| `animation.humanoid.holding.v1.0` | leftarm, rightarm |
| `animation.humanoid.look_at_target.default.v1.0` | hat, head |
| `animation.humanoid.look_at_target.gliding.v1.0` | hat, head |
| `animation.humanoid.look_at_target.swimming.v1.0` | hat, head |
| `animation.humanoid.move.v1.0` | leftarm, leftleg, rightarm, rightleg |
| `animation.humanoid.riding.arms.v1.0` | leftarm, rightarm |
| `animation.humanoid.riding.legs.v1.0` | leftleg, rightleg |
| `animation.humanoid.sneaking.v1.0` | body, head, leftarm, leftleg, rightarm, rightleg |
| `animation.humanoid.swimming.v1.0` | leftarm, leftleg, rightarm, rightleg |
| `animation.humanoid.use_item_progress.v1.0` | rightarm |
| `animation.skeleton.attack.v1.0` | leftarm, rightarm |

---

### sniffer.animation.json (7 animations)

| Animation | Bones |
|-----------|-------|
| `animation.sniffer.baby_transform` | head |
| `animation.sniffer.walk` | body, head |
| `animation.sniffer.longsniff` | head |
| `animation.sniffer.search` | body, head |
| `animation.sniffer.dig` | body, head |
| `animation.sniffer.stand_up` | body, head |
| `animation.sniffer.feeling_happy` | head |

---

### spider.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.spider.look_at_target` | head |

---

### squid.animation.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.squid.move` | body |
| `animation.squid.rotate` | body |

---

### strider.animation.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.strider.look_at_target.default` | body |
| `animation.strider.walk` | body |

---

### tripod_camera.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.tripod_camera.neutral` | body |

---

### tropicalfish.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.tropicalfish.flop` | body |

---

### turtle.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.turtle.general` | body |

---

### vex.animation.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.vex.idle` | leftItem, leftarm, rightItem, rightarm |
| `animation.vex.charge` | leftarm, rightarm |

---

### villager.animation.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.villager.baby_transform` | head (scale) |
| `animation.villager.get_in_bed` | body |

---

### vindicator.animation.json (4 animations)

| Animation | Bones |
|-----------|-------|
| `animation.vindicator.attack` | leftarm, rightarm |
| `animation.vindicator.hand_attack` | leftarm, rightarm |
| `animation.vindicator.base` | leftItem, leftarm, rightItem, rightarm |
| `animation.vindicator.riding.arms` | leftarm |

---

### warden.animation.json (9 animations)

| Animation | Bones |
|-----------|-------|
| `animation.warden.look_at_target.default` | head |
| `animation.warden.move` | body, head |
| `animation.warden.emerge` | body, head |
| `animation.warden.dig` | body, head |
| `animation.warden.roar` | body, head |
| `animation.warden.sniff` | body, head |
| `animation.warden.bob` | body, head |
| `animation.warden.attack` | body, head |
| `animation.warden.sonic_boom` | body, head |

---

### wither_skeleton.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.wither_skeleton.attack` | leftarm, rightarm |

---

### wither_skull.animation.json (1 animation)

| Animation | Bones |
|-----------|-------|
| `animation.wither_skull.move` | head |

---

### wolf.animations.json (5 animations)

| Animation | Bones |
|-----------|-------|
| `animation.wolf.baby_scaling` | head |
| `animation.wolf.head_rot_z` | head |
| `animation.wolf.setup` | body |
| `animation.wolf.shaking` | body |
| `animation.wolf.sitting` | body |

---

### zombie.animation.json (2 animations)

| Animation | Bones |
|-----------|-------|
| `animation.zombie.attack_bare_hand` | leftarm, rightarm |
| `animation.zombie.swimming` | body, leftarm, leftleg, rightarm, rightleg |

---

## Dressing Room Animations (48 animations)

These are persona/dressing room animations that use player-like bone names:

| File | Animation | Bones |
|------|-----------|-------|
| dressing_room_idle_arm_1 | animation.idle_arm_1 | leftArm, rightArm, waist |
| dressing_room_idle_back_1 | animation.idle_back_1 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_idle_bottom_1 | animation.idle_bottom_1 | leftLeg, rightLeg, root, waist |
| dressing_room_idle_torso_1 | animation.idle_torso_1 | body, head, leftArm, rightArm, waist |
| dressing_room_react_arm_1 | animation.react_arm_1 | leftArm, rightArm, waist |
| dressing_room_react_arm_2 | animation.react_arm_2 | leftArm, rightArm, waist |
| dressing_room_react_back_1 | animation.react_back_1 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_back_2 | animation.react_back_2 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_bored_1 | animation.react_bored_1 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_bored_arm_1 | animation.react_bored_arm_1 | leftArm, rightArm, waist |
| dressing_room_react_bored_back_1 | animation.react_bored_back_1 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_bored_bottom_1 | animation.react_bored_bottom_1 | leftLeg, rightLeg, root, waist |
| dressing_room_react_bored_head_1 | animation.react_bored_head_1 | head, waist |
| dressing_room_react_bored_torso_1 | animation.react_bored_torso_1 | body, head, leftArm, rightArm, waist |
| dressing_room_react_bottom_1 | animation.react_bottom_1 | leftLeg, rightLeg, root, waist |
| dressing_room_react_bottom_2 | animation.react_bottom_2 | leftLeg, rightLeg, root, waist |
| dressing_room_react_bottom_3 | animation.react_bottom_3 | leftLeg, rightLeg, root, waist |
| dressing_room_react_confirm_1 | animation.react_confirm_1 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_confirm_2 | animation.react_confirm_2 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_head_1 | animation.react_head_1 | head, waist |
| dressing_room_react_head_2 | animation.react_head_2 | head, waist |
| dressing_room_react_idle | animation.react_idle | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_offer_1 | animation.react_offer_1 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_offer_2 | animation.react_offer_2 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_offer_arm_1 | animation.react_offer_arm_1 | leftArm, rightArm, waist |
| dressing_room_react_offer_arm_2 | animation.react_offer_arm_2 | leftArm, rightArm, waist |
| dressing_room_react_offer_back_1 | animation.react_offer_back_1 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_offer_back_2 | animation.react_offer_back_2 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_offer_bottom_1 | animation.react_offer_bottom_1 | leftLeg, rightLeg, root, waist |
| dressing_room_react_offer_bottom_2 | animation.react_offer_bottom_2 | leftLeg, rightLeg, root, waist |
| dressing_room_react_offer_head_1 | animation.react_offer_head_1 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_offer_head_2 | animation.react_offer_head_2 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_offer_torso_1 | animation.react_offer_torso_1 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_offer_torso_2 | animation.react_offer_torso_2 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| dressing_room_react_torso_1 | animation.react_torso_1 | head, leftArm, rightArm, waist |
| dressing_room_react_torso_2 | animation.react_torso_2 | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |

---

## Summary Statistics

| Category | Files | Animations |
|----------|-------|-----------|
| Player-specific | 3 | 60 |
| Humanoid shared | 2 | 47 |
| Dressing room/Persona | 36 | 36 |
| Mob animations (using same bone names) | 50+ | 243 |
| Item animations | 4 | 6 |
| **TOTAL** | **68** | **386** |

### Bones Animated by Non-Player Files

Many mob animations use generic bone names that happen to match player bones:

| Bone | Used by (non-player files) |
|------|---------------------------|
| `body` | allay, armadillo, enderman, fox, frog, iron_golem, llama, nautilus, panda, parrot, phantom, pig, polar_bear, pufferfish, shulker_bullet, squid, strider, tripod_camera, tropicalfish, turtle, villager, warden, wolf, zombie |
| `head` | allay, armadillo, enderman, goat, hoglin, horse, nautilus, ocelot, panda, parrot, pig, polar_bear, rabbit, sheep, shulker, sniffer, spider, villager, warden, wither_skull, wolf |
| `leftarm` | agent, enderman, evoker, piglin, pillager, skeleton, vex, vindicator, wither_skeleton, zombie |
| `rightarm` | agent, enderman, evoker, piglin, pillager, skeleton, vex, vindicator, wither_skeleton, zombie |
| `leftleg` | agent, enderman, evoker, piglin, zombie |
| `rightleg` | agent, enderman, evoker, piglin, zombie |
| `root` | ender_dragon, minecart |
| `hat` | enderman, skeleton (v1.0) |
| `rightItem` | allay, vex, vindicator |

---
