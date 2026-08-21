---
title: "Unity Lights Troubleshooting Guide"
categories: Unity
tags: lighting
excerpt: "Multiple things can go wrong when baking lights in the Unity Game Engine. Some objects may still be dark after baking, some areas may not receive enough light, or shadows may appear off. Before you do any troubleshooting, there are a few concepts you should know before baking lights in Unity."
image:
    path: /assets/images/lights_troubleshooting_article/lights_troubleshooting_article_thumbnail.jpg
    thumbnail: /assets/images/lights_troubleshooting_article/lights_troubleshooting_article_thumbnail.jpg
---

Multiple things can go wrong when baking lights in the Unity Game Engine. Some objects may still be dark after baking, some areas may not receive enough light, or shadows may appear off.

Before you do any troubleshooting, there are a few [concepts you should know before baking lights in Unity]({{ site.baseurl }}{% post_url 2025-11-01-baking-lights-in-unity-getting-started %}), such as lightmaps, light types, and light modes. If you're not familiar with them, the linked article will help you get started.

This article also assumes you know [how to bake lights in Unity]({{ site.baseurl }}{% post_url 2025-11-01-how-to-bake-lights-in-unity-guide %}) and are familiar with the setup process, the _Lighting_ window, and the general workflow associated with adding lights and other GameObjects to a scene.

This introductory video covers these basics, in case you don't know them.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/kOo1CaDdCF0?si=VUJrJdahaGk-Esrj" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

{% include toc %}

## Objects in Unity are still dark after baking lights.

<figure class="align-center">
  <img src="{{ '/assets/images/objects_still_dark_article/objects_still_dark_article_thumbnail.jpg' | absolute_url }}" alt="A front porch with unusually black shadows in Unity.">
  <figcaption>Unusually dark objects in a level.</figcaption>
</figure>

Dark objects in the scene may occur as a result of **improperly setting up the 3D models**.

GameObjects must be marked _Static_ in the _Inspector_ window, the _Contribute Global Illumination_ box must be checked, and the 3D model must have the _Generate Lightmap UVs_ box checked.

The **light sources in the scene may also have an _Intensity_ or _Range_ that's too low to illuminate objects well**. Increasing these values in the _Inspector_ window can help brighten things up.

If you're still having trouble with dark objects, read the [_5 Reasons Why Objects in Unity are Still Dark After Baking Lights_]({{ site.baseurl }}{% post_url 2026-08-21-5-reasons-objects-in-unity-remain-dark-after-baking-lights %}) article, where the issue is discussed in more detail.

## Baking lights in Unity is taking too long.

**High lighting setting values** in the _Lighting_ window can exponentially increase bake times.

The biggest culprit of long bake times is the _Progressive Updates_ setting. Turning this off alone can significantly reduce the time it takes to bake lights.

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_taking_long_article/progressive_updates_unchecked_img.jpg' | absolute_url }}" alt="The Progressive Updates checkbox in Unity's Lighting window.">
  <figcaption>Unchecking this significantly decreases bake times.</figcaption>
</figure>

**Too many lights and reflection probes** in a scene may also increase bake times, so reducing them can improve things.

If you'd like to dive deeper into why lights in Unity are still taking a long time to bake, read the [_Baking Lights in Unity Taking Too Long? 5 Tips to Speed it Up_]({{ site.baseurl }}{% post_url 2025-11-01-tips-to-speed-up-light-baking-in-unity %}) article.

## No reflections after baking lights in Unity.

Reflections in Unity are achieved using reflection probes. Reflection probes take snapshots of the predefined area and store them in a cubemap.

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_get_started_article/reflection_probe_img.jpg' | absolute_url }}" alt="A large reflection probe in front of a house in Unity.">
  <figcaption>The large sphere to the left is a reflection probe.</figcaption>
</figure>

The object's material will first need to be smooth enough to reflect light; otherwise, it won't show any reflections. You can adjust the material's _Smoothness_ in the _Inspector_ window with the material selected.

If you want the smooth objects in your scene to have reflections, **place a reflection probe nearby and adjust the area it covers** based on what you'd like to reflect.

**_Tip:_** Use fewer reflection probes in large, open areas where there's little to show in reflections. More reflection probes work better in tighter areas with corners, but too many can hurt your game's performance.
{: .notice--info}

## Blurry reflections after baking lights in Unity.

If, after placing reflection probes in a scene and baking lights, the reflections appear blurry, you can **adjust the reflection probe's resolution** to sharpen them.

<figure class="align-center">
  <img src="{{ '/assets/images/lights_troubleshooting_article/reflection_probe_resolution_32_img.jpg' | absolute_url }}" alt="Reflection from a 32-unit resolution reflection probe in Unity.">
  <figcaption>Reflection from a 32-unit resolution reflection probe.</figcaption>
</figure>

Select the reflection probe in the scene and, in the _Inspector_ window, unfold the _Cubemap Capture Settings_ dropdown in the _Reflection Probe_ component.

Click the _Resolution_ setting's dropdown and choose a higher number to increase the sharpness of blurry reflections.

<figure class="align-center">
  <img src="{{ '/assets/images/lights_troubleshooting_article/reflection_probe_resolution_256_img.jpg' | absolute_url }}" alt="Reflection from a 256-unit resolution reflection probe in Unity.">
  <figcaption>Reflection from a 256-unit resolution reflection probe.</figcaption>
</figure>

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

## Reflections in Unity are not moving.

Reflection probes are set to _Baked_ by default. **Baked reflection probes result in static reflections**.

If you want dynamic reflections that update as objects move in the Unity player, you'll need to set the reflection probe's _Type_ to _Realtime_ in the _Inspector_ window.

## Shadows in Unity are blurry/too soft/not crisp after baking lights.

Setting a light source's mode to _Baked_ results in its light only showing after baking, and it **casts softer shadows**.

<figure class="align-center">
  <img src="{{ '/assets/images/lights_troubleshooting_article/soft_shadows_img.jpg' | absolute_url }}" alt="Dark interior of a blue house in Unity.">
  <figcaption>Blurry shadows from a baked light.</figcaption>
</figure>

You'll need to use either _Realtime_ or _Mixed_ lights to cast sharper shadows.

You can still cast soft shadows with _Realtime_ or _Mixed_ lights by changing the _Shadow Type_ in the GameObject's _Light_ component in the _Inspector_ window under the _Shadows_ dropdown.

## No shadows as objects move in Unity.

Light sources whose mode is set to _Baked_ cast static shadows. Objects that pass in the areas they light up will either not cast shadows, or the shadows they cast initially won't update as the objects move.

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_get_started_article/baked_light_static_shadow.gif' | absolute_url }}" alt="A grey cube with a static shadow moving back and forth in Unity.">
  <figcaption>Static shadow from a baked light.</figcaption>
</figure>

**You'll need lights whose mode is set to _Realtime_ or _Mixed_** to cast shadows on moving objects in the area they light up.

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_get_started_article/realtime_light_dynamic_shadow.gif' | absolute_url }}" alt="A grey cube with a dynamic shadow moving back and forth in Unity.">
  <figcaption>Dynamic shadow from a <em>Realtime</em>/<em>Mixed</em> light.</figcaption>
</figure>

You can update a light source's mode in the _Inspector_ window under the _General_ dropdown's _Mode_ setting of the _Light_ component.

## Console errors in Unity after baking lights.

### Not enough GPU memory to fit an entire lightmap.

```
Not enough GPU memory to fit an entire lightmap, disabling progressive updates.
Available GPU memory : 499.0 MB
```

You might encounter this error after consecutively baking light maps in Unity multiple times with the _Progressive Updates_ box checked.

If you check your GPU usage using Windows' built-in _Task Manager_ or _Xbox Game Bar_ overlay, you'll see that the VRAM usage is high - possibly around 90%.

You should see something similar in the _System Monitor_ on Linux devices or _Activity Monitor_ on Apple Mac devices.

**_Tip:_** Press <kbd>Windows Key</kbd> + <kbd>G</kbd> to open the _Xbox Game Bar_ overlay on Windows devices. It has a small window displaying the performance statistics of the CPU, GPU, VRAM, and RAM.
{: .notice--info}

**Uncheck the _Progressive Updates_ option** in the _Lighting_ window to prevent this error. If you need the option checked, closing and re-opening Unity should free up the VRAM.

### Overlapping UV's error.

```
There are 11 objects in the Scene with overlapping UV's.
Please see the details list below or use the 'UV Overlap' visualization mode
in the Scene View or Lightmaps in Lighting Settings for more information.
```

This error occurs due to **overlapping areas in the geometry** affecting the lightmap output.

You can inspect which parts overlap by clicking the _Draw Mode_ dropdown at the top right of the _Scene_ window (usually the first one from the left) and selecting _UV Overlap_. **Overlapping UVs are highlighted in red**.

<figure class="align-center">
  <img src="{{ '/assets/images/lights_troubleshooting_article/lights_troubleshooting_article_thumbnail.jpg' | absolute_url }}" alt="UV Overlap debug mode in Unity.">
  <figcaption><em>UV Overlap</em> debug mode.</figcaption>
</figure>

You could try increasing the _Lightmap Resolution_ in the _Lighting_ window to fix this, but the best option would be to **fix the overlapping UVs in Blender or other 3D modeling software** if possible.

If you don't have the necessary skills, reach out to the asset's creator and ask for assistance with the overlapping UVs.

**_Tip:_** You can use the other options under the _Baked Global Illumination_ dropdown in the scene's _Draw Mode_ to debug lights.
{: .notice--info}

## Light passes through non-existent cracks and spaces in Unity.

Light that bleeds through non-existent spaces in the game's geometry is called a light leak.

<figure class="align-center">
  <img src="{{ '/assets/images/lights_troubleshooting_article/light_leaks_img.png' | absolute_url }}" alt="A red sphere and yellow square lit up in a house in Unity.">
    <figcaption>Light leaking from non-existent spaces.</figcaption>
</figure>

The most likely culprit for light leaks is issues with the 3D model rather than bad lighting settings.

If increasing the _Lightmap Resolution_ and samples in the _Inspector_ window yields no results, it's best to inform the asset's creator about the light leaks and where they occur so they can update it in Blender or the 3D software used to create the asset.

## Transparent objects in Unity appear solid.

<figure class="align-center">
  <img src="{{ '/assets/images/lights_troubleshooting_article/opaque_windows_img.png' | absolute_url }}" alt="A muddy white pickup truck with black windows in Unity.">
    <figcaption>Opaque windows on a pickup truck.</figcaption>
</figure>

If a transparent object that's supposed to let light pass through it appears opaque, **check the object's material in the _Inspector_ window**.

You'll find the material in the GameObject's _Mesh Renderer_ component under the _Materials_ dropdown.

Ensure the material's _Surface Type_ is set to _Transparent_. Click the color bar in the _Base Map_ setting and adjust the alpha (A) channel. An alpha channel of 0 is fully transparent, while 255 is fully opaque.

<figure class="align-center">
  <img src="{{ '/assets/images/lights_troubleshooting_article/transparent_window_img.png' | absolute_url }}" alt="A muddy white pickup truck with transparent windows in Unity.">
    <figcaption>Transparent windows on a pickup truck.</figcaption>
</figure>

## Area lights in Unity don't light up the scene.

Light from **_Area_ lights must be baked** for it to affect the scene.

If you make any changes to an _Area_ light, such as increasing its _Intensity_ or _Range_, you'll need to bake the lights again to see their effect.

**_Tip:_** An _Area_ light's mode is permanently set to _Baked_ for performance reasons. You can't change it to _Realtime_ or _Mixed_.
{: .notice--info}

## How do I make objects glow in Unity?

<figure class="align-center">
  <img src="{{ '/assets/images/lights_troubleshooting_article/glowing_objects_img.png' | absolute_url }}" alt="Glowing objects behind an old house in Unity.">
    <figcaption>Glowing objects behind the house.</figcaption>
</figure>

The glowing effect can be achieved through [post-processing](https://docs.unity3d.com/Packages/com.unity.postprocessing@3.5/manual/index.html). Post-processing is similar to adding filters to an image.

It lets you adjust your game's color contrast, exposure, or even perform some color correction.

The post-processing effect that makes objects glow in Unity is called **_Bloom_**. You can also adjust the intensity and threshold of the glow in your scene.

## The scene is still bright after removing/disabling all lights.

If, after removing or disabling lights in a scene, the scene remains bright, you should **bake the lights again to update the lightmap**.

Alternatively, you can **clear the baked light data** to restore the scene to its previous state before baking any lights.

Remember that **some skyboxes have a sun or moon** that also emits light onto objects in the scene. Changing the skybox or removing it and then rebaking lights can help eliminate any unwanted illumination.

## Smudges on walls and discolorations after baking lights in Unity.

Smudges and other discolorations on object surfaces are signs of noisy lightmaps.

<figure class="align-center">
  <img src="{{ '/assets/images/lights_troubleshooting_article/wall_smudges_img.jpg' | absolute_url }}" alt="Dark blue house interior in Unity.">
    <figcaption>Non-uniform blue color on the walls.</figcaption>
</figure>

Try moving the nearby lights and rebake the light. If the spots disappear, the light may have been positioned incorrectly, such as too close to or overlapping geometry.

If that doesn't fix the issue, try **increasing the _Lightmap Resolution_** in the _Lighting_ window to a higher value, like 100.

Higher values for _Direct Samples_, _Indirect Samples_, or _Environment Samples_ can sometimes result in clearer lightmaps too.

## Bonus

**Faulty scripts** controlling lights can also cause problems in Unity. For example, a script that's supposed to increase a light source's intensity may end up decreasing it to 0 if it's written poorly.

If changing light settings yields no results, it's worth it to [debug](https://youtu.be/akyMZwL3bcs?si=I0L86fI1kbzNWoV6) any scripts attached to a light source to ensure everything's working as intended.