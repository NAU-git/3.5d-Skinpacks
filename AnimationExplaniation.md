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

| Animation | Bones | Purpose |
|-----------|-------|---------|
| `animation.player.attack.positions` | head | Resets head rotation during attack |
| `animation.player.attack.rotations` | body, leftArm, rightArm | Main attack — swings arms during melee combat |
| `animation.player.base_pose.upside_down` | waist | Flips player upside down (commands) |
| `animation.player.bob` | leftArm, rightArm | Idle arm bobbing while walking |
| `animation.player.bob.stationary` | leftArm, rightArm | Idle arm bobbing while standing still |
| `animation.player.bow_equipped` | leftArm, rightArm, rightItem | Bow aiming pose — arms follow look direction |
| `animation.player.cape` | cape | Cape physics/flap animation |
| `animation.player.crossbow_equipped` | leftArm, rightArm | Crossbow aiming pose |
| `animation.player.crossbow_hold` | leftArm, rightArm | Holding crossbow ready |
| `animation.player.melee_spear_attack` | body, rightArm, rightItem | Spear thrust attack animation |
| `animation.player.glide` | leftArm, rightArm, leftLeg, rightLeg | Elytra gliding pose — limbs spread |
| `animation.player.holding` | leftArm, rightArm | Default holding items pose |
| `animation.player.holding_heavy_core` | rightItem | Offset for heavy core item |
| `animation.player.holding.zombie` | leftArm, rightArm | Zombie holding pose (arms forward) |
| `animation.player.look_at_target.inverted` | head | Head tracking when upside down |
| `animation.player.look_at_target.ui` | head | Head tracking in UI screens |
| `animation.player.move.arms` | leftArm, rightArm | Arm swing while walking |
| `animation.player.move.arms.single` | leftArm, rightArm | Single-arm swing variant |
| `animation.player.move.arms.stationary` | leftArm, rightArm | No arm movement (standing still) |
| `animation.player.move.arms.statue_of_liberty` | leftArm, rightArm | One arm raised pose |
| `animation.player.move.arms.zombie` | leftArm, rightArm | Zombie arms forward pose |
| `animation.player.move.legs` | leftLeg, rightLeg | Leg animation while walking |
| `animation.player.move.legs.inverted` | leftLeg, rightLeg | Inverted walking (upside down) |
| `animation.player.move.legs.single` | leftLeg, rightLeg | Single-leg walk variant |
| `animation.player.move.legs.stationary` | leftLeg, rightLeg | No leg movement (standing still) |
| `animation.player.riding.root` | root | Base position while riding |
| `animation.player.riding.arms` | leftArm, rightArm | Arms resting while riding |
| `animation.player.riding.arms.zombie` | leftArm, rightArm | Zombie arms while riding |
| `animation.player.riding.legs` | leftLeg, rightLeg | Legs while riding |
| `animation.player.shield_block_main_hand` | rightArm, rightItem | Shield blocking with main hand |
| `animation.player.shield_block_off_hand` | leftArm, leftItem | Shield blocking with off hand |
| `animation.player.sleeping` | head, root | Sleeping pose — player lies horizontal |
| `animation.player.sneaking` | body, head, leftArm, rightArm, leftLeg, rightLeg, root | Sneaking/crouching — entire body lowered |
| `animation.player.sneaking.inverted` | body, head, leftArm, rightArm, leftLeg, rightLeg, root | Sneaking while upside down |
| `animation.player.swim` | leftArm, rightArm, root | Swimming arm stroke (1.3s loop) |
| `animation.player.swim.no_right_arm` | leftArm, root | Swimming with only left arm |
| `animation.player.swim.legs` | leftLeg, rightLeg | Swimming leg kick |
| `animation.player.swim.legs.single` | leftLeg, rightLeg | Single-leg kick variant |
| `animation.player.swim.legs.stationary` | leftLeg, rightLeg | No leg kick (standing still in water) |
| `animation.player.crawl` | leftArm, rightArm, root | Crawling arm animation (1.3s loop) |
| `animation.player.crawl.no_right_arm` | leftArm, root | Crawling with only left arm |
| `animation.player.crawl.legs` | leftLeg, rightLeg | Crawling leg animation |

---

### humanoid.animation.json

| Animation | Bones | Purpose |
|-----------|-------|---------|
| `animation.humanoid.attack.rotations` | body, leftArm, rightArm | Shared attack animation for humanoids |
| `animation.humanoid.base_pose` | waist | Default waist rotation (neutral) |
| `animation.humanoid.big_head` | head | Enlarges head (special effects) |
| `animation.humanoid.bob` | leftArm, rightArm | Shared idle arm bob |
| `animation.humanoid.bow_and_arrow` | leftArm, rightArm | Shared bow aiming pose |
| `animation.humanoid.brandish_spear` | rightArm | Spear brandish/throw pose |
| `animation.humanoid.holding_spyglass` | rightArm | Holding spyglass up to eye |
| `animation.humanoid.tooting_goat_horn` | rightArm, rightItem | Blowing goat horn |
| `animation.humanoid.holding_brush` | rightItem | Brush item default position |
| `animation.humanoid.brushing` | rightArm, rightItem | Brushing animation (suspicious sand/gravel) |
| `animation.humanoid.celebrating` | leftArm, rightArm | Victory celebration — arms raised |
| `animation.humanoid.charging` | rightArm | Charging attack pose |
| `animation.humanoid.damage_nearby_mobs` | leftArm, rightArm, leftLeg, rightLeg | Iron golem smash animation |
| `animation.humanoid.holding` | leftArm, rightArm | Default item holding pose |
| `animation.humanoid.look_at_target.default` | head | Default head tracking |
| `animation.humanoid.look_at_target.gliding` | head | Head tracking while gliding |
| `animation.humanoid.look_at_target.swimming` | head | Head tracking while swimming |
| `animation.humanoid.move` | leftArm, rightArm, leftLeg, rightLeg | Full body walk animation |
| `animation.humanoid.riding.body` | body | Body position while riding |
| `animation.humanoid.riding.arms` | leftArm, rightArm | Arms while riding |
| `animation.humanoid.riding.legs` | leftLeg, rightLeg | Legs while riding |
| `animation.humanoid.sneaking` | body, head, leftArm, rightArm, leftLeg, rightLeg | Humanoid sneak pose |
| `animation.humanoid.swimming` | leftArm, rightArm, leftLeg, rightLeg | Full body swimming (1.3s loop) |
| `animation.humanoid.use_item_progress` | rightArm | Using/eating animation |
| `animation.humanoid.melee_spear_hold` | rightArm, rightItem | Holding spear ready |
| `animation.humanoid.melee_spear_use` | rightArm, rightItem | Spear thrust attack |
| `animation.zombie.melee_spear_hold` | leftArm, rightArm, rightItem | Zombie spear hold |
| `animation.zombie.melee_spear_use` | leftArm, rightArm, rightItem | Zombie spear attack |

---

### player_firstperson.animation.json

| Animation | Bones | Purpose |
|-----------|-------|---------|
| `animation.player.first_person.attack_rotation` | rightArm | First-person attack swing |
| `animation.player.first_person.attack_rotation_item` | rightItem | First-person item attack |
| `animation.player.first_person.base_pose` | body, head | First-person base camera pose |
| `animation.player.first_person.crossbow_equipped` | leftArm, rightItem | First-person crossbow aiming |
| `animation.player.first_person.crossbow_hold` | rightItem | First-person crossbow hold |
| `animation.player.first_person.melee_spear_hold` | rightItem | First-person spear hold |
| `animation.player.first_person.melee_spear_use` | rightItem | First-person spear use |
| `animation.player.first_person.melee_spear_attack` | rightItem | First-person spear attack |
| `animation.player.first_person.breathing_bob` | rightItem | Idle item bob |
| `animation.player.first_person.empty_hand` | rightArm, rightItem, leftItem | Empty hand first-person pose |
| `animation.player.first_person.map_hold` | leftArm, rightArm | Holding map with both hands |
| `animation.player.first_person.map_hold_attack` | leftArm, rightArm | Using map item |
| `animation.player.first_person.map_hold_main_hand` | rightArm | Map in main hand |
| `animation.player.first_person.map_hold_off_hand` | leftArm | Map in off hand |
| `animation.player.first_person.swap_item` | leftArm, rightArm | Item swap animation |
| `animation.player.first_person.shield_block` | leftArm, rightArm | First-person shield block |
| `animation.player.first_person.vr_attack_rotation` | rightArm | VR attack swing |
| `animation.player.first_person.walk` | leftArm, rightArm | First-person walk bob |

---

### look_at_target.animation.json

| Animation | Bones | Purpose |
|-----------|-------|---------|
| `animation.common.look_at_target` | head | Generic head look-at target |

---

### elytra.animation.json

| Animation | Bones | Purpose |
|-----------|-------|---------|
| `animation.elytra.default` | body | Elytra default scale |
| `animation.elytra.gliding` | body | Elytra gliding scale |
| `animation.elytra.sneaking` | body | Elytra sneaking scale |
| `animation.elytra.sleeping` | body | Elytra sleeping scale |
| `animation.elytra.swimming` | body | Elytra swimming scale |

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
