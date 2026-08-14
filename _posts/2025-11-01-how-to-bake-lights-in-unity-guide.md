---
title: "How to Bake Lights in Unity: A Step-by-Step Guide"
categories: Unity
tags: lighting
excerpt: "Baked lights in Unity offer better performance than realtime lights because all the lighting computations happen before the game runs. They add realism to your game by simulating bounced light and how it lights up different areas in the scene."
image:
    path: /assets/images/how_to_bake_lights_article/how_to_bake_lights_thumbnail.jpg
    thumbnail: /assets/images/how_to_bake_lights_article/how_to_bake_lights_thumbnail.jpg
---

Baked lights in Unity offer better performance than realtime lights because all the lighting computations happen before the game runs.

They add realism to your game by simulating bounced light and how it lights up different areas in the scene.

Coupled with reflection probes and light probes, you can achieve realistic lighting at a fraction of the cost.

This guide walks you through all the things you need to do before [baking lights in the Unity Game Engine]({{ site.baseurl }}{% post_url 2025-11-01-baking-lights-in-unity-getting-started %}) and provides additional useful information to achieve your desired lighting setup.

If you're reading this article on a smaller device, right-click on the images (long-press on touch devices) and select _Open image in new tab_ to view them at full size.

{% include toc %}

## Set Up Process

If you're new to Unity and don't know the basics, such as the _Hierarchy_ window, _Inspector_ window, or how to work with assets, watch this [introductory video](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL) to get up to speed.

The first step in preparing your models for light baking is to **ensure they can generate lightmap UVs**.

Remember that **baked lights work best with static objects** in your scene, such as the walls in a house, immovable furniture, or props the player can see but can't interact with.

If you imported the 3D model from the Unity Asset Store, it will likely be inside a folder named _Models_, _Meshes_, _FBX_, or something similar. If you dragged it into Unity from your computer, it'll show up as is.

Remember that 3D models end in `.fbx`, so don't confuse them with other similar-looking files, such as prefabs that end in `.prefab` or materials, which end with `.mat`.

Once the 3D model has been imported using Unity's _Package Manager_ window or dragged and dropped into the _Project_ window from your computer, click it and observe the _Inspector_ window.

**_Tip:_** If you can't find a window, click on the _Window_ option in the navbar at the top of the screen and check the dropdowns.
{: .notice--info}

Click the _Model_ tab in the _Inspector_ window and check the box next to _Generate Lightmap UVs_. Click _Apply_ to apply the settings.

<figure class="align-center">
  <img src="{{ '/assets/images/how_to_bake_lights_article/generate_lightmap_uv_img.jpg' | absolute_url }}" alt="The 'Generate Lightmap UVs' checkbox in Unity.">
  <figcaption>The <em>Generate Lightmap UVs</em> checkbox.</figcaption>
</figure>

Checking this box **ensures the 3D model will generate lightmap data** when baking lights. Repeat this for the other static objects in the level you're building.

Next, drag the 3D model into the _Scene_ window, turning it into a _GameObject_.

Once the model is in the scene, the _Inspector_ window will display new information related to GameObjects. Check the box at the top right beside _Static_ to let Unity know the model won't move at any point in the level.

<figure class="align-center">
  <img src="{{ '/assets/images/how_to_bake_lights_article/static_checkbox_img.jpg' | absolute_url }}" alt="The 'Static' checkbox in Unity.">
  <figcaption>The <em>Static</em> checkbox.</figcaption>
</figure>

If you modeled the GameObject using _ProBuilder_, it will likely have a _ProBuilder MeshFilter_ component with a _Lightmap Static_ checkbox that'll be automatically checked when you check the _Static_ checkbox.

The GameObject should have a _Mesh Renderer_ component in the _Inspector_. Click it to unfold the dropdown, revealing other dropdowns.

**_Tip:_** If you don't see this component, it might be on one of the GameObject's children. You can check for children in the _Hierarchy_ window.
{: .notice--info}

The one you're most interested in is the _Lighting_ dropdown. Click it to reveal the lighting options.

Check the box next to _Contribute Global Illumination_ so the GameObject influences lightmaps and light probes when baking lights.

<figure class="align-center">
  <img src="{{ '/assets/images/how_to_bake_lights_article/contribute_gi_checkbox_img.jpg' | absolute_url }}" alt="The 'Contribute Global Illumination' checkbox in Unity.">
  <figcaption>The <em>Contribute Global Illumination</em> checkbox.</figcaption>
</figure>

**_Tip:_** Checking _Contribute Global Illumination_ without marking the GameObject as _Static_ will automatically check the _Static_ box.
{: .notice--info}

Enabling global illumination will reveal another dropdown named _Lightmapping_. These settings inside it can be left as is, unless you want even finer control over the lightmapping process.

Leave the _Receive Global Illumination_ dropdown at _Lightmaps_ since the GameObject will be illuminated by the lighting data from the lightmap.

If you don't want the GameObject to cast shadows or only want shadows from a particular direction, you can change the _Cast Shadows_ option.

Repeat these steps with any new GameObjects you add to the scene as you're designing your level.

## Types of Light in Unity

There are different light types in the Unity Game Engine, so the one you choose will depend on how you want the light to affect the scene.

### Directional Light

Directional lights are good for **light coming from a source very far away**, such as the sun or the moon. They don't have a physical location in the scene, so you can place them anywhere, and the lighting will be the same. One is often enough per level.

<figure class="align-center">
  <img src="{{ '/assets/images/how_to_bake_lights_article/directional_light_img.jpg' | absolute_url }}" alt="A directional light gizmo surrounded by a red square in front of a house in Unity.">
  <figcaption>Directional light in a scene.</figcaption>
</figure>

### Point Light

Point lights are good for **lights that light up an area in a radius**, such as light from candles, a lantern, or a fire.

<figure class="align-center">
  <img src="{{ '/assets/images/how_to_bake_lights_article/point_light_house_img.jpg' | absolute_url }}" alt="A point light in front of a house in Unity.">
  <figcaption>A point light by the fence.</figcaption>
</figure>

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

### Spot Light

Spot lights work well with **lights projected in one direction in a cone shape**, such as you'd see from flashlights or search lights.

<figure class="align-center">
  <img src="{{ '/assets/images/how_to_bake_lights_article/flashlight_in_house_img.jpg' | absolute_url }}" alt="A spot light illuminating a red ball and yellow square in Unity.">
  <figcaption>A spot light in a house.</figcaption>
</figure>

### Area Light

Area lights **emit light uniformly from a circular or rectangular area**. These are great for indoor lights and other smaller sources of light.

<figure class="align-center">
  <img src="{{ '/assets/images/how_to_bake_lights_article/area_lights_img.jpg' | absolute_url }}" alt="Area lights on the front porch of a house in Unity.">
  <figcaption>Area lights by the front door.</figcaption>
</figure>

| Directional Light | Point Light | Spot Light | Area Light |
| --- | --- | --- | --- |
| Lights up entire scene. | Circular radius light. | Cone shaped light. | Circular or rectangular light emission. |
| 1 per scene often enough. | Can have multiple. | Can have multiple. | Can have multiple. |
| Sun or moon. | Candles, lanterns, etc. | Flashlights, streetlights, etc. | Gentle lights e.g. bulbs. |
| Modest performance. | Many hurt performance. | Better performance than point. | Most costly. |
| Realtime or baked. | Realtime or baked. | Realtime or baked. | Baked only. |

## Adding Lights in Unity

Once the level looks the way you envisioned, it's time to add some lights.

Click the "+" in the _Hierarchy_ window > _Light_ > Select the light you want to add.

You can change the lighting mode from _Realtime_, _Mixed_, or _Baked_ based on which looks good to you.

Realtime and mixed lights have crisper, dynamic shadows but have a bigger impact on performance.

Baked lights are the best for performance but **don't update the lighting when they're moved** and **don't cast dynamic shadows for moving objects**.

**_Tip:_** You can bake lights in Unity for all three light types to improve your game's appearance. You don't have to use realtime lights only.
{: .notice--info}

You can control each light's intensity, color, range, and shadows cast by changing the options in the _Light_ component in the Inspector window.

Once you've added all the lights and the scene looks good to you, it's time to bake them.

## Baking Lights in Unity

First, open the _Lighting_ window if it's not open: _Window_ > _Rendering_ > _Lighting_.

Under the _Lighting Settings_ in the Scene tab, you'll need to create a new _Lighting Settings Asset_. This is a file that stores the level's lighting settings and ends with `.lighting`.

You don't have to adjust any values initially after creating the asset, but it's required to change the lighting settings.

Ensure the _Baked Global Illumination_ box is checked, and select _Shadowmask_ or _Baked Indirect_ for the [_Lighting Mode_](https://docs.unity3d.com/6000.2/Documentation/Manual/class-LightingSettings.html#:~:text=Lighting%20Mode%20dropdown) option. You can tinker with these later to see which works better for your game.

<figure class="align-center">
  <img src="{{ '/assets/images/how_to_bake_lights_article/generate_light_btn_img.jpg' | absolute_url }}" alt="Buttons used to bake lights in Unity surrounded by red squares.">
  <figcaption>Time to bake some lights.</figcaption>
</figure>

Click the button at the bottom of the window labeled _Generate Lighting_ to bake lights and wait until the countdown timer at the bottom right of the screen reaches 0.

<figure class="align-center">
  <img src="{{ '/assets/images/how_to_bake_lights_article/before_bake_img.jpg' | absolute_url }}" alt="A dark front section of a house in Unity.">
  <figcaption>Before baking lights.</figcaption>
</figure>

<figure class="align-center">
  <img src="{{ '/assets/images/how_to_bake_lights_article/after_bake_img.jpg' | absolute_url }}" alt="An illuminated front section of a house in Unity.">
  <figcaption>After baking lights.</figcaption>
</figure>

If you followed the steps correctly, the objects in your level should have more realistic lighting. If not, read the _Unity Lights Troubleshooting Guide_ to help triage the problem.

Baking lights in Unity can take a long time, so you can turn down some of the lighting settings to speed it up.

Here's a breakdown of some of the settings and how they affect light baking:

- **Lightmapper**: Determines which piece of hardware you'll use to bake lightmaps, either the CPU or GPU. Try switching between them if one takes too long to bake lights.

- **Direct Samples**: Samples used for direct light calculations. Higher values improve the lightmap quality but increase bake times. Changes in predefined steps, between 1 and 256.

- **Indirect Samples**: Samples used for indirect light (bounced light). Higher values improve the lightmap quality but increase bake times. Changes in predefined steps, between 1 and 256.

- **Max Bounces**: Maximum number of light bounces used in calculating indirect lighting. Higher values improve indirect lighting but may increase bake times.

- **Lightmap Resolution**: Controls the lightmap's resolution. Higher values improve the lightmap's resolution but increase bake times.

**_Tip:_** You can hover over each setting, and a tooltip will appear explaining what it does.
{: .notice--info}

## In Closing

You now know how to bake lights in the Unity Game Engine, and what's left is to tweak the settings until you achieve the desired lighting in your level.

You can go a step further and adjust the final appearance of your game using post-processing to achieve things like glowing objects or effects like film grain for games set in older times.