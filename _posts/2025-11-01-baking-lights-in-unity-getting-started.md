---
title: "Baking Lights in Unity: Everything You Need to Know to Get Started"
categories: Unity
tags: lighting
excerpt: "Different lights in a scene can create a varying atmosphere. These scenarios can be accomplished using the correct lights in the Unity Game Engine, and an important concept when using Unity lights is baking."
image:
    path: /assets/images/baking_lights_get_started_article/baking_lights_getting_started_thumbnail.jpg
    thumbnail: /assets/images/baking_lights_get_started_article/baking_lights_getting_started_thumbnail.jpg
---

Different lights in a scene can create a varying atmosphere. Brighter light during the day is often associated with a calmer or upbeat atmosphere, such as you'd expect when going for a picnic.

Dim lights at night create a gloomier, scarier atmosphere. These scenarios can be accomplished using the correct lights in the [Unity Game Engine](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL), and an important concept when using Unity lights is baking.

{% include toc %}

## What does baking lights in Unity mean?

Lights in video games involve computer calculations to simulate their behavior in the real world.

These calculations take more time as the number of lights in your Unity game increases, and too many lights can significantly increase the calculations, negatively impacting the game's performance.

Since most objects in a game don't move throughout the level, these lighting calculations can be completed ahead of time and stored, freeing up computer resources to handle other tasks, such as animations and visual effects.

**The process of calculating lighting data before the game runs** is called baking lights, and the precomputed lighting data is stored in a special texture called a **lightmap**.

## What are lightmaps in Unity used for?

Consider this scenario. Look at the environment around you. Chances are, you're in a room with a chair on which you sit, and a table where you've placed your computer. 

Maybe there's a cup of coffee nearby and some books. The room has some light coming from somewhere, illuminating a significant part of it.

If the time of day never changed, and the room's light remained constant, the lighting in the room would be the same forever.

The bright parts would be bright, the semi-bright parts would remain semi-bright, and the dark parts would remain dark.

Now, pretend for a moment there's a dark room next to the one you're in that has the same things but is completely black.

If you could strip away the surface of every object in the lit room, along with its current brightness, and then place it on the matching object in the dark room, the two rooms would end up looking the same.

That's what happens when you bake lights in the Unity Game Engine.

Unity "turns on the lights" in your level to see what it would look like when lit up, places a large, digital, plastic sheet over all the static objects in a scene (like the plastic that fits snuggly around wrapped food), stores the lighting data in that sheet, peels off the sheet, "turns off the lights", and places the sheet back exactly the same way in the dark level, making it look like it's lit up but without worrying about the lights being on.

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_get_started_article/backyard_lightmap_img.jpg' | absolute_url }}" alt="The lightmap of the backyard in the thumbnail image, as seen from above.">
  <figcaption>The lightmap of the backyard in the thumbnail image, as seen from above.</figcaption>
</figure>

The lightmap (digital plastic sheet) stores the lighting data when baking lights and is placed over the objects in your game's scene, making them look like they're illuminated.

**_Tip:_** Even if you remove the light source after baking lights, the scene will still appear lit because of the precomputed light data. You can clear the baked data to restore the scene's initial appearance.
{: .notice--info}

Unity lights have three light modes:

- Realtime

- Mixed

- Baked

**Realtime lights** are lights whose calculations are done when the game is running. These lights cast dynamic shadows for moving objects in your game.

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_get_started_article/realtime_light_dynamic_shadow.gif' | absolute_url }}" alt="A grey cube with a dynamic shadow moving back and forth in Unity.">
  <figcaption>The cube's shadow moves when it moves.</figcaption>
</figure>

Realtime lights only work with direct lighting, i.e., light coming from the source and landing on an object directly.

**Baked lights** are lights whose calculations are done before the game runs, and the light data is stored in a lightmap. These lights don't cast dynamic shadows without some additional tools.

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_get_started_article/baked_light_static_shadow.gif' | absolute_url }}" alt="A grey cube with a static shadow moving back and forth in Unity.">
  <figcaption>The cube's shadow doesn't move when using baked lights.</figcaption>
</figure>

Baked lights work with direct and indirect lighting. Indirect lighting is light that bounces off a surface and then lands on an object.

**Mixed lights** blend the properties of baked and realtime lights. They work with direct lighting when the game is running and baked indirect lighting, which is precomputed.

Mixed lights also cast dynamic shadows on moving objects.

**_Tip:_** Unity uses a group of techniques called **global illumination** to achieve realistic lighting results.
{: .notice--info}

| Realtime Lights | Baked Lights | Mixed Lights |
| --- | --- | --- |
| Calculations done **as game runs**. | Calculations done **before** game runs. | Calculations can be done **as game runs or before**. |
| Dynamic shadows. | Static shadows. | Dynamic shadows. |
| Direct lights only. | Direct & indirect lights. | Direct & indirect lights. |
| Highest performance impact. | More performant. | Variable performance impact. |

Which light you choose will depend on your goals. Do you have many moving objects that need light? Realtime or mixed lights are a good choice. The same applies to a moving light source, such as a flashlight.

Is most of the scene static? Baked lights will save you some performance.

## Why You Should Bake Lights

Regardless of which light mode you choose, it's still worth baking lights for a couple of reasons.

### Accurate Lighting

Even though realtime lights simulate how light works in the real world better than baked lights, by [default](https://docs.unity3d.com/6000.5/Documentation/Manual/realtime-gi-using-enlighten.html#:~:text=By,Scene%2E), they only work with direct light.

Light bounces in many different ways and indirectly lights up objects, and this behavior can be achieved by baking lights in the Unity Game Engine.

### Performance Gains

Baking lights saves you precious resources that can be used to enhance your game even further compared to doing the light calculations when the game is running.

### Flexibility

You can adjust the lighting settings in the _Lighting_ window to bake lights at different resolutions and complexity.

This flexibility lets you make the necessary adjustments to ensure your game runs at a steady frame rate and maintains optimal performance, even under stress.

## Does baking lights affect reflections in Unity?

Reflections occur when light bounces off a smooth surface. Reflections in Unity are obtained by placing reflection probes in different areas of your scene.

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_get_started_article/reflection_probe_img.jpg' | absolute_url }}" alt="A large reflection probe in front of a house in Unity.">
  <figcaption>The large sphere to the left is a reflection probe.</figcaption>
</figure>

Reflection probes take snapshots of the environment in an area you define and store them in a cubemap.

A **cubemap** is like a hollow box surrounding the reflection probe, and the inside walls of the cubemap are where the snapshots are stored.

The area a reflection probe covers can be adjusted for the best results in your game. When a reflective object moves in that area, the probe looks through the snapshots it took and applies the correct one to the object's surface as a reflection.

There are three types of reflection probes in Unity:

- Realtime

- Baked

- Custom

**Realtime reflection probes** update reflections for dynamic objects in your game's scene, such as the player. The result is more realistic reflections, but it also has a bigger performance impact.

**Baked reflection probes** are baked together with lights and work with static objects. Moving objects in the scene won't update reflections on shiny surfaces if you use baked reflection probes.

**Custom reflection probes** let you use a custom cubemap for reflections.

| Realtime Reflection Probe | Baked Reflection Probe |
| --- | --- |
| Dynamic reflections. | Static reflections. |
| Higher performance impact. | More performant. |
| Best for moving objects. | Best for static objects. |

You can use baked reflection probes and baked lights to precompute all the lighting data in your game's scene for realistic lighting and reflections while saving on performance.

This can be useful for low-end devices, such as mobile phones, VR headsets, or low-end computers.

**_Tip:_** Even though a mirror has reflections, adding one to a game often requires more work than placing reflection probes in a scene.
{: .notice--info}

A hybrid approach of baked lights and some realtime reflection probes can also work. It all depends on your game's needs.

The single source of truth will always be the game's performance when you test it using Unity's profiler.

## Indirect Lighting and Dynamic Objects in Unity

You can use **light probes** in your game to leverage the performance gains of baked lights in addition to more realistic bounced light on dynamic objects.

Light probes store light information **as it passes through empty spaces**, while lightmaps store light information **when it hits an object's surface**.

If you have a dynamic object in the scene, such as a vehicle, you can place light probes in empty areas to store the bounced light information from static objects.

For example, if the car is driving past a blue building, the shadow cast on it from a realtime or mixed light should be slightly blue because of the bounced light.

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_get_started_article/shadow_w_light_probe_img.jpg' | absolute_url }}" alt="A white capsule beside a blue wall in Unity.">
  <figcaption>Shadow with light probes.</figcaption>
</figure>

Without light probes, the shadow will still be dark, but with light probes, the indirect light is calculated correctly, and the shadow cast is slightly blue.

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_get_started_article/shadow_no_light_probe_img.jpg' | absolute_url }}" alt="A white capsule beside a blue wall in Unity.">
  <figcaption>Shadow without light probes.</figcaption>
</figure>

## Cons of Baking Light in Unity

Even though baking lights saves you performance when the game is running, there are still costs associated with it.

### Long Bake Times

Lights in the Unity Game Engine can be baked at varying degrees of accuracy. The more accurate the light, the longer it'll take to bake.

Long bake times are a common challenge for many game developers, but there are settings you can adjust to improve them.

Some of the settings you can change in the _Lighting_ window include the number of times light bounces when it hits a surface, the number of light samples to use when generating lightmaps, or the size of the lightmap.

Larger, higher-resolution lightmaps for lights that bounce many times will take longer to bake than smaller, lower-resolution ones for lights that bounce a few times.

### Noisy Lightmaps

Some lightmaps can produce noisy results due to the lighting settings or geometry in your game.

A lightmap is noisy when it produces smudges and other strange shapes or discolorations on the surface of objects.

This _Unity Lights Troubleshooting Guide_ can help you find the problem and provides potential solutions.

### Inaccurate Shadows

Realtime lights and mixed lights cast sharper, crisper shadows compared to baked lights.

Baked lights may save some performance beforehand, but they sometimes produce softer shadows that aren't always convincing.

<figure class="align-center">
  <img src="{{ '/assets/images/baking_lights_get_started_article/baked_light_static_shadow.gif' | absolute_url }}" alt="A grey cube with a static shadow moving back and forth in Unity.">
  <figcaption>The pole's shadow below the window is smudged.</figcaption>
</figure>

| Baked Light Pros | Baked Light Cons |
| --- | --- |
| Accurate lighting. | Inaccurate shadows. |
| Performance gains. | Long bake times. |
| Flexibility in adjusting settings. | Noisy lightmaps. |

## In Closing

Now that you have a better understanding of baking lights and what it can do for your game, you're ready to learn how to bake lights in the Unity Game Engine.