# Beastmaster Rework (BG2:EE)

A replacement for the vanilla **Beast Master** ranger kit, inspired by Dota's Beastmaster: an axe-wielding ranger with **one strong pet that scales to the end of the game** instead of a pile of fragile summons, plus a short-lived **HP buffer** as an alternative to stacking damage resistance.

## Requirements
- **Baldur's Gate II: Enhanced Edition** (v2.6) or **EET**
- **WeiDU** v247 or newer
- A **new character**: existing Beast Masters won't retroactively gain the new level-1 abilities
- Install **after** SCS and any mods that add or change armor, items or kits. The plate restriction is built from the armors present at install time.

## Installation
1. Copy the `BMKIT` folder into your game folder.
2. Install `BMKIT/setup-BMKIT.tp2` with WeiDU, the same way as any other mod. For example, copy the WeiDU binary into the game folder as `setup-BMKIT` (or `setup-BMKIT.exe`) and run it.
3. To uninstall, run the same setup again and choose uninstall. Everything below is reverted.

## Kit description (as shown in game)
```
BEASTMASTER: Beastmasters are rangers who have turned their backs on towns for good. Many are outcasts or of mixed blood, welcome in no hall and content to keep it that way, and they are found wherever the roads give out, from the High Forest to the Cloud Peaks. In place of companions they keep the loyalty of beasts: a great razorback cat that comes when called, and hawks that gather overhead when steel is drawn. A Beastmaster fights with the axe, the tool of someone who has lived by it, and has little use for the weapons of temples and town militias.

Advantages:
– May achieve High Mastery (four slots) in Axes.
– 1st level: May use Summon Razorback once per day. Gains one additional use at levels 4, 8, 12, 16, and 20.

SUMMON RAZORBACK: The Beastmaster calls a razorback to fight alongside the party for 6 turns. Only one razorback will answer at a time; calling again dismisses the one already present. The razorback is immune to Death Spell and Death Fog, and grows stronger as the Beastmaster gains levels. Casting time: 6.
  Level 1: 24 HP, AC 4, THAC0 14, 2 attacks per round for 1d6+1 slashing damage (strikes as a +1 weapon)
  Level 5: 56 HP, AC 2, THAC0 10, 3 attacks per round for 1d8+2 (strikes as +2)
  Level 11: 110 HP, AC -1, THAC0 5, 3 attacks per round for 1d10+4 (strikes as +3), 15% resistance to physical damage, 25% resistance to fire, cold, electricity, and acid
  Level 17: 160 HP, AC -4, THAC0 1, 4 attacks per round for 2d6+6 (strikes as +4), 30% resistance to physical damage, 50% resistance to fire, cold, electricity, and acid

– 6th level: May use Avian Guardians once per day.

AVIAN GUARDIANS: A flock of spectral hawks wheels around the Beastmaster, throwing themselves in the way of every blow. For 4 rounds the Beastmaster gains temporary Hit Points based on current maximum Hit Points, and all damage is taken from these first. The temporary Hit Points fade when the effect ends. Casting is instantaneous.
  Level 6: 80% of maximum Hit Points
  Level 12: 90% of maximum Hit Points
  Level 18: 100% of maximum Hit Points

– May select the Call of the Wild high-level ability.

CALL OF THE WILD: Summon Razorback now calls two razorbacks instead of one. Calling again dismisses both. This ability may be taken only once.

Disadvantages:
– May not use blunt weapons (maces, clubs, flails, morning stars, war hammers, or quarterstaves).
– May not wear armor heavier than splint mail.
– May not dual-class.
– Casting time of spells is increased by 1. Innate abilities are not affected.
```

## How it works
- **Summon Razorback**: an innate spell with four creature tiers (levels 1/5/11/17), based on the Spirit Lion with spirit visuals. Claws are magical weapons from +1 to +4. The razorback is immune to Death Spell (including SCS's sub-spells) and Death Fog. Base casting time is 5, which becomes 6 with the kit's casting penalty.
- **One pack at a time, no cheese**: every cast resets a global token. New razorbacks claim a fresh ID, and any razorback holding an old ID removes itself as soon as its script runs, even one left off-screen or in another area.
- **Avian Guardians**: instant, can't be interrupted or dispelled. It adds temporary max HP equal to 80/90/100% of your *current* max HP, calculated in 10-HP steps, so Constitution boosts count. It lasts 4 rounds; when it expires, the bonus is removed and any damage taken while it was up comes out of the bonus first. The visual is a sepia Globe of Blades with no damaging effect, and it has its own portrait icon.
- **Call of the Wild** (HLA, once): permanently sets a spell state that makes each Summon Razorback cast call a second razorback.
- **Restrictions**: blunt weapons are blocked by item type. Plate and full plate get a "not usable by Beastmaster" effect, so they show red. No dual-classing. Spells cast 1 speed factor slower; innates are affected too, except Avian Guardians, which is instant.
- **Stock perks removed**: +15% stealth, Find Familiar, Animal Summoning I–III. Normal ranger abilities stay.
- **Party AI**: razorbacks follow the party AI toggle. With AI off, they only act when ordered.

## What it changes
Only the **BEASTMASTER** rows and columns of shared tables (`kitlist`, `clastext`, `weapprof`, `dualclas`, `luabbr`), the kit's own name and description strings, and one effect added to each plate/full-plate armor. It also adds one row each to `splprot.2da` and `statdesc.2da` and one spell state to `splstate.ids`. All new resources use the `BMK` prefix.

## Credits
- Built with WeiDU and documentation from the [IESDP](https://gibberlings3.github.io/iesdp/).
- Kit concept inspired by Beastmaster from Dota.
- Baldur's Gate II: Enhanced Edition is © Beamdog / Wizards of the Coast. This is a fan mod.
