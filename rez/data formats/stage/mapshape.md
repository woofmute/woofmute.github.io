# Rez MapShape Data Format

## 836
### STG01.bin - map table @ 0x8c32cba8 (0x2cba8 raw)

## Map Table Format
22 longs, which are:  
  
- A pointer to the **Map Data Table**,  
- 21 **Map Parameters**.  
  
This repeats per mapshape until done.
  
## Map Parameters
1. Fog type,  
2. Fog near,  
3. Fog far,  
4. Fog colour,  
5. BG colour,  
6. Wire colour,  
7. Camera angle,  
8. Camera distance,  
9. Starting pass speed,  
10. Pass speed from loop,  
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
