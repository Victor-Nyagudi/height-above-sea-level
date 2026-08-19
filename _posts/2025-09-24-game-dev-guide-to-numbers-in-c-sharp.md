---
title: A Game Developer's Guide to Numbers in C#
categories: C#
tags: beginner-c# scripting
excerpt: "From the remaining lives a player has to the health potions in their inventory, every video game deals with numbers at some point or another, so knowing how to work with them in C# is crucial to making a successful game in the Unity Game Engine."
image:
    path: /assets/images/numbers_article/numbers_article_header_img.jpg
    thumbnail: /assets/images/numbers_article/numbers_article_thumbnail.jpg
date: 2026-08-10
---

From the remaining lives a player has to the health potions in their inventory, every video game deals with numbers at some point or another, so knowing how to work with them in C# is crucial to making a successful game in the [Unity Game Engine](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL).

Numbers in C# can be generally categorized into two types: **whole numbers**, also known as integers, and **decimal numbers**, also referred to as floating-point numbers.

This article assumes you have a basic understanding of [variables]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %}) and [constants]({{ site.baseurl }}{% post_url 2025-09-21-game-dev-guide-to-constants-in-c-sharp %}). If you're not familiar with them, read the linked posts first.

If you're a visual learner, you can watch the video version below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/p9KItGlIlkA?si=_9jQYvE01_rNlQA7" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

{% include toc %}

## How do you create a number in C#?

Numbers already exist in C#, so you don't have to re-create them.

A common approach is to store them in variables or constants and use them in mathematical operations like addition, subtraction, etc.

```csharp
int one = 1;

int two = 2;

var three = 3;

const float Four = 4.0f;
```

Mathematical operations are discussed in more detail in the [operators]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %}) article.

## Whole Numbers (Integers)

Whole numbers in video games work well with **anything that increases or decreases in fixed steps of one or more**, such as ammo, player lives, or coins collected.

If the player fires their gun, the remaining ammo decreases by one.

If they hold down the fire button to empty the clip, the ammo continuously decreases by one until it reaches zero, and they run out of ammunition.

When the player picks up ammo, the number jumps to a fixed whole number, such as 25, not 25.5. The same applies to losing and gaining lives.

There are multiple [integer types in C#](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types) you can use, but the following are the five most common ones that will most likely apply to the Unity game you're building.

### `sbyte`

An `sbyte` is one of the smaller integer types that stores numbers **from -128 to 127**. Trying to store any number less than -128 or greater than 127 will result in an error.

```csharp
sbyte age = 23;

var remainingLives = 3; // ❌ You have to use 'sbyte' instead of 'var'.

const sbyte Health = 100;

public class Elf
{
    private sbyte _mana = 100;

    // ... Other code about the class goes here.
}

sbyte shields = 200; // ❌ 'sbyte' can only go up to 127.
```

If the player in your game can have at most 3 lives, an `sbyte` would be a good option because it covers the range of lives, 0 to 3, while taking up little space: **1 byte**.

You could also use it for character ages in a role-playing game since humans rarely live past the age of 127.

### `byte`

A `byte` is another small integer type capable of storing numbers **from 0 to 255**.

It also **takes up 1 byte of space**.

```csharp
byte shields = 200;

var speed = 25; // ❌ You have to use 'byte' instead of 'var'.

const byte DamageMultiplier = 150;

public class Dwarf
{
    private byte _maxAge = 250;

    // ... Other code about the class goes here.
}

byte income = 1000; // ❌ 'byte' can only go up to 255.
```

If you want a little more breathing room than an `sbyte` offers without using up too much extra space, a `byte` is a good choice.

For example, if your fantasy characters can live up to 250, then you can store their age in a `byte` instead of an `sbyte`.

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

### `short`

A `short`, sometimes written as `Int16`, has a capacity of **-32,768 to 32,767**.

This could be useful if, for instance, the maximum amount of wood or steel the player can harvest is 20,000 units.

```csharp
short woodCollected = 732;

Int16 potatoesCollected = 658;

var steel = 800; // ❌ You have to use 'short' instead of 'var'.

const short MaxDamage = 1500;

public class SteelMill
{
    private short _capacity = 20000;

    // ... Other code about the class goes here.
}

short missionReward = 50000; // ❌ 'short' can only go up to 32,767.
```

Simply put, if you need a number that can reach the low thousands, a `short` is a good candidate.

It **takes up 2 bytes of space**.

### `int`

An `int`, also written as `Int32`, is one of the most commonly used integer types. It has a capacity of about **-2.1 billion to around 2.1 billion**.

Its large capacity makes it ideal for games with giant economies where numbers can reach the billions.

```csharp
int income = 100000;

Int32 grenades = 20;

// ✅ You can use 'var' with a WHOLE number only for 'int' type.
var steel = 800;

const int MaxSpeed = 250;

public class Bank
{
    private int _capacity = 200000000;

    // ... Other code about the class goes here.
}
```

It **takes up 4 bytes of space**, so if your game is performance-critical and you don't need the large range, one of the smaller types would be a better choice.

### `long`

A `long`, also written as `Int64`, is another one of the larger integer types, surpassing the billions.

```csharp
long totalXP = 1000;

Int64 weaponSkill = 5;

// ✅ You can use 'var' only with numbers BIGGER than what an 'int' can hold.
var regionIncome = 8000000000;

const long MaxLevel = 200;

public class City
{
    private long _totalPopulation = 100000000;

    // ... Other code about the class goes here.
}
```

A `long` **takes up 8 bytes of space** due to its much larger range compared to the other integer types.

You may notice some performance dips as your video game grows when working with numerous `long` type numbers, so use it with discretion.

You'll more often than not be fine using an `int` over a `long`.

## Decimal Numbers (Floating-point Numbers)

Decimal numbers in video games work well **when dealing with numbers that require greater precision**, such as health bars in the user interface or aiming angles.

If the player in your game needs to throw an object, it's a much better experience if they can aim in small, fine movements instead of janky, snappy motions, in _some_ games at least.

C# has three floating-point types to help you achieve this.

**_Tip:_** You can still use floating-point types with whole numbers, but you can't use integer types with decimal numbers.
{: .notice--info}

### `float`

Probably the easiest to remember since it uses the same first four words as floating, a `float`, also known as a `Single`, is the smallest of the three.

A `float` number **must** end with an "_f_" or "_F_" if it's a decimal, but the suffix can be omitted when using whole numbers.

```csharp
float currentProgress = 76.8f;
float inventoryItems = 30;
float angle = 22.5; // ❌ Number must end with 'f'/'F' if it's a decimal.

Single checkpoints = 10;
Single healthRemaining = 1.7F;

// ✅ You can use 'var' ONLY if the number ends with 'f'/'F'.
var xpLost = 20000f;

const float Rotation = 45.0f;

public class Throwable
{
    private float _defaultArc = 63.5F;

    // ... Other code about the class goes here.
}
```

It has a capacity in the billions on the positive and negative sides and **uses up 4 bytes of space**.

This is the least accurate of the three, but it works fine for the majority of games you'd want to make in Unity.

### `double`

A `double` is larger than a `float` and is the default type used with decimal numbers that don't end with a letter.

```csharp
double airplaneYaw = 76.8d;
double totalFuel = 1000;

// ✅ Adding 'd'/'D' to decimal numbers is optional.
double remainingDistance = 22.5;

// ✅ Decimal numbers default to 'double' type
// if there's no letter after the number.
var fuelCostPerMile = 200.50;

const double BankingAngle = 75.0D;

public class Airplane
{
    private double _cost = 200000000.00d;

    // ... Other code about the class goes here.
}
```

It has a capacity exceeding the billions and **uses up 8 bytes of space**. A double type number can optionally end with "_d_" or "_D_".

You can think of it as a middleground between the `float` and `decimal`, balancing precision and performance.

It could work in your game, but the extra precision might be an unnecessary trade-off for the extra space it consumes.

### `decimal`

The most accurate of the three, a `decimal` type, is great for games with elaborate banking systems and economies that need numbers to be as precise as possible.

```csharp
decimal housingCost = 100000.00m;
decimal interestRate = 32.625M;

// ❌ Numbers must end with 'm'/'M'.
decimal profitMargin = 1.0923;

// ✅ You can use 'var' if the number ends with 'm'/'M'.
var losses = 147325.098321m;

const decimal RevenuePerCustomer = 22.76530M;

public class Country
{
    private decimal _debt = 200000000.525m;

    // ... Other code about the class goes here.
}
```

A `decimal` type, in exchange for the extra precision, **uses up the most space at 16 bytes**. This extra memory consumption is more noticeable as your game grows.

Numbers of type `decimal` **must** end with an "_m_" or "_M_". The accuracy is most noticeable when rounding decimal numbers.

If accuracy is fundamental to the Unity game you're building, the tradeoff could be worth it.

## `float` vs. `double` vs. `decimal`: Which to Use?

The one you choose will depend on how accurate you want your numbers to be versus how performant your game is.

| `float` | `double` | `decimal` |
| --- | --- | --- |
| Numbers end with "f"/"F". | Numbers end with "d"/"D". | Numbers end with "m"/"M". |
| Consumes the least space. (4 bytes) | Consumes twice as much space as `float`. (8 bytes) | Consumes the most space. (16 bytes) |
| Good accuracy. | Better accuracy. | Most accurate. |

A `float` is sufficient for most games, ranging from simple platformers to complex 3D adventure games. The added accuracy of the other types won't always add value to your game.

A `decimal` is great in money-oriented games for an extra layer of realism, but this extra detail may go unnoticed, and you end up using up more resources for something that could've used less had you gone with a different type.

**_Tip:_** If you don't assign a value to a number variable, whole or decimal, the number defaults to 0.
{: .notice--info}

## Why can't you use commas to separate big numbers in C#?

Commas are used to separate a group of items in lists, arrays, and other types. Using them to separate large numbers in C# will cause an error.

You can use an underscore in place of the commas to separate large numbers into a more human-readable format.

```csharp
int oneBillion = 1,000,000,000; // ❌ Doesn't work!

int oneBillion = 1_000_000_000; // ✅ No issues here.
```

The underscore is a **digit separator**. The computer will still read the number correctly if you use it.

## Recap

- Numbers in C# can generally be classified as whole (integer) or decimal (floating-point) numbers.

- `sbyte`, `byte`, `short`, `int`, and `long` are used with whole numbers only.

- `float`, `double`, and `decimal` are used with decimals, but can also be used with whole numbers.

- The larger its range or the more accurate a number is, the more space it uses up.

- A decimal number created with `var` and no suffix defaults to the `double` type.

This post is the third in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses how to use numbers in mathematical operations, such as addition and subtraction, using [operators]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %}).

Here's the complete list:

1. [A Game Developer's Guide to Variables in C#]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %})
2. [A Game Developer's Guide to Constants in C#]({{ site.baseurl }}{% post_url 2025-09-21-game-dev-guide-to-constants-in-c-sharp %})
3. A Game Developer's Guide to Numbers in C# _(you are here)_
4. [A Game Developer's Guide to Operators in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %})
5. [A Game Developer's Guide to Strings in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %})
6. [A Game Developer's Guide to Booleans in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-booleans-in-c-sharp %})
7. [A Game Developer's Guide to Enums in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-enums-in-c-sharp %})
8. [A Game Developer's Guide to Conditional Statements in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-conditional-statements-in-c-sharp %})
9. [A Game Developer's Guide to Loops in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-loops-in-c-sharp %})
10. [A Game Developer's Guide to Classes in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-classes-in-c-sharp %})
11. A Game Developer's Guide to Access Modifiers in C#
12. A Game Developer's Guide to Fields & Properties in C#
13. A Game Developer's Guide to Methods in C#
14. A Game Developer's Guide to Lists & Arrays in C#
15. A Game Developer's Guide to Dates & Times in C#