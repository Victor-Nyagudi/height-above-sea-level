---
title: "5 Reasons Why Objects in Unity are Still Dark After Baking Lights"
categories: Unity
tags: lighting
excerpt: "Baking lights in Unity doesn't always yield the desired results. One common issue you might run into is objects in your level appearing darker than expected, sometimes even darker than they were before baking lights."
image:
    path: /assets/images/objects_still_dark_article/objects_still_dark_article_thumbnail.jpg
    thumbnail: /assets/images/objects_still_dark_article/objects_still_dark_article_thumbnail.jpg
---

[Baking lights in Unity]({{ site.baseurl }}{% post_url 2025-11-01-baking-lights-in-unity-getting-started %}) doesn't always yield the desired results. One common issue you might run into is objects in your level appearing darker than expected, sometimes even darker than they were before baking lights.

There are multiple reasons why this happens, but there are lighting-related steps you can take to mitigate it.

{% include toc %}

## Incorrect Setup

Before you bake lights, ensure your level's 3D models are properly set up.

Each 3D model in the scene must have the **_Generate Lightmap UVs_ option checked**. This ensures that it influences the lightmap that's placed over the objects after baking.

<figure class="align-center">
  <img src="{{ '/assets/images/how_to_bake_lights_article/generate_lightmap_uv_img.jpg' | absolute_url }}" alt="The 'Generate Lightmap UVs' checkbox in Unity.">
  <figcaption>The <em>Generate Lightmap UVs</em> checkbox.</figcaption>
</figure>

Ensure the 3D model, after dragging it into the scene, thus making it a GameObject, has the _Static_ checkbox checked in the _Inspector_ window. **Objects in a scene must be marked static** to be included in the lighting calculations for direct and indirect lighting.

Ensure the **_Contribute Global Illumination_ checkbox is checked** on the GameObject's _Light_ component so it's part of the lighting calculations when baking lights.

The setup process is explained in further detail in the [_How to Bake Lights in Unity: A Step-by-Step Guide_]({{ site.baseurl }}{% post_url 2025-11-01-how-to-bake-lights-in-unity-guide %}) article.

## Incomplete Light Baking

If, at any moment, you stop or cancel the light baking process, some objects in the scene will be dark because the lighting calculations are incomplete.

You'll need to **let the process run to completion** so the lighting calculations are done for everything in the scene.

You might be tempted to interrupt the process because [baking lights in Unity is taking too long]({{ site.baseurl }}{% post_url 2025-11-01-tips-to-speed-up-light-baking-in-unity %}), but there are settings you can adjust to improve the bake times.

## Poorly Set Up Light Sources

Some objects in your game may still be dark after baking lights because the light intensity is too low or is at 0.

Try **increasing the light intensity in the light source's _Intensity_ setting** in the GameObject's _Light_ component and then bake the lights again. This setting is revealed by unfolding the _Emission_ dropdown.

You should also **ensure the light source's _Color_ setting is set to a bright color** over a dark one that's harder to see.

Some objects in your game's level might be dark because the **light is obstructed by other objects** in the scene.

Move lights around to ensure the desired objects are lit up properly. Alternatively, you can move the objects blocking the light instead.

A common mistake that can result in dark objects is giving the light source **a _Range_ setting that ends at the edge of the area you want to light**.

<figure class="align-center">
  <img src="{{ '/assets/images/how_to_bake_lights_article/point_light_house_img.jpg' | absolute_url }}" alt="A point light in front of a house in Unity.">
  <figcaption>A light range that ends at the level's edge.</figcaption>
</figure>

Light in the real world often travels beyond the area you want to light, so ensure to **extend a light source's range beyond the level's boundaries** to ensure it lights up each object sufficiently.

Lastly, ensure the **_Indirect Multiplier_ option in the GameObject's _Light_ component is set to any number greater than 0**. This setting determines the intensity of indirect lighting in the scene.

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

## Incorrect Light Settings

The settings in the _Lighting_ window determine how the light is baked, and the wrong settings can result in dark objects.

Ensure the **_Baked Global Illumination_ checkbox under the _Mixed Lighting_ dropdown is checked**.

<figure class="align-center">
  <img src="{{ '/assets/images/how_to_bake_lights_article/generate_light_btn_img.jpg' | absolute_url }}" alt="Buttons used to bake lights in Unity surrounded by red squares.">
  <figcaption><em>Baked Global Illumination</em> checkbox in the <em>Lighting</em> window.</figcaption>
</figure>

This setting determines if _Mixed_ and _Realtime_ lights will use baked _Global Illumination_, i.e., allows baking of light from both light types.

You'll most likely use mixed lights in your Unity game, so always keep this setting checked.

Ensure the **_Direct Samples_, _Indirect Samples_, _Environmental Samples_, and _Max Bounces_ have a value of at least 1 or more**.

These settings control the samples used in calculating lighting data and the number of times light bounces in the scene, respectively.

**_Tip:_** Hover over each setting's name in the _Lighting_ window, and a tooltip will pop up, explaining what it's for.
{: .notice--info}

## Forgetting to Rebake Lights

If you move a _Baked_ light type after baking lights to a dark area, the area will remain dark. Adding an Area light to a scene also doesn't light up the level, regardless of its intensity.

This happens because the lighting data hasn't been updated, and the only way to update it is to **bake the lights again** in the _Lighting_ window.

_Realtime_ and _Mixed_ light types will update the lighting as you move the light sources around the scene, but the lighting may still appear off, and some objects might still be dark.

If constantly baking lights sounds tedious, you can check the _Auto Generate_ box at the bottom of the Lighting window to bake lights every time lights are moved, added, or anything affecting lights in the scene happens.

Enabling this option may increase bake times, so use it with discretion.

**_Tip:_** You can restore the level to how it was before baking lights by clicking the arrow next to the _Generate Lighting_ button and selecting _Clear Baked Data_.
{: .notice--info}

## In Closing

These are a few reasons why objects in your Unity game's level might still be dark after baking lights, but if you're still experiencing problems with lighting, the _Unity Lights Troubleshooting Guide_ should help you even further.