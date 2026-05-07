# Changelog

![Banner](https://raw.githubusercontent.com/SkrubbySkrubInAShrub/nordic-souls-PBR/main/.github/NordicSoulsBanner.png)

<p align="center">
  <a href="https://github.com/SkrubbySkrubInAShrub/nordic-souls-PBR/blob/main/README.md">ReadMe</a> |
  <a href="https://www.nexusmods.com/skyrimspecialedition/mods/158119">Nexus</a> |
  <a href="https://discord.com/invite/9cRs3KPyuW">Discord</a> |
  <a href="https://ko-fi.com/geborgen">Ko-fi</a> |
  <a href="https://loadorderlibrary.com/lists/nordic-souls-3-0-1-pbr-edition">Modlist</a> |
  <a href="https://github.com/SkrubbySkrubInAShrub/nordic-souls-PBR/blob/main/GAMEPLAYGUIDE.md">Gameplay Guide</a> |
  <a href="https://github.com/SkrubbySkrubInAShrub/nordic-souls-PBR/blob/main/MODIFICATIONGUIDE.md">Modification Guide</a> |
  <a href="https://github.com/SkrubbySkrubInAShrub/nordic-souls-PBR/blob/main/PERFORMANCEGUIDE.md">Modification Guide</a> |
  <a href="https://github.com/SkrubbySkrubInAShrub/nordic-souls-PBR/blob/main/CHANGELOG.md">Changelog</a> |
  <a href="https://github.com/SkrubbySkrubInAShrub/nordic-souls-PBR/blob/main/FAQ.md">FAQ</a>
</p>

## Contents
- [Improving Visual Quality](#improving-visual-quality)
  - [Shadowmaps](#shadowmaps-cpu--gpu--vram)
  - [Screen Space Shadows (SSS)](#screen-space-shadows-sss-gpu)
  - [Screen Space Global Illumination (SSGI)](#screen-space-global-illumination-ssgi-gpu)
  - [Upscaling](#upscaling-gpu--vram)
  - [High-Resolution Textures](#high-resolution-textures-vram)
- [Improving Performance](#improving-performance)
  - [Screen Space Global Illumination (SSGI)](#screen-space-global-illumination-ssgi-gpu-1)
  - [Upscaling](#upscaling-gpu--vram-1)
  - [Frame Generation (FG)](#frame-generation-fg-vram)
  - [Grass](#grass-gpu--vram)

# Performance Tuning Guide

This guide covers various ways to adjust the balance between visual quality and performance.
Each section is tagged with **GPU**, **CPU**, or **VRAM** to indicate the type of load affected.

---

## Improving Visual Quality

*For when your framerate has headroom and you want to invest it in better visuals.*

### Shadowmaps `[CPU / GPU / VRAM]`

Shadow maps are configured conservatively in this list to preserve performance. Increasing the
shadow map resolution reduces shadow flickering and improves shadow sharpness, particularly in
exterior areas.

To increase shadow map resolution, set the following value in your `SkyrimPrefs.ini` under the
`[Display]` section:

```ini
iShadowMapResolution=4096
```

### Screen Space Shadows (SSS) `[GPU]`

Screen Space Shadows are left at their default settings in this list, but can easily be increased
for better visuals. Higher settings cause small and distant objects to cast longer, more accurate
shadows.

In the CS menu, increase the sample count to **4**.

### Screen Space Global Illumination (SSGI) `[GPU]`

Screen Space Global Illumination is one of the most impactful effects in CS, simulating light
bouncing with a high degree of accuracy. It is also one of the heavier effects, but higher quality
settings result in less flickering and boiling, and more stable lighting overall.

If you have performance headroom, set the quality to **Extreme** in the CS menu.

### Upscaling `[GPU / VRAM]`

CS uses **Quality** upscaling by default. **Native AA** is also available for a sharper and more
stable image.

To enable it, set the upscaling mode to **Native** in the CS menu.

### High-Resolution Textures `[VRAM]`

If you have 16 GB of VRAM or more, upgrading to higher-resolution textures is straightforward.
The following mods ship with multiple resolution options; this list uses lower-resolution variants
by default:

- Tomato's Riften and Ratway
- Tomato's PBR Forts and Dungeons
- Faultier's PBR Skyrim
- Tomato's PBR Whiterun
- Tomato's PBR Solitude
- Vanaheimr Landscapes PBR

Download the higher-resolution version from each mod's page and overwrite the existing files.

---

## Improving Performance

*For when you need to reclaim framerate by reducing visual quality.*

### Screen Space Global Illumination (SSGI) `[GPU]`

SSGI is the heaviest effect in this list. Reducing its quality will introduce more flickering,
boiling, and instability in light bouncing. That said, it offers the most significant performance
gains.

It is recommended to reduce upscaling quality first (see below). If further gains are needed,
reduce SSGI quality to **Low** in the CS menu, or disable the Indirect Lighting (IL) component
entirely and use only Ambient Occlusion (AO) at the lowest quality setting.

### Upscaling `[GPU / VRAM]`

CS uses **Quality** upscaling by default. Lower resolution scales are available and can provide
easy performance gains depending on your native resolution.

Set the upscaling mode to **Balanced** or **Performance** in the CS menu. Adjust the sharpening
settings afterward to compensate for any loss in visual clarity.

### Frame Generation (FG) `[VRAM]`

Frame Generation is enabled by default in CS. While it provides additional frames, it also
increases VRAM usage. If you are experiencing VRAM-related stuttering, disabling FG may help
alleviate it.

### Grass `[GPU / VRAM]`

This list uses **Freak's Floral Fields (FFF)**, a relatively demanding grass mod. Swapping it out
for a lighter alternative can recover a significant amount of performance. A more detailed guide
will be published in the future; the steps below outline the process at a high level.

1. Note the position of FFF in your load order.
2. Install a new grass mod and its requirements.
3. Place the new `.esp` files adjacent to FFF's grass mod entries.
4. Disable FFF. If the new grass mod includes DLC areas (Solstheim, Soul Cairn), disable those
   plugins as well.
5. Disable the **NS PBR - Grass Cache** mod.
6. In MO2, open the **Tools** menu (the puzzle icon) and select **Precache Grass**. This process
   takes at least 20 minutes on fast hardware and over an hour on typical systems. It will crash
   and restart automatically; this is expected behavior.
7. Once complete, a grass folder will be generated in your MO2 overwrite directory. Delete the
   grass folder from the **NS PBR - Grass Cache** mod and replace it with the newly generated one.
   Deleting before copying is faster than overwriting due to the large number of files involved.
8. Re-enable the **NS PBR - Grass Cache** mod.
9. Disable **NS PBR - PG Patcher Output**.
10. Launch **PG Patcher** from MO2. Verify that the instance and profile paths are correct, then
    run the patcher.
11. Re-enable **NS PBR - PG Patcher Output**.
12. In the Plugins tab, ensure the patcher output plugins (`PG_1.esp`, `ParallaxGen.esp`) are
    placed before DynDOLOD.
