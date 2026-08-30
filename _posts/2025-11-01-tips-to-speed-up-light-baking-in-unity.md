---
title: "Baking Lights in Unity Taking Too Long? 5 Tips to Speed It Up"
categories: Unity
tags: lighting 3D
excerpt: "Baking lights in Unity can improve your game's performance by doing all the lighting calculations before the game runs, but the process can sometimes take a long time to complete."
image:
    path: /assets/images/baking_lights_taking_long_article/baking_taking_long_thumbnail.jpg
    thumbnail: /assets/images/baking_lights_taking_long_article/baking_taking_long_thumbnail.jpg
date: 2026-08-14
---

[Baking lights in Unity]({{ site.baseurl }}{% post_url 2025-11-01-baking-lights-in-unity-getting-started %}) can improve your game's performance by doing all the lighting calculations before the game runs, but the process can sometimes take a long time to complete.

There are several reasons for the lengthy bake times, which can take hours in some cases, but there are adjustments you can make to prevent this.

This article assumes you know [how to bake lights in Unity]({{ site.baseurl }}{% post_url 2025-11-01-how-to-bake-lights-in-unity-guide %}) and explores the settings you can change to improve bake times.

If you're reading this article on a smaller device, right-click on images (long press on touch devices) and select _Open image in new tab_ to view them at full size.

{% include toc %}

## Progressive Updates

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_taking_long_article/progressive_updates_unchecked_img.jpg' | absolute_url }}" alt="The Progressive Updates checkbox in Unity's Lighting window.">
  <figcaption><em>Progressive Updates</em> checkbox in the <em>Lighting</em> window.</figcaption>
</figure>

The _Progressive Updates_ option in the _Lighting_ window **determines if the lightmapper should prioritize baking what's visible in the scene view**.

Checking the box next to it will update the objects in the scene gradually as the light is baking. Objects will initially appear dark and slowly brighten.

Turning off _Progressive Updates_ alone can significantly reduce light baking times.

My internal tests on a fairly simple scene have shown that **bake times reduced from over 15 minutes to under 2 minutes** when I turned off _Progressive Updates_.

## Lightmapper

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_taking_long_article/lightmapper_option_img.jpg' | absolute_url }}" alt="The Lightmapper dropdown in Unity's Lighting window.">
  <figcaption><em>Lightmapper</em> checkbox in the <em>Lighting</em> window.</figcaption>
</figure>

The _Lightmapper_ option in the _Lighting_ window **determines which system is used to bake lights**.

There are currently two options: _Progressive CPU_ and _Progressive GPU_.

If you're experiencing long bake times using the _Progressive CPU_, switch to the _Progressive GPU_.

The CPU is already handling other tasks, such as running the Unity Editor and any other open programs, so offloading some of the work to the GPU can help speed up bake times since it doesn't normally handle as many tasks as the CPU.

A simple internal test using Windows' built-in _Task Manager_ revealed that baking lights using the _Progressive CPU_ consumed up to 100% of the CPU for an extended period.

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_taking_long_article/progressive_cpu_perf.jpg' | absolute_url }}" alt="Perfomance metrics from Windows Task manager when baking lights using Progressive CPU in Unity.">
  <figcaption>CPU usage when baking lights with <em>Progressive CPU</em>.</figcaption>
</figure>

The _Progressive GPU_ fluctuated between 40% and 100% of the GPU's processes.

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_taking_long_article/progressive_gpu_perf.jpg' | absolute_url }}" alt="Perfomance metrics from Windows Task manager when baking lights using Progressive GPU in Unity.">
  <figcaption>GPU usage when baking lights using <em>Progressive GPU</em>.</figcaption>
</figure>

The difference between the two is that if Unity is using 100% of the CPU, little is left over to perform other tasks on the computer. Even trying to take a screenshot resulted in noticeable delays.

The GPU being under such high loads hardly affects regular computer operations. Furthermore, the load doesn't consistently stay at 100%.

## Samples

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_taking_long_article/lighting_window_samples_img.jpg' | absolute_url }}" alt="The Samples values in Unity's Lighting window.">
  <figcaption>Samples values in the <em>Lighting</em> window.</figcaption>
</figure>

The lightmapper uses samples to determine lighting calculations. There are three samples in the _Lighting_ window:

- **Direct Samples**: Used for direct lighting calculations.

- **Indirect Samples**: Used for indirect lighting (bounced light) calculations.

- **Environment Samples**: Used for environment lighting calculations.

These settings are adjusted in predefined steps, ranging from 1 to 256. Higher values for these settings result in higher-quality lightmaps but increase the time it takes to bake lights in the Unity Game Engine.

Internal tests revealed that a value of 256 for each setting with _Progressive Updates_ turned off is a good starting point for baking lights.

These values, with _Progressive Updates_ turned off and all other settings at their default, resulted in **bake times of roughly one minute** for a modestly detailed scene.

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

## Lightmap Resolution

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_taking_long_article/lightmap_resolution_option_img.jpg' | absolute_url }}" alt="The Lightmap Resolution value in Unity's Lighting window.">
  <figcaption><em>Lightmap Resolution</em> value in the <em>Lighting</em> window.</figcaption>
</figure>

The _Lightmap Resolution_ setting in the _Lighting_ window **determines the lightmap's resolution in texels per unit**.

A higher resolution results in higher-quality lightmaps and improved lighting in your game at the cost of increased bake times.

That being said, you're probably curious what the best lightmap resolution is for your game.

For smaller levels, such as interiors with few objects and simple lighting, a lightmap resolution between 50 and 75 should suffice.

For more realistic lighting, a lightmap resolution above 75 is a good starting point.

You can always lower the lightmap resolution if the time it takes to bake lights becomes too long.

**Tip:** Increasing the lightmap resolution may solve smudges on walls and other artifacts caused by noisy lightmaps.
{: .notice--info}

## Lighting Mode

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_taking_long_article/lightmap_resolution_option_img.jpg' | absolute_url }}" alt="The Lighting Mode dropdown in Unity's Lighting window.">
  <figcaption><em>Lighting Mode</em> option in the <em>Lighting</em> window.</figcaption>
</figure>

Unity has three [lighting modes](https://docs.unity3d.com/6000.0/Documentation/Manual/lighting-mode.html) for mixed lights listed below in order of their effect on performance.

1. Distance Shadowmask & Shadowmask _(most expensive)_

2. Baked Indirect

3. Subtractive _(least expensive)_

The visual fidelity of your game will determine the lighting mode you'll use when baking lights.

**_Distance Shadowmask_** and **_Shadowmask_** offer more realistic lighting but with a higher performance cost. _Distance Shadowmask_ is more costly compared to _Shadowmask_.

**_Baked Indirect_** also offers realistic lighting and realtime shadows. The main difference between it and the _Shadowmask_ lighting modes is that _Baked Indirect_ only casts shadows up to a specified [_Shadow Distance_](https://docs.unity3d.com/6000.0/Documentation/Manual/shadow-distance.html).

**_Subtractive_** offers simple lighting and low-fidelity shadows. This is a great option for low-poly games or games with stylized art.

Using the _Subtractive_ lighting mode may improve the light baking times, but the other modes may not have a big impact if the level's lighting is set up correctly.

## Bonus

- Adding many lights to a level can increase the time it takes to bake lights in Unity. Instead of using multiple light sources, you can **use fewer lights with a longer range and higher intensity** to light up more areas.

- Many [reflection probes]({{ site.baseurl }}{% post_url 2026-08-21-reflection-probes-in-unity %}) may also negatively impact bake times. Use fewer reflection probes in larger, open areas where fewer objects appear in a reflection. **Reducing the reflection probe's resolution also helps**.

- **Too many light probes may affect light baking times**. Use fewer, spaced-out light probes in open areas and more, condensed light probes in areas with many objects where light will often bounce, leading to more complex lighting calculations.

- In some cases, baking lights might be taking too long because of **hardware limitations**, so you'll need parts that are more capable of handling all the lighting computations you require.

## What are the best light settings in Unity?

There's no one-size-fits-all solution to lighting settings in the Unity Game Engine. The best light settings are obtained through adjustments until the game developer is satisfied with the results.

Regardless, if you're unsure of where to start and are looking for some general settings that will **bake lights in under 2 minutes with decent results** for a modestly detailed scene, try the following. All the other settings remain at their default option.

- **Lighting Mode**: Baked Indirect

- **Lightmapper**: Progressive GPU

- **Progressive Updates**: Off

- **Direct Samples**: 256

- **Indirect Samples**: 256

- **Environment Samples**: 256

- **Max Bounces**: 2 or 4

- **Lightmap Resolution**: 50

- **Max Lightmap Size**: 1024

## In Closing

The tests and settings used in this article were on a computer with the following relevant specs:

- **GPU**: NVIDIA GeForce GTX 1660 6GB VRAM

- **CPU**: Ryzen 5 2600

- **RAM**: Dual-channel 16GB

- **OS**: Windows 11

Computers with better hardware will perform better, while those with poorer hardware might experience degraded performance.

If you're still experiencing trouble with lights, read the [_Unity Lights Troubleshooting Guide_]({{ site.baseurl }}{% post_url 2026-08-21-unity-lights-troubleshooting-guide %}) to help you diagnose the problem.