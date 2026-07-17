# Animation References
## Vanilla Resource Pack v26.0.0

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
  - `body` → rotation (dynamic)
  - `leftArm` → rotation (dynamic)
  - `rightArm` → rotation (30° swing)
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
  - `leftArm` → rotation (cosine wave)
  - `rightArm` → rotation (opposite cosine wave)
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
  - `leftArm` → rotation (target rotation + sneaking offset)
  - `rightArm` → rotation (target rotation)
  - `rightItem` → rotation [0, -10, 0] (static)
- **Purpose:** Bow aiming pose — arms follow look direction

---

#### animation.player.cape
- **Loop:** Yes
- **Bones Affected:** `cape`
- **Properties:**
  - `cape` → position (armor offset), rotation (dynamic)
- **Purpose:** Cape physics/flap animation

---

#### animation.player.crossbow_equipped
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - `leftArm` → position [0, 0, 0.5], rotation (dynamic)
  - `rightArm` → rotation (dynamic)
- **Purpose:** Crossbow aiming pose

---

#### animation.player.crossbow_hold
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - `leftArm` → rotation (swimming check, target rotation)
  - `rightArm` → rotation (swimming check, target rotation)
- **Purpose:** Holding crossbow ready

---

#### animation.player.melee_spear_attack
- **Loop:** Yes
- **Bones Affected:** `body`, `rightArm`, `rightItem`
- **Properties:**
  - `body` → rotation (attack body rotation)
  - `rightArm` → rotation (spear attack motion)
  - `rightItem` → position [0, -1.5, -1.5], rotation (dynamic)
- **Purpose:** Spear thrust attack animation

---

#### animation.player.glide
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`, `leftLeg`, `rightLeg`
- **Properties:**
  - Arms → rotation (spread out)
  - Legs → rotation (slight angle)
- **Purpose:** Elytra gliding pose — limbs spread

---

#### animation.player.holding
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation (holding position)
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
  - `head` → rotation (inverted look-at)
- **Purpose:** Head tracking when upside down

---

#### animation.player.look_at_target.ui
- **Loop:** Yes
- **Bones Affected:** `head`
- **Properties:**
  - `head` → rotation (UI look direction)
- **Purpose:** Head tracking in UI screens

---

#### animation.player.move.arms
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation (walk cycle)
- **Purpose:** Arm swing while walking

---

#### animation.player.move.arms.single
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation (one-armed walk)
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
  - `leftArm` → rotation (raised up)
  - `rightArm` → rotation (normal)
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
  - `leftLeg` → rotation (walk cycle, slight angle)
  - `rightLeg` → rotation (walk cycle, opposite phase)
- **Purpose:** Leg animation while walking

---

#### animation.player.move.legs.inverted
- **Loop:** Yes
- **Bones Affected:** `leftLeg`, `rightLeg`
- **Properties:**
  - Both legs → position [0, 8, 0], rotation (inverted angles)
- **Purpose:** Inverted walking (upside down)

---

#### animation.player.move.legs.single
- **Loop:** Yes
- **Bones Affected:** `leftLeg`, `rightLeg`
- **Properties:**
  - Both legs → rotation (walk cycle)
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
  - `root` → position (riding offset)
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
  - Both legs → rotation (sitting pose)
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
  - `leftItem` → position (dynamic), rotation (dynamic)
- **Purpose:** Shield blocking with off hand

---

#### animation.player.sleeping
- **Loop:** Yes
- **Bones Affected:** `head`, `root`
- **Properties:**
  - `head` → rotation (dynamic)
  - `root` → position (dynamic), rotation [-90, 0, 0] (lying down)
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
  - `root` → position [0, 1.25, 9], rotation (dynamic)
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
  - `root` → position (dynamic), rotation (horizontal)
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
  - Both legs → rotation (kick cycle)
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
  - `root` → position (dynamic), rotation (horizontal)
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
  - Both legs → rotation (crawl leg movement)
- **Purpose:** Crawling leg animation

---

### humanoid.animation.json

---

#### animation.humanoid.attack.rotations
- **Loop:** Yes
- **Bones Affected:** `body`, `leftArm`, `rightArm`
- **Properties:**
  - `body` → rotation (body twist)
  - `leftArm` → rotation (arm swing)
  - `rightArm` → rotation (attack swing)
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
  - Both arms → rotation (cosine wave)
- **Purpose:** Shared idle arm bob

---

#### animation.humanoid.bow_and_arrow
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation (bow pose)
- **Purpose:** Shared bow aiming pose

---

#### animation.humanoid.brandish_spear
- **Loop:** Yes
- **Bones Affected:** `rightArm`
- **Properties:**
  - `rightArm` → rotation (spear raise)
- **Purpose:** Spear brandish/throw pose

---

#### animation.humanoid.holding_spyglass
- **Loop:** Yes
- **Bones Affected:** `rightArm`
- **Properties:**
  - `rightArm` → rotation (spyglass hold + 5°)
- **Purpose:** Holding spyglass up to eye

---

#### animation.humanoid.tooting_goat_horn
- **Loop:** Yes
- **Bones Affected:** `rightArm`, `rightItem`
- **Properties:**
  - `rightArm` → rotation (dynamic + 5°)
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
  - `rightArm` → rotation (dynamic + 5°)
  - `rightItem` → position (6 keyframes), rotation (6 keyframes)
- **Purpose:** Brushing animation (suspicious sand/gravel)

---

#### animation.humanoid.celebrating
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - `leftArm` → rotation (dynamic + [180, -135])
  - `rightArm` → rotation (dynamic + [180, 153])
- **Purpose:** Victory celebration — arms raised

---

#### animation.humanoid.charging
- **Loop:** Yes
- **Bones Affected:** `rightArm`
- **Properties:**
  - `rightArm` → rotation (dynamic + 5°)
- **Purpose:** Charging attack pose

---

#### animation.humanoid.damage_nearby_mobs
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`, `leftLeg`, `rightLeg`
- **Properties:**
  - All four limbs → rotation (knockback)
- **Purpose:** Iron golem smash animation

---

#### animation.humanoid.holding
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`
- **Properties:**
  - Both arms → rotation (dynamic + [0, 0])
- **Purpose:** Default item holding pose

---

#### animation.humanoid.look_at_target.default
- **Loop:** Yes
- **Bones Affected:** `head`
- **Properties:**
  - `head` → rotation (look-at + 0°)
- **Purpose:** Default head tracking

---

#### animation.humanoid.look_at_target.gliding
- **Loop:** Yes
- **Bones Affected:** `head`
- **Properties:**
  - `head` → rotation (look-at + [-45, 0])
- **Purpose:** Head tracking while gliding

---

#### animation.humanoid.look_at_target.swimming
- **Loop:** Yes
- **Bones Affected:** `head`
- **Properties:**
  - `head` → rotation (look-at + 0°)
- **Purpose:** Head tracking while swimming

---

#### animation.humanoid.move
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`, `leftLeg`, `rightLeg`
- **Properties:**
  - Arms → rotation (walk cycle)
  - Legs → rotation (walk cycle, slight angle)
- **Purpose:** Full body walk animation

---

#### animation.humanoid.riding.body
- **Loop:** Yes
- **Bones Affected:** `body`
- **Properties:**
  - `body` → position (riding offset)
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
  - Both legs → rotation (sitting)
- **Purpose:** Legs while riding

---

#### animation.humanoid.sneaking
- **Loop:** Yes
- **Bones Affected:** `body`, `head`, `leftArm`, `rightArm`, `leftLeg`, `rightLeg`
- **Properties:**
  - `body` → rotation (dynamic)
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
  - Legs → rotation (kick)
- **Purpose:** Full body swimming animation

---

#### animation.humanoid.use_item_progress
- **Loop:** Yes
- **Bones Affected:** `rightArm`
- **Properties:**
  - `rightArm` → rotation (item use motion)
- **Purpose:** Using/eating animation

---

#### animation.humanoid.melee_spear_hold
- **Loop:** Yes
- **Bones Affected:** `rightArm`, `rightItem`
- **Properties:**
  - `rightArm` → rotation (dynamic + 0°)
  - `rightItem` → position [0, -1.5, -1.5] (static)
- **Purpose:** Holding spear ready

---

#### animation.humanoid.melee_spear_use
- **Loop:** Yes
- **Bones Affected:** `rightArm`, `rightItem`
- **Properties:**
  - `rightArm` → rotation (thrust)
  - `rightItem` → position [0, -1.5, -1.5], rotation (dynamic)
- **Purpose:** Spear thrust attack

---

#### animation.zombie.melee_spear_hold
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`, `rightItem`
- **Properties:**
  - Both arms → rotation (dynamic + 0°)
  - `rightItem` → position [0, -1.5, -1.5] (static)
- **Purpose:** Zombie spear hold

---

#### animation.zombie.melee_spear_use
- **Loop:** Yes
- **Bones Affected:** `leftArm`, `rightArm`, `rightItem`
- **Properties:**
  - Both arms → rotation (dynamic)
  - `rightItem` → position [0, -1.5, -1.5], rotation (dynamic)
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

## Common Animation Effects

Useful for skin pack manipulation:

| Animation | Effect |
|-----------|--------|
| `animation.witch.general` | Stops any/all original animations |
| `animation.evoker.general` | Removes arms/torso area |
| `animation.parrot.sitting` | Moves torso area down by roughly 2 pixels |
| `animation.axolotl.idle_floor_underwater` | Moves torso area up by roughly 2 pixels |
| `animation.fireworks_rocket.move` | Scales torso area to about 0.6, moves with head |
| `animation.arrow.move` | Same as fireworks, head gets stretched |
| `animation.humanoid.big_head` | Scales head and outer skin layers to different sizes |
| `animation.enderman.scary_face` | Moves head higher than outer skin layer |
| `animation.tripod_camera.neutral` | Moves torso area to the floor |
| `animation.elytra.default` | Scales torso area up by 1 pixel |
| `animation.player.base_pose.upside_down` | Makes torso area upside-down |
| `animation.strider.look_at_target.default` | Fixes issues with enderman, fireworks, and arrow animations |
| `animation.goat.look_at_target` | Limits player head movement slightly |

---

## Complete Cross-File Animation Scan

**Total: 386 animations across 68 files** affect player bone names.

Many mob animations use the same bone names as the player (body, head, leftarm, rightarm, etc.). Below is a summary of notable mob animations that affect player-like bones:

| File | Notable Animations | Bones Used |
|------|-------------------|------------|
| `agent.animation.json` | move, swing_arms, shrug | body, head, leftArm, leftLeg, rightArm, rightLeg |
| `allay.animation.json` | idle, fly, hold_item, dance | body, head, rightItem |
| `armadillo.animation.json` | walk, roll_up, rolled_up | body, head |
| `drowned.animation.json` | attack.rotations, swimming | body, leftarm, rightarm, leftleg, rightleg, root |
| `enderman.animation.json` | base_pose, scary_face, carrying | body, hat, head, leftarm, leftleg, rightarm, rightleg |
| `evoker.animation.json` | casting, general, move | leftarm, leftLeg, rightarm, rightLeg |
| `fox.animation.json` | crouch, pounce, sit, sleep | body, head |
| `piglin.animation.json` | crossbow.charge, sword.attack, move | body, head, leftarm, leftleg, rightarm, rightleg |
| `skeleton.animations.v1.0.json` | Full humanoid set | body, head, leftarm, leftleg, rightarm, rightleg, waist |
| `villager.animation.json` | get_in_bed | body |
| `warden.animation.json` | move, emerge, dig, roar, sniff | body, head |
| `zombie.animation.json` | attack_bare_hand, swimming | body, leftarm, leftleg, rightarm, rightleg |

---

## Dressing Room Animations

These persona/dressing room animations use player-like bone names:

| Animation | Bones |
|-----------|-------|
| `animation.idle_arm_1` | leftArm, rightArm, waist |
| `animation.idle_back_1` | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| `animation.idle_bottom_1` | leftLeg, rightLeg, root, waist |
| `animation.idle_torso_1` | body, head, leftArm, rightArm, waist |
| `animation.react_arm_1` | leftArm, rightArm, waist |
| `animation.react_back_1` | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| `animation.react_bored_1` | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| `animation.react_confirm_1` | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| `animation.react_head_1` | head, waist |
| `animation.react_idle` | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
| `animation.react_offer_1` | body, head, leftArm, leftLeg, rightArm, rightLeg, root, waist |
