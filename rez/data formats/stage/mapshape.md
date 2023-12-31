# Rez MapShape Data Format

## Build 836
- STG01.BIN - map table @ 0x8c32cba8 (0x2cba8 raw) - [info](/rez/notes/836/stg01.html)
- STG02.BIN - map table @ 0x8c34e70c (0x4e70c raw)
- STG03.BIN - map table @ 0x8c32ec8c (0x2ec8c raw)
- STG04.BIN - map table @ 0x8c32eb94 (0x2eb94 raw)
- STG05.BIN - map table @ 0x8c3507f4 (0x507f4 raw)
- STG20.BIN - map table @ 0x8c36ecb0 (0x6ecb0 raw)

## Map Table Layout
22 longs, which are:  
- A pointer to the **Map Data Table**,  
- 21 **Map Parameters**.  

This repeats per mapshape until done.

## Map Data Table Layout
6 longs, which are:
- The total number of objects in the **instance list**,
- The total number of objects in the **model list**,
- The total number of entries in the **group list**,
- The pointer for the map instance list,
- The pointer for the map model list,
- The pointer for the map group list.

## Instance List Layout
11 longs, which are:
1. Object ID (in order of objects in the object list),
2. Unknown (object won't render on certain values),
3. X position,
4. Z position,
5. Y position,
6. X rotation,
7. Z rotation,
8. Y rotation,
9. X scale,
10. Z scale,
11. Y scale.

This repeats for each object defined in the scene object count.

## Model List Layout
12 longs per object, these are:
1. The offset for the **NJCM** model in the stage .NB file,
2. The offset for the model's starting **NMDM** animation in the .NB (optional),
3. A pointer to a table of pointers to 1ST_READ's code (same for each object),
4. The offset for the model's **CPSM** in the .NB,
5. The offset for the model's next **CPSM** in the .NB,
6. Object display mode (00 solid/01 wire)
7. Unknown,
8. Can take an **NMDM** offset and use it constantly but unsure if this is its purpose,
9. Unknown,
10. Unknown,
11. An offset for the model's **NMDM** in the .NB (for constant anim?),
12. The offset for the **NMDM** to override with when the layer is about to transition.

This repeats for every object to be defined in the object list.
  
## Map Parameters
1. Fog type,  
2. Fog near,  
3. Fog far,  
4. Fog colour,  
5. BG colour,  
6. Wire colour,  
7. Camera far,  
8. Camera distance,  
9. Starting pass animation index in STG NB,  
10. Pass loop animation index in STG NB,  
11. Pass doesn't count-up when not 01,  
12. Affects starting map frame number,  
13. Affects which frame the map changes shape on,  
14. Layer transition effect mode,  
15. Layer transition effect buildup time,  
16. Layer transition effect duration,  
17. Unknown,  
18. Fade duration from previous map,  
19. Time until auto advance,  
20. Layer type,  
21. Texture overlay ID.  

### Fog Type
[Demonstration video](https://www.youtube.com/watch?v=XuC3sLRRlJ4)

Rez supports a few different fog modes, but normally only uses mode 1. Mode 2 looks cool but can cause the stage to appear to flicker when in motion.

- 0 - None,
- 1 - Default distant fog,
- 2 - Striped fog,
- 3 - Inverse fog,
- 4 - 4 to 7 are the same as 1.

### Layer Transition Effect Mode
[Demonstration video](https://www.youtube.com/watch?v=tpK9foMSge4)

The layer transition effect is applied when you go to the next layer, and can be further controlled by the buildup time and duration values.

- 0 - None,
- 1 - Fade to white,
- 2 - Invert camera,
- 3 - Screen buffer blur (default),
- 4 - Slide the render output down from top left over screenbuffer screenshot,
- 5 - All values 5 and above will crash.

### Layer Type
The game will let you use values other than 1 and 2 for this, but the other types seem to behave the same as 1 and 2. The game does use 3 sometimes, which is like 1.

- 1 - Gameplay layer, mainflow events will happen.
- 2 - Transition layer, mainflow will be paused. Used for the short animations between gameplay layers.  

---
[Back to Rez Research page](/rez.html)