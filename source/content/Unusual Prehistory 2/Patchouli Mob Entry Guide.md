Hi. You want to write entries for the UP-2 patchouli book. 
*Written by @vakypanda on discord. Ping/dm me for questions*
## Overview

### Structure
- **Entry** → A JSON file containing all data for one mob.
- **Page** → A template section within the entry.
- **Variables** → Editable fields within each page.

All entries are located at: 
`src/main/resources/assets/unusual_prehistory/patchouli_books/paleopedia/en_us/entries/mobs`

It is strongly recommended to clone the in-dev GitHub repository before editing.  
Editing files separately increases the risk of formatting or ID errors.
## Entry JSON

![[carnotaurus_page.png]]

```json
{  
  "name": "Carnotaurus",  
  "icon": "unusual_prehistory:textures/gui/paleopedia/icons/carnotaurus.png",  
  "category": "unusual_prehistory:mobs",  
  "advancement": "unusual_prehistory:revive_carnotaurus",  
  "extra_recipe_mappings": {  
    "unusual_prehistory:fury_fossil": 0,  
    "unusual_prehistory:carnotaurus_egg": 0,  
    "unusual_prehistory:carnotaurus_spawn_egg": 0  
  },  
  "pages": [  
    {  
      "type": "unusual_prehistory:mob_entry_1",  
      "display_name": "Carnotaurus",  
      "id": "carnotaurus",  
      "flavor_text": "meat-eating-bull",  
      "fossil_item": "unusual_prehistory:fury_fossil",  
      "egg_item": "unusual_prehistory:carnotaurus_egg",  
      "variant_key": "",  
      "image_tooltip": "An abelisaur with a short, deep skull and massive pair of horns, Carnotaurus furiously charges at anything it sets its sights on in a blind, rage-fuelled stampede."  
    },  
    {  
      "id": "carnotaurus",  
      "type": "unusual_prehistory:mob_entry_2",  
  
      "era_image": "late_cretaceous",  
      "era_tooltip_period": "Late Cretaceous Period",  
  
      "temperament.temperament_type": "hostile",  
  
      "clone.clone_type": "nest_egg",  
      "clone.clone_tooltip_heading": "Nest Egg",  
      "clone.clone_tooltip": "Egg must be placed down to hatch",  
  
      "activity.activity_type": "diurnal",  
      "activity.activity_tooltip": "Active during the day",  
  
      "feature_1.item": "minecraft:skeleton_skull",  
      "feature_1.tooltip": "§7A furious animal, Carnotaurus will charge at any mob it sees, ramming them with it's horns",  
      "feature_1.title_one_line": "Furious",  
      "feature_1.title_two_line": "",  
  
      "feature_2.item": "tag:unusual_prehistory:permanently_pacifies_mob",  
      "feature_2.tooltip": "§7After being §apacified§7, Carnotaurus will continue to attack most monsters",  
      "feature_2.title_one_line": "Bodyguard!",  
      "feature_2.title_two_line": ""  
    }  
  ]  
}
```

## High-Level Fields 
#### `name` 
Name displayed on the Category page. Should be Title Case (so `Carnotaurus` or `Lobe-Finned Fish`)

#### `icon`
Icons are located under `"unusual_prehistory:textures/gui/paleopedia/icons/[mob].png` (eg: `carnotarus.png`)

#### `category`
Don't edit this variable 

#### `advancement`
Uses advancement ID, structure is `unusual_prehistory:revive_x` (eg; `unusual_prehistory:revive_lobe_finned_fish`

#### `extra_recipe_mappings`
All items that will allow you to quick-check this specific page from your inventory. Should be item IDs of the spawn egg, fossil and egg. The number corresponds to page number, keep it as `0`

```json
"extra_recipe_mappings": {  
    "unusual_prehistory:fury_fossil": 0,  
    "unusual_prehistory:carnotaurus_egg": 0,  
    "unusual_prehistory:carnotaurus_spawn_egg": 0  
  },  
```

This is all information for organising and displaying the page within the context of the patchouli book. Next is the actual entry, under `pages`. Each page has a `type`, and there are 3-4 types you can use for a mob entry:

## Page Types

1. `unusual_prehistory:mob_entry_1`: page with render
2. `unusual_prehistory:mob_entry_2`: page with behaviours and 3 features 
3. `unusual_prehistory:mob_entry_features`: page with 4 features 
4. `unusual_prehistory:mob_entry_text`: page with one long text-wall 

---
### `unusual_prehistory:mob_entry_1`

#### `display_name` 
Identical to `name

#### `id` 
id of the mob, without `unusual_prehistory:` prefix. Example; `unusual_prehistory:lobe_finned_fish` -> `lobe_finned_fish`

#### `flavor_text`
English translation of animal name. If there is none (such as mobs like Manipulator and Lobe Finned Fish) remove the line entirely

#### `fossil_item`
Item ID of the fossil used to revive the creature

#### `egg_item`
Item ID of the egg that is obtained from the fossil

#### `image_tooltip`
Short blurb that appears when the player hovers over the animal render. Keep it concise. 

#### `variant_key`
Part of the image tooltip, for mobs with variants that are based on species or genera. The numbers are written on the render. 
- Species are not capitalised, Eg (Dunkleosteus); `"variant_key": "1 raveri 2 marsaisi 3 terrelli",`
- Genera are capitalsied, Eg (Lobe Finned Fish); `"variant_key": "1 Allenypterus 2 Scaumenacia 3 Laccognathus 4 Eusthenopteron 5 Gooloongia",`

---
### `unusual_prehistory:mob_entry_2

#### `id` 
id of the mob, without `unusual_prehistory:` prefix. Example; `unusual_prehistory:lobe_finned_fish` -> `lobe_finned_fish`
#### `era_image`
Has to be prefixed with `early_`, `mid_` or `late_`, Eg; `late_cretaceous`, `early_cenozoic`, `mid_ordovician`
Valid eras are;
- `cambrian`
- `ordovician`
- `silurian`
- `devonian`
- `carboniferous`
- `permian`
- `triassic`
- `jurassic`
- `cretaceous`
- `cenozoic`
- `holocene`*
- `precambrian`*
\*These have NO `early_`, `mid_` or `late` prefixes

Some mobs have large existences over many eras or long periods of time. They should have custom era images, and the era image field should just be identical to `id` (so `carnotaurus` or `lobe_finned_fish`)

#### `era_tooltip_period`
Tooltip the player sees when they hover over the era image - 
- Can be one-era, Eg;`Late Cretaceous Period` or `Holocene Epoch`
- Can be two-era, Eg; `Late Cretaceous Period into the Holocene Epoch`
	- Take note of "into the" here

#### `temperament.temperament_type` 
Valid values are 
- `hostile`
- `passive`
- `neutral`
- `boss`

#### `clone.clone_type`, `clone.clone_tooltip` & `clone.clone_tooltip_heading`

Place-able Egg (mostly for reptiles and non-avian dinosaurs)
```json
"clone.clone_type": "nest_egg",  
"clone.clone_tooltip_heading": "Nest Egg",  
"clone.clone_tooltip": "Egg must be placed down to hatch",
```

Throw-able Egg (for avians mostly)
```json
"clone.clone_type": "projectile_egg",  
"clone.clone_tooltip_heading": "Projectile Egg",  
"clone.clone_tooltip": "Egg must be thrown to hatch",
```

Underwater Egg (for sharks and aquatic creatures)
```json
"clone.clone_type": "aquatic_egg",  
"clone.clone_tooltip_heading": "Aquatic Egg",  
"clone.clone_tooltip": "Egg must be placed underwater to hatch",
```

Floating Egg (mostly for amphibians)
```json
"clone.clone_type": "raft_egg",  
"clone.clone_tooltip_heading": "Raft Egg",  
"clone.clone_tooltip": "Egg must be placed on-top of water to hatch",
```

Embryo (mostly for mammals)
```json
"clone.clone_type": "embryo",  
"clone.clone_tooltip_heading": "Embryo",  
"clone.clone_tooltip": "Embryo must be placed in §aLiving Ooze§r §7to gestate",
```

#### `activity.activity_type` & `activity.activity_tooltip` 

Awake at day 
```json
"activity.activity_type": "diurnal",  
"activity.activity_tooltip": "Active during the day"
```

Awake at night 
```json
"activity.activity_type": "nocturnal",  
"activity.activity_tooltip": "Active during the night"
```

Sleep depends on external factors that are not day night or dawn 
```json
"activity.activity_type": "cathemeral",  
"activity.activity_tooltip": "Active randomly throughout the day or based on specific factors"
```

Animal does not sleep
```json
"activity.activity_type": "sleepless",  
"activity.activity_tooltip": "Does not sleep"
```

Animal is awake at dusk and/or dawn 
```json
"activity.activity_type": "crepuscular",  
"activity.activity_tooltip": "Active at dusk or dawn"
```

#### `feature_x.item`... 
See [[#Feature Writing]]

---
### `unusual_prehistory:mob_entry_features`

See [[#Feature Writing]]

---
### `unusual_prehistory:mob_entry_text`

#### `text`
Paragraph that can be [formatted](https://vazkiimods.github.io/Patchouli/docs/patchouli-basics/text-formatting). 

---
## Feature Writing 

x can be `1`, `2`, `3` or `4` (in the case of [[#`unusual_prehistory mob_entry_features`]])
#### `feature_x.item`
Item ID of a Unusual Prehistory 2 or Vanilla MC item that best represents the feature. 

#### `feature_x.tooltip`
Descriptive blurb about the feature and all relevant uses. Uses minecraft book formatting for text. 
- Start with `§7` and always switch back to this color after keywords 
- Use `§a` before keywords, and `§r` after keywords. 
- Use the [Minecraft Wiki Formatter](https://minecraft.wiki/w/Calculators/Formatting_code_editor) to format with ease, Example;
- "`§7After being §apacified§r, §7Carnotaurus will continue to attack most monsters"` will look like

![[formatting.png|500]]

![[carnotaurus_page_tooltip_2.png]]

#### `feature_x.title_one_line`  & `feature_x.title_two_line`
Title of the blurb. Keep it concise. If it goes over two lines due to the length, use `two_line` instead of `one_line` 
### But what features should I document? 

One small rule - start every feature entry with the mobs name. Or most of them at-least, where applicable. So `Kentrosaurus did this and that...` or `Carnotaurus was this or that...`

The following are examples of features that must/can be included, based on the mob. The wording for some features is standard - make sure you keep it the same across entries.

- Holocene Artifact 
```json
"The artifact used to revive [MOBNAME] is found in/can be obtained by §a[MECHANIC/PLACE/MOB/STRUCTURE]§7"
```
- Holocene Mobs require Breeding feature 
```json
"Being recently-extinct, [MOBNAME] are able to breed after being fed §a[ITEM]§7"
```
- Breeding or general reproduction mechanics ( even cloning, like with Praepusa )
```json
"[MOBNAME] may be bred using §a[ITEM]§7"
```
- Taming
```json
"[MOBNAME] can be tamed using §a[TAME ITEM/S]§7; tamed [MOBNAME] can [...]/be saddled/be saddled and mounted/be mounted/be commanded to attack/etc."
```
- Ability to be bucketed
```json
"[MOBNAME] can be collected and transported using a §aWater Bucket§7"
```
- Drops 
- Special Interactions with the player
- Special Interactions with other mobs
- Other Special Behaviours 
## Renders

![[megalania_render_red.png]]

Location: `unusual_prehistory:textures/gui/paleopedia/images/`

*note for add-on makers - the render should be included under `assets/unusual_prehistory/textures/gui/paleopedia/images`, even in your add-on's resources*

Requirements:
- Image size must be **256x256**.
- The actual render must fit within the top-left **200x200** area. (Red area above)
- Do not crop or cut off the mob.
- Use dynamic poses.
- For large mobs, position the head closer to the camera (See Brachiosaurus, Mosasaurus and Aegirocassis renders).
	- Scale using bilinear scaling if possible
- Renders with multiple species or genera in them have numbering. 
	- Numbers from 0-9 can be found on the aseprite sheet in the paleopedia texture folder 

%%
# Future 
- [ ] add hyperlinks to the book for eras -> specific fossil
- [ ] add hyperlinks to the book for hatching eggs -> egg hatching / gestation process
- [ ] MYA for the era blurb maybe 
%%