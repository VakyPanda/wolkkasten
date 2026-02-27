Hi. You want to write entries for the UP-2 patchouli book. 
Written by @vakypanda on discord. Ping me for questions. 
## Overview

- **Entry** - a json file, containing all the information for the specific mob's entry in the book
- **Page** - the page on the book, it has set templates that can be assigned at the highest level of the entry
- **Variables** - the values you will be editing for each given creature. Some variables have to be left blank in certain cases. You should remove that line entirely.

The guide is to make sure formatting is kept consistent. I've tried to make the process of adding new entries super easy, so the json file youll see for any mob's entry is very short and requires some basic information to be filled.

All Entries are located under `src/main/resources/assets/unusual_prehistory/patchouli_books/paleopedia/en_us/entries/mobs`. Best you clone the github repository for the indev update before you start. If not just write the jsons down seperately, but remember that can make it unnecessarily difficult to weed out issues. Optionally get a beta from someone and make a resourcepack (or ask me and ill make it for you) and use that to edit the entries.  
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
      "image_tooltip": "Late Cretaceous abelisaur with a short, deep skull and a massive pair of horns that give it its name"  
    },  
    {  
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
  
      "feature_2.item": "minecraft:golden_apple",  
      "feature_2.tooltip": "§7After being §apacified§r, §7Carnotaurus will continue to attack most monsters",  
      "feature_2.title_one_line": "Bodyguard!",  
      "feature_2.title_two_line": ""  
    }  
  ]  
}
```

Here's the json for the carnotaurus, subject to change. Let's walk through it step-by-step. 

1. `name` is the name displayed on the Category page. This is the name you see when you look at all the dinosaur pages under the "mobs" section in the book. **Title Case**.
2. `icon` is the icon of the mob. These should be located under `"unusual_prehistory:textures/gui/paleopedia/icons/[mob].png` (eg: `carnotarus.png` ). If an icon is missing, ping and ask me or someone else on discord. ALL the icons are located on the Barl-Inc-Assets github, alongside a aseprite sheet of the icons that may be missing. *This is a change I (vaky) made as of 2.0 cause I think its a bit cleaner than the egg sprites and also showcases the era colors better. 
3. `category` do not change this, should always be `unusual_prehistory:mobs`
4. `advancement` self-explanatory, will just be eg; `unusual_prehistory:revive_dunkleosteus`
5. `extra_recipe_mappings` gives all the items that should link to this page in the patchouli book. It generally contains the egg, fossil and spawn egg of a mob. *The number is the page number, 0 means first page, 1 means second, and so forth. Keep it as 0.* 
```json
"extra_recipe_mappings": {  
    "unusual_prehistory:fury_fossil": 0,  
    "unusual_prehistory:carnotaurus_egg": 0,  
    "unusual_prehistory:carnotaurus_spawn_egg": 0  
  },  
```

This is all information for organising and displaying the page within the context of the patchouli book. Next is the actual entry, under `pages`. Each page has a `type`, and there are 3-4 types you can use for a mob entry:

1. `unusual_prehistory:mob_entry_1` this is the page that contains the render 
	1. `display_name` is identical to `name`
	2. `id` is the id of the mob, which you can see in-game using `F3+H`. **OMIT THE `unusual_prehistory:` PART**. Eg; `unusual_prehistory:lobe_finned_fish` becomes `lobe_finned_fish`
	3. `flavor text` english translation of the animals name. If there is none (eg; Lobe Finned Fish) **remove this line entirely**.
	4. `fossil_item` self explanatory. Use `F3+H` to see the fossil item id in-game. Have JEI installed if you do not know what fossil makes what dinosaur - the transmogrifier recipes are JEI compatible. In this case, do NOT leave out `unusual_prehistory:` from the name
	5. `egg_item` same as `fossil_item` but for eggs instead
	6. `variant_key` part of the tooltip that appears when you hover over the render, for numbered renders. Capitalised names for Genera, simple names for species. Each is seperated by the number on the render ( see the renders section ) 
		Dunkleosteus variants are species:
		`"variant_key": "1 raveri 2 marsaisi 3 terrelli",`
		Lobe Finned Fish variants are genera 
		`"variant_key": "1 Allenypterus 2 Scaumenacia 3 Laccognathus 4 Eusthenopteron 5 Gooloongia",`
	7. `image_tooltip` this is a small blurb that appears when you hover your mouse over the animals render. Feel free to write what you want, but keep it brief yet descriptive, and fun! 
	8. See the section below **On Renders** to understand how the renders in the assets should be structured if you're doing those too. 

2. `unusual_prehistory:mob_entry_2` this is the page that contains info on era, behaviour and the first feature blurbs
	1. `era_image` the mod will come with built in eras as follows; 
		1. `early`, `mid`, and `late` for
		2. `cambrian`, `ordovician`, `silurian`, `devonian`, `carboniferous`, `permian` `triassic`, `jurassic`, `cretaceous`, `cenozoic`. You can therefore build `late_cretaceous`, `early_cenozoic` etc. 
		3. `precambrian` and `holocene` will have one image each ( no late and early )
		4. ON TOP OF THIS we will probably have to do a few custom era images for certain mobs that cross over multiple eras. You'll have to look up their texture in the eras folder, it is the same as their name (so `carnotaurus.png`. If this texture doesn't exist, ask me to make it (@vakypanda). You can also look at the aseprite file within the same folder and see how the multi-era files are set-up and do it yourself - its up to you!  `unusual_prehistory:textures/gui/paleopedia/eras/`
	2. `era_tooltip_period` refers to the tooltip you see when you hover over the era image. There are two possibilities;
		1. eg; `Late Cretaceous Period` or `Holocene Epoch` - one period mobs
		2. eg; `Late Cretaceous into the Early Cenozoic Period` - two or more period mobs. Earliest to latest period. Take note of **"into the"** here. 
	3. `temperament.temperament_type` can be `hostile`, `passive`, `neutral
	4. `clone.clone_type`, `clone.clone_tooltip_heading` and `clone.clone_tooltip` are a set of values which have fixed formatting and **MUST BE COPIED FROM [HERE](#COPY-AND-PASTE)**. The 'clone' values just mean how the mob is hatched - via egg, embryo, aquatic egg, etc
	5. The same goes for `activity.activity_type` and `activity.activity_tooltip`, which go over the daily activity of the specific mob (diurnal, nocturnal, etc)

[[#Feature Writing]] has it's own separate section 
## Feature Writing 

1. `feature_x.item` where x can be `1`, `2` or `3`. These feature-related variables dictate the little feature blurbs and what they show. `feature_x_item` can contain a vanilla or UP2 item id, grabbed the same way as the fossil and egg items were. The item should be related to what the feature being described is, ideally the item is directly related to the mob and if not it is related by concept or feel. 
2. `feature_x.tooltip` should be a descriptive blurb about the feature and all its relevant uses. The entire section is formatted gray and you MUST use `§a` before any key-words or items or mob names - this will highlight the word in *green*. After the key-word, add `§7` to turn the text following it back to gray. Example; "`§7After being §apacified§r, §7Carnotaurus will continue to attack most monsters"`. 
![[carnotaurus_page_tooltip_1.png]]
![[carnotaurus_page_tooltip_2.png]]

3. `feature_x.one_line` this is the 'title' of the blurb - its short and punchy. Can be monotone if you want - "Breeding" for example. Up to you. 
4. `feature_x.two_line` the difference between this and the above is simply splitting the title into two lines instead of one. If you find your `one_line` title is getting too long and being automatically moved to the next line, move your title here and leave `one_line` empty. This is because the `two_line` title has specific alignment to make it look good. [[#But what features should I document?]]
#### But what features should I document? 
1. Breeding is an important one - Holocene mobs have it
2. Drops or interactions 
3. Special Behaviours 
## On Renders
- When renders are being put in the `unusual_prehistory:textures/gui/paleopedia/images/` folder, there are a few things to remember
	1. The image must be `256x256` in dimension
	2. The actual **RENDER** must be WITHIN THE TOP LEFT `200x200` pixels. This is MANDATORY or else your render WILL get cut off;

		![[megalania_render_red.png]]

		(*The red area represents the area the render can actually fit into, which is 200x200 pixels.*)
	3. Try to take renders in a dynamic pose. Since there is a lot of compression at this size, for big mobs (like a sauropod or something like aegirocassis) I'd suggest taking the render such that the head of the mob is quite large and near the camera, while the rest of the mob is in the distance but distorted and smaller. Try to not cut off mobs, it clashes with the style of the entries. 
	4. some mobs have species variants ( eg; Lobe finned fish ). Look at their render in [the GitHub Assets](https://github.com/platypushasnohat/Unusual-Prehistory-2/tree/main/src/main/resources/assets/unusual_prehistory/textures/gui/paleopedia) if you have access to those - theyre numbered! These "numbers" go in the `variant_key` section of the entry. 

# Copy-And-Paste 
## Cloning 
Placeable Egg (mostly for reptiles and non-avian dinosaurs)
```json
"clone.clone_type": "nest_egg",  
"clone.clone_tooltip_heading": "Nest Egg",  
"clone.clone_tooltip": "Egg must be placed down to hatch",
```

Throwable Egg (for avians mostly)
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

## Activity
```json
"activity.activity_type": "diurnal",  
"activity.activity_tooltip": "Active during the day"
```

```json
"activity.activity_type": "nocturnal",  
"activity.activity_tooltip": "Active during the night"
```

```json
"activity.activity_type": "cathemeral",  
"activity.activity_tooltip": "Active randomly throughout the day or based on specific factors"
```

```json
"activity.activity_type": "sleepless",  
"activity.activity_tooltip": "Does not sleep"
```

```json
"activity.activity_type": "crepuscular",  
"activity.activity_tooltip": "Active at dusk or dawn"
```

%%
# Future 
- [ ] add hyperlinks to the book for eras -> specific fossil
- [ ] add hyperlinks to the book for hatching eggs -> egg hatching / gestation process
- [ ] MYA for the era blurb maybe 
%%