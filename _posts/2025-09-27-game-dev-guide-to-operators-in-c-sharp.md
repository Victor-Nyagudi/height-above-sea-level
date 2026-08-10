---
title: A Game Developer's Guide to Operators in C#
categories: C#
tags: beginner-c# scripting
excerpt: "If the player in your game picks up some ammo, you'll need to update the ammo count to reflect this increase. It's also common to reduce the player's health whenever they take damage. These are operations that will require operators."
image:
    thumbnail: /assets/images/operators_article/operators-thumbnail--landscape.jpg
---

If the player in your game picks up some ammo, you'll need to update the ammo count to reflect this increase.

It's also common to reduce the player's health whenever they take damage. These are operations that will require operators.

Operators can be used to do mathematical operations such as addition and subtraction, or compare different values to check if they're equal.

This article assumes you have some knowledge of variables, constants, and numbers, but if you don't, read the linked articles to get up to speed.

If you're a visual learner, you can watch the video version below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/PGrNsVII6js?si=bZGYvMPiQMP3xm2Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## What is an operator?

Operators are symbols used to perform various operations in C#. The five most common ones you'll use are:

1. Arithmetic operators

2. Comparison operators

3. Equality operators

4. Assignment operators

5. Logical operators

## Arithmetic Operators

Arithmetic operators are used to perform the common **mathematical operations** you've encountered in your daily life:

- Addition

- Subtraction

- Multiplication

- Division

### Addition

You can add two or more numbers using the (`+`) operator.

This is useful in actions in your Unity game that increase a number. For example, if the player harvests some wood, the wood counter in the user interface should increase.

Alternatively, collecting health pick-ups should replenish the player's health after they've taken damage.

```csharp
var woodInInventory = 20;
var woodCollected = 10;

var totalWood = woodInInventory + woodCollected;

Debug.Log(totalWood); // Logs '30'.

sbyte health = 90;
sbyte healthOrb = 10;

Debug.Log(health + healthOrb); // Logs '100'.
```

If your game involves the player collecting coins, C# has an operator that can increase the total coins collected by exactly 1, since that most likely will be the value of each coin.

This operator is called the **increment operator**, and it's written using two plus signs: (`++`).

When placed after a variable, which is how you'll use it most often, the increment operator increases the variable's value **on the next line**.

When placed before a variable, the increment operator increases the variable's value **on the same line**.

```csharp
var coinsCollected = 7;

// Assume the player just picked a golden coin.

Debug.Log(coinsCollected++); // Logs '7'.
Debug.Log(coinsCollected); // Logs '8'.

var ammo = 19;

// Assume the player just picked a bullet.

Debug.Log(++ammo); // Logs '20'.
Debug.Log(ammo); // Logs '20'.
```

**_Warning:_** This is one of the quirks of using the operator that may leave you wondering why the coin counter isn't increasing when it should, so use it with discretion.
{: .notice--warning}

### Subtraction

Taking damage should reduce the player's health. Similarly, using a magic potion should reduce the total potions in the player's inventory.

You can subtract one number from the other using the (`-`) operator.

Let's say taking a hit reduces the player's health by 25 hit points (HP). This is what the code would look like.

```csharp
var magicPotions = 10;

// Assume the player just used a magic potion.

Debug.Log(magicPotions - 1); // Logs '9'.

byte health = 100;

// Assume the player just took some damage.

Debug.Log(health - 25); // Logs '75'.
```

A similar operator to the increment operator exists in subtraction: the **decrement operator** (`--`).

Unlike the increment operator, this operator decreases the variable by exactly 1.

It decreases the variable on the next line when placed **after the variable**, or on the same line when placed **before the variable**.

```csharp
var magicPotions = 10;

// Assume the player just used a magic potion.

Debug.Log(magicPotions--); // Logs '10'.
Debug.Log(magicPotions); // Logs '9'.

byte health = 100;

// Assume the player just took a small hit.

Debug.Log(--health); // Logs '99'.
Debug.Log(health); // Logs '99'.
```

**_Tip:_** Only the addition and subtraction operators have a unique variation of them.
{: .notice--info}

### Multiplication

If the game you're making in the Unity game engine has damage multipliers, you can use the multiplication (`*`) operator to implement them.

This operator multiplies two or more numbers together, so you could store the damage booster in a constant and then multiply that by the current damage to triple it.

```csharp
const int DamageMultiplier = 3;

var currentDamage = 50;

var boostedDamage = currentDamage * DamageMultiplier;

Debug.Log(boostedDamage); // Logs '150'.
```

### Division

Some games have debuffs that negatively impact the player, such as slowing down their movement.

Let's say there's an evil wizard in your game that casts a spell on the player, reducing their movement speed by 50%.

You can divide the player's speed by 2 to get the new speed when the debuff is applied using the division (`/`) operator.

```csharp
var speed = 100;
var speedPenalty = 2;

var slowedSpeed = speed / speedPenalty;

Debug.Log(slowedSpeed); // Logs '50'.
```

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

### Remainder

The remainder operator (`%`) is used to get the remainder after dividing a number.

For example, 10 divided by 4 results in a remainder of 2 because 4 can only go into 10 a maximum of two times.

```csharp
int ten = 10;
int four = 4;

var remainder = ten % four;

Debug.Log(remainder); // Logs '2'.
```

Let's say you want to create a pattern in your Unity game where the odd-numbered tiles are white and the even-numbered tiles are black.

You could use the remainder operator to divide all the numbers by 2. If there's a remainder, then the number is odd. If there's no remainder, the number is even.

```csharp
var tileOne = 1;
var tileTwo = 2;
var tileThree = 3;
var tileFour = 4;

Debug.Log(tileOne % 2); // Has remainder. Is odd, so white tile.
Debug.Log(tileTwo % 2); // No remainder. Is even, so black tile.
Debug.Log(tileThree % 2); // Has remainder. Is odd, so white tile.
Debug.Log(tileFour % 2); // No remainder. Is even, so black tile.
```

## Comparison Operators

Comparison operators **compare two numbers** to check which is bigger, smaller, or if the two numbers are equal.

These operators use the common mathematical symbols:

- `>`: greater than

- `<`: less than

- `>=`: greater than or equal to

- `<=`: less than or equal to

If your game has a rage mode, you can check if the current rage meter has reached or exceeded a certain number, then activate it.

```csharp
var currentRage = 95;

const sbyte RageTrigger = 100;

if (currentRage >= RageTrigger)
{
    Debug.Log("Rage mode enabled. AARGH!!");
    // Increase damage, speed, and health in this code block.
}
```

## Equality Operators

Equality operators **check if two numbers are equal**.

`==` checks if two values are equal, while `!=` checks if two values aren't equal.

You can use them to check if a player has taken damage before trying to replenish their health when they collect a health orb to prevent exceeding the maximum health they can have.

```csharp
var health = 75;
var healthOrb = 10;

// Only add HP if health is not full.
if (health != 100)
    Debug.Log(health + healthOrb); // Logs '85'.

if (health == 100)
    Debug.Log("Max health reached."); // Doesn't log anything. Can you guess why?
```

## Assignment Operators

Assignment operators **assign values to a variable**. The most common one is the single `=` sign.

A variable is often assigned a value during creation, but this can be delayed until later in your game's code.

The `=` can be combined with arithmetic operators to assign variables new values.

- `+=`: assigns a new value to the variable, where the **number to its right** is added to the variable's old value.

- `-=`: **deducts the number to its right** from the variable's old value, then updates the variable.

- `*=`: **multiplies the number to its right** by the variable's old value, then updates the variable.

- `/=`: **divides the variable's old value** by the number to its right, then updates the variable.

```csharp
int shields = 100;

shields += 25; // Player picks up '25'shields.

Debug.Log(shields); // 'shields' are now at '125'.

var health = 100;

health -= 20; // Player has taken '20' damage.

Debug.Log(health); // 'health' is now at '80'.

// The same applies to '*=' and '/=' operators.
```

## Logical Operators

Logical operators are used on values that are either `true` or `false`. These are known as booleans.

They're commonly used in conditional statements, a topic discussed in more detail in a separate post, to toggle different parts of your Unity game's code on or off.

Let's say you want to give the driver in your racing game 500XP if they finish first in the race.

The two conditions for them to get the XP are:

1. They have to finish the race.

2. They have to finish the race in first place.

You can use the `&&` operator to achieve this.

It lets you chain multiple conditions, so the code in the if statement only executes if **all the conditions are met**.

If even one condition isn't met, the code does not execute.

```csharp
var hasFinishedRace = true;
var finishPosition = 1;

if (hasFinishedRace && finishPosition == 1)
    Debug.Log("Driver has received 500XP!");
```

Alternatively, you could give the driver 100XP if they finish the race in any position **or** pass through 5 checkpoints.

The two conditions are:

1. Finishing the race, or...

2. Passing through 5 checkpoints.

The difference this time is that **only one condition** must be met for the code to execute.

You can use the `||` operator to achieve this. The two symbols are called a **double pipe**.

```csharp
var hasFinishedRace = true;
var checkpointsPassed = 3;

if (hasFinishedRace || checkpointsPassed == 5)
    Debug.Log("Driver has received 100XP!");
```

The `!` operator **inverts a `true` or `false` value**. For example, `!true` is read as "**NOT true**", while `!false` is "**NOT false**".

It's useful when working with predefined Boolean variables that the player controls and can change at any time.

You can use it to check if the player is **not** on the ground before playing a flying kick animation.

This ensures the flying kick animation only plays when the player is airborne because they can choose to stay grounded or jump at any time.

```csharp
bool isPlayerGrounded = true;

if (!isPlayerGrounded)
{
    // If player is NOT grounded, this is logged to the console.
    Debug.Log("The player is airborne.");
}

Debug.Log(!true); // Logs 'false'.
Debug.Log(!false); // Logs 'true'.
```

### Recap

- **Arithmetic operators** are for mathematical operations, such as addition and subtraction.

- **Comparison operators** check if one number is larger, smaller, or equal to another.

- **Equality operators** check if two numbers are equal or not.

- **Assignment operators** assign or re-assign values to variables.

- **Logical operators** chain conditions together or reverse a Boolean value.

This post is the fourth in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses how to use strings to work with text.

Here's the full list of posts in the series:

1. A Game Developer's Guide to Variables in C#
2. A Game Developer's Guide to Constants in C#
3. A Game Developer's Guide to Numbers in C#
4. A Game Developer's Guide to Operators in C# _(you are here)_
5. A Game Developer's Guide to Strings in C#
6. A Game Developer's Guide to Booleans in C#
7. A Game Developer's Guide to Enums in C#
8. A Game Developer's Guide to Conditional Statements in C#
9. A Game Developer's Guide to Loops in C#
10. A Game Developer's Guide to Classes in C#
11. A Game Developer's Guide to Access Modifiers in C#
12. A Game Developer's Guide to Fields & Properties in C#
13. A Game Developer's Guide to Methods in C#
14. A Game Developer's Guide to Lists & Arrays in C#
15. A Game Developer's Guide to Dates & Times in C#