Hi. You want to write entries for the UP2 patchouli book. 
Written by @vakypanda on discord. Ping me for questions. 
# Overview
The guide is to make sure formatting is kept consistent. I've tried to make the process of adding new entries super easy, so the json file youll see for any mob's entry is very short and requires some basic information to be filled.

Some variables have to be left blank in certain cases. Here's what that looks like;

```json
"empty_variable_of_some_kind": "",  
```


Entries are located under `src/main/resources/assets/unusual_prehistory/patchouli_books/paleopedia/en_us/entries/mobs`. Best you clone the github repository for the indev update before you start. If not just write the jsons down seperately, but remember that can make it unnecessarily difficult to weed out issues. Optionally get a beta from someone and make a resourcepack (or ask me and ill make it for you) and use that to edit the entries. Variables are the parts of the entry youll be changing for your page. 
# Variables

![[2026-02-10_01.51.26.png]]

```json
{  
  "name": "Carnotaurus",  
  "icon": "unusual_prehistory:textures/gui/paleopedia/icons/carnotaurus.png",  
  "category": "unusual_prehistory:mobs",  
  "advancement": "unusual_prehistory:revive_carnotaurus",  
  "pages": [  
    {  
      "type": "unusual_prehistory:mob_entry_1",  
      "display_name": "Carnotaurus",  
      "id": "carnotaurus",  
      "flavor_text": "meat-eating-bull",  
      "fossil_item": "unusual_prehistory:fury_fossil",  
      "egg_item": "unusual_prehistory:carnotaurus_egg",  
      "image_tooltip": "§7A large animal that existed long ago and was really really mad."  
    },  
    {  
      "type": "unusual_prehistory:mob_entry_2",  
      "era_image": "unusual_prehistory:textures/gui/paleopedia/eras/late_cretaceous.png",  
      "era_tooltip_period": "Late Cretaceous Period",  
      "temperament": "hostile",  
  
      "feature_1_item": "minecraft:barrier",  
      "feature_1_tooltip": "§7Do not §fthe §7Carnotaurus",  
      "feature_1_title_one_line": "Do not.",  
      "feature_1_title_two_line": "",  
  
      "feature_2_item": "minecraft:mutton",  
      "feature_2_tooltip": "§7Carnotaurus loves eating §feverythhing",  
      "feature_2_title_one_line": "Feeding Time!",  
      "feature_2_title_two_line": "",  
  
      "feature_3_item": "minecraft:bone",  
      "feature_3_tooltip": "§7Carnotaurus is §fvery angry §7and §fwould like to eat you lowkey",  
      "feature_3_title_one_line": "",  
      "feature_3_title_two_line": "DESTROY ALL HUMANS!"  
    }  
  ]  
}
```

Here's the json for the carnotaurus, subject to change. Let's walk through it step-by-step. 

1. `name` is the name displayed on the Category page. This is the name you see when you look at all the dinosaur pages under the "mobs" section in the book. **Title Case**.
2. `icon` is the icon of the mob. These should be located under `"unusual_prehistory:textures/gui/paleopedia/icons/[mob].png` (eg: `carnotarus.png` ). If an icon is missing, ping and ask me or someone else on discord. ALL the icons are located on the Barl-Inc-Assets github, alongside a aseprite sheet of the icons that may be missing. *This is a change I (vaky) made as of 2.0 cause I think its a bit cleaner than the egg sprites and also showcases the era colors better. 
3. `category` do not change this, should always be `unusual_prehistory:mobs`
4. `advancement` self-explanatory, will just be eg; `unusual_prehistory:revive_mammoth`

This is all information for organising and displaying the page within the context of the patchouli book ^ next is the actual entry, under `pages`. Each page has a `type`, and there are 3-4 types you can use for a mob entry:

1. `unusual_prehistory:mob_entry_1` this is the page that contains the render 
	1. `display_name` is identical to `name`
	2. `id` is the id of the mob, which you can see in-game using `F3+H`. **OMIT THE `unusual_prehistory:` PART**. Eg; `unusual_prehistory:lobe_finned_fish` becomes `lobe_finned_fish`
	3. `flavor text` english translation of the animals name. If there is none (eg; Lobe Finned Fish) just leave this variable blank.
	4. `fossil_item` self explanatory. Use `F3+H` to see the fossil item id ingame. Have JEI installed if you do not know what fossil makes what dinosaur - the transmogrifier recipes are JEI compatible. In this case, do NOT leave out `unusual_prehistory:` from the name
	5. `egg_item` same as `fossil_item` but for eggs instead
	6. `image_tooltip` this is a small blurb that appears when you hover your mouse over the animals render. Feel free to write what you want, but keep it brief yet descriptive, and fun! 
	7. See the section below **On Renders** to understand how the renders in the assets should be structured if you're doing those too. 

2. `unusual_prehistory:mob_entry_2` this is the page that contains info on era, behaviour and the first feature blurbs
	1. `era_image` the mod will come with built in eras as follows; 
		1. `early`, `mid`, and `late` for
		2. `cambrian`, `paleozoic`, `triassic`, `jurassic`, `cretaceous`, `cenozoic`. You can therefore build `late_cretaceous`, `early_cenozoic` etc. 
		3. `precambrian` and `holocene` will have one image each
		4. ON TOP OF THIS we will probably have to do a few custom era images for certain mobs that cross over multiple eras. You'll have to look up their texture in the eras folder. `unusual_prehistory:textures/gui/paleopedia/eras/`
	2. `era_tooltip_period` refers to the tooltip you see when you hover over the era image. There are two possibilities;
		1. eg; `Late Cretaceous Period`, `Holocene Epoch` - one period mobs
		2. eg; `Late Cretaceous Period into the Early Cenozoic Period` - two or more period mobs. Earliest to latest period. Take note of "into the" here. 
	3. `temperament` can be `hostile`, `passive`, `neutral`
	4. `feature_x_item` where x can be `1`, `2` or `3`. These feature-related variables dictate the little feature blurbs and what they show. `feature_x_item` can contain a vanilla or UP2 item id, grabbed the same way as the fossil and egg items were. The item should be related to what the feature being described is, ideally the item is directly related to the mob and if not it is related by concept or feel. 
	5. `feature_x_tooltip` should be a descriptive blurb about the feature and all its relevant uses. The entire section is formatted gray and you MUST use `§f` before any key-words or items or mob names - this will highlight the word in *white*. After the key-word, add `§7` to turn the text following it back to gray. Example; `Carnotaurus can drop a §fCarnotaurus Horn §7upon being slain. 
![[2026-02-10_01.55.29.png]]
	6. `feature_x_one_line` this is the 'title' of the blurb - its short and punchy. Can be monotone if you want - "Breeding" for example. Up to you. 
	7. `feature_x_two_line` the difference between this and the above is simply splitting the title into two lines instead of one. If you find your `one_line` title is getting too long and being automatically moved to the next line, move your title here and leave `one_line` empty. This is because the `two_line` title has specific alignment to make it look good. 

#### But what features should I document? 
1. Breeding is an important one - Holocene mobs have it
2. Drops or interactions 
3. Special Behaviours 

##### In the future (soon) I plan to also include two more types of pages. 
- The first will be a full page of feature slots, in-case you need more space than the basic one can provide
- The second will be a full page of text and a header, for fun facts and detailed descriptions about the real animal. Will be included at the very end of any entry, for curious players to learn something! 
	
#### On Renders
- When renders are being put in the `unusual_prehistory:textures/gui/paleopedia/images/` folder, there are a few things to remember
	1. The image must be `256x256` in dimension
	2. The actual **RENDER** must be WITHIN THE TOP LEFT `200x200` pixels. This is MANDATORY or else your render WILL get cut off;

		![[Pasted image 20260210002556.png]]
		*The red area represents the area the render can actually fit into, which is 200x200 pixels.*
	3. Try to take renders in a dynamic pose. Since there is a lot of compression at this size, for big mobs (like a sauropod or an icthyosaur) I'd suggest taking the render such that the head of the mob is quite large and near the camera, while the rest of the mob is in the distance but distorted and smaller. Try to not cut off mobs, it clashes with the style of the entries. 


# Future 
- add the text and feature pages
- add hyperlinks to the book for eras -> specific fossil
- add hyperlinks to the book for hatching eggs -> egg hatching / gestation process
- add parallel icon to temperament for;
	- `Eggs must be &fThrown to hatch`
	- `Eggs must be &fPlaced on Water to hatch`
	- `Eggs must be &fPlaced down to hatch`
	- `Embryos must be &fPlaced in Organic Ooze to gestate.`
- add parallel icon for diet?
	- `Herbivorous`
	- `Carnivore`
	- `Omnivore`
	- `Piscivore`
	- `Insectivore`
	- `Nectarivore`
	- `Scavenger`
	- `Planktivore`
- add parallel icon for activity?
	- `Diurnal`
	- `Nocturnal`
	- `Crepuscular`
	- `Cathemeral`
- MYA for the era blurb maybe 
- diorama of symbols over the era blurb instead of the clock 
	- or a bigger clock. 