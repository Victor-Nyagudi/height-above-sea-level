---
title: A Game Developer's Guide to Booleans in C#
categories: C#
tags: beginner-c# scripting
excerpt: "Booleans in C# are like on/off switches. They're often used with conditional statements to control the flow of your code's execution. Booleans can only be one of two values: `true` or `false`."
image:
    path: /assets/images/booleans_article/booleans_article_thumbnail.jpg
    thumbnail: /assets/images/booleans_article/booleans_article_thumbnail.jpg
---

Booleans in C# are like **on/off switches**. They're often used with conditional statements to control the flow of your code's execution.

Booleans can only be one of two values: `true` or `false`. These values have the same meaning in programming as they do in English, and they play a part in how booleans are named.

This article assumes you know how to use [variables]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %}), [operators]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %}), [numbers]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %}), and [strings]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %}), and will reference them in code examples.

If you're a visual learner, you can watch the video version below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/Yt3EzAm6SGQ?si=pIzsDw5Y9A43mFk0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

{% include toc %}

## How to Use Booleans in Unity

Boolean variables or [constants]({{ site.baseurl }}{% post_url 2025-09-21-game-dev-guide-to-constants-in-c-sharp %}) are created using the `bool` keyword. The variable is assigned a value of either `true` or `false`.

If you don't assign a boolean variable a value, it automatically defaults to `false`.

**_Tip:_** "true" and "false" are special keywords in C#. You can't use them to name anything without some modification.
{: .notice--info}

It's a common convention to name booleans by **prefixing "_is_" or "_has_" to the name**, such that the name sounds like it's asking a question.

```csharp
bool isGrounded = true;

var hasPowerUp = false;
```

In addition to making it easier to distinguish boolean variables from other variables in C#, this naming convention improves your code's readability.

Consider this example. Let's say the game you're building in the [Unity Game Engine](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL) has a character that can punch or fire their gun, depending on whether they're armed or not at the moment.

You can use a boolean value, like `isArmed`, to check if the player is holding a weapon. If this value is true, the character fires their gun. If not, they punch.

```csharp
var isArmed = true;

if (isArmed)
    Debug.Log("Fire the gun."); // <- This line will execute.
else
    Debug.Log("Punch.");
```

By using the naming convention, you can read this as, "If the player is armed, fire the gun. Otherwise, punch."

The boolean value in this scenario acts as a switch. When you turn on a car, the engine runs. Similarly, if the value is `true`, the switch is on, and the code block gets executed.

When you turn off the car, the engine stops. If the value is `false`, the switch is off, and the code block isn't executed.

`if` statements are covered in more detail in the conditional statements article, but they are strongly tied to booleans, so they'll be mentioned briefly.

**_Tip:_** You can use booleans in Unity as a literal switch to turn the [lights]({% post_url 2025-11-01-baking-lights-in-unity-getting-started %}) in a room on or off.
{: .notice--info}

## The Relationship Between Booleans and Operators

### Comparison and Equality Operators

**Comparison operators and equality operators result in a boolean value**. In a way, these operators ask a question. They can also be used in the condition of a conditional statement.

Some examples of comparison operators include greater than `>`, less than `<`, and greater than or equal to `>=`.

Let's say you want to show a warning message if the player tries to collect crafting material when they've reached the maximum.

You can use a comparison operator to compare the current crafting materials in the inventory, plus the collected ones, with a predefined maximum limit.

If the new total number of crafting items is greater than the limit, you'll show the player a message informing them they can't hold any more crafting items.

```csharp
const int MaxCraftingMaterials = 5000;

var inventoryMaterials = 4620;
var materialsCollected = 500;

var totalMaterials = inventoryMaterials + materialsCollected;

if (totalMaterials > MaxCraftingMaterials)
    Debug.Log("You can't carry any more materials.");
```

Similarly, suppose your Unity game features collectibles, and you want to award the player 500 XP after collecting 10 items,

In that case, you can use an equality operator to check if the player has reached this milestone, then award the XP.

**_Tip:_** Equality operators use two "=" signs.
{: .notice--info}

```csharp
var collectibles = 9;

if (collectibles == 10)
{
    // This code block won't be executed because
    // 'collectibles' (9) is NOT equal to 10 above.
    Debug.Log("You've received 500XP!");
}
```

### NOT Operator (!)

The **NOT operator**, written using a single exclamation mark (!), reverses a boolean value.

For example, `!true` is `false`. You can read it as "NOT true", meaning false. Similarly, `!false` (NOT false) is `true`.

The NOT operator is useful for boolean values that change often. This is evident in scenarios, such as the one mentioned earlier in this article, where the player can either be armed or disarmed.

There'll be times you want to do other things when the player is unarmed, such as carrying heavy objects. For simplicity's sake, assume there's no way to holster the weapon.

Picking up or dropping weapons changes the `isArmed` boolean variable, so you can check if the player is unarmed by placing an exclamation mark before `isArmed`, turning it into "is NOT armed", then lifting an object.

```csharp
var isArmed = true;

if (!isArmed)
    Debug.Log("You can now pick up objects.");
```

Booleans can also be used in classes when declaring fields or properties. Those are explained in more detail in separate articles.

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

## Recap

- Booleans are like on/off switches **controlling the execution of different sections of code**.

- Boolean names are commonly **prefixed with "_is_" or "_has_"**.

- Boolean variables **default to `false`** if not assigned a value.

- **Comparison and equality operators** result in a boolean value.

- The NOT operator **reverses a boolean value**.

This article is the sixth in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses how to use [enums]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-enums-in-c-sharp %}) to work with multiple related constants.

Here's the complete list of articles in the series:

1. [A Game Developer's Guide to Variables in C#]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %})
2. [A Game Developer's Guide to Constants in C#]({{ site.baseurl }}{% post_url 2025-09-21-game-dev-guide-to-constants-in-c-sharp %})
3. [A Game Developer's Guide to Numbers in C#]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %})
4. [A Game Developer's Guide to Operators in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %})
5. [A Game Developer's Guide to Strings in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %})
6. A Game Developer's Guide to Booleans in C# _(you are here)_
7. [A Game Developer's Guide to Enums in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-enums-in-c-sharp %})
8. [A Game Developer's Guide to Conditional Statements in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-conditional-statements-in-c-sharp %})
9. [A Game Developer's Guide to Loops in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-loops-in-c-sharp %})
10. [A Game Developer's Guide to Classes in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-classes-in-c-sharp %})
11. [A Game Developer's Guide to Access Modifiers in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-access-modifiers-in-c-sharp %})
12. [A Game Developer's Guide to Fields & Properties in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-fields-and-properties-in-c-sharp %})
13. [A Game Developer's Guide to Methods in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-methods-in-c-sharp %})
14. [A Game Developer's Guide to Lists & Arrays in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-lists-and-arrays-in-c-sharp %})
15. [A Game Developer's Guide to Dates & Times in C#]({{ site.baseurl }}{% post_url 2026-08-20-game-dev-guide-to-dates-and-times-in-c-sharp %})