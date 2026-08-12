---
title: A Game Developer's Guide to Constants in C#
categories: C#
tags: beginner-c# scripting
image:
    path: /assets/images/constants_article/constants_article_header_img.jpg
    thumbnail: /assets/images/constants_article/constants_article_thumbnail.jpg
---

A constant in C#, the half-brother of a [variable]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %}), is like **a mini storage location for temporary data** you'll reuse when building a video game in the [Unity Game Engine](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL).

As the name suggests, a constant is **a value that stays the same after it is created**. It can only be updated in one place: where you created it.

If the player in your game can only carry a maximum of 20 items in their inventory, you can store that number in a constant so you don't accidentally change it somewhere else in the code.

Constants are fundamental to any video game and are often used with variables, whether in handwritten code or visual scripting tools.

## How do you create a constant in C#?

There are four simple steps to creating a constant.

1. Write the keyword `const`.
2. Write the constant's type.
3. Write the constant's name.
4. Give the constant a value.

```csharp
// 'int' is the type.
// 'MaxAmmo' is the name.
// '30' is the value.
const int MaxAmmo = 30;

const int Lives = 3;

const string Name = "Ellie";

const bool IsFirefly = true;
```

The constant's type can be any of the built-in types in C#, such as `int`, `string`, or `bool`. Unlike variables, you can't use a class you created as a constant's type.

**_Tip:_** The act of creating a constant is also known as "declaring a constant".
{: .notice--info}

The name you give a constant can be anything, but there are limitations and naming conventions you should be aware of. These are discussed below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/UPNLmdRekFA?si=4KJIC9PI4O1Q8RJi" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

A constant is assigned a value using one equal sign (=) after the constant's name, followed by the value. The type will determine how the value is written.

### String Constant

A [string]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %}) constant is written using two double quotes ("") and, optionally, characters between them. Strings in C# are used to work with text.

```csharp
const string Hero = "Doomfist";

const string Role = "Tank";

const string Ultimate = "Meteor Strike";
```

### Boolean Constant

A boolean constant is written using either the `true` or `false` keywords. Booleans are like on/off switches that toggle different parts of your code on or off.

```csharp
const bool IsPlayerOne = true;

const bool HasStealthCamo = false;

const bool ShouldAttack = true;
```

### Number Constant

A [number]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %}) constant is written as a regular number with no extra formatting.

```csharp
const int DamageMultiplier = 3;

// 'decimal' is a type used with decimal numbers.
// It usually ends with an 'm'.
const decimal Income = 250.00m;

const int MaxItems = 10;
```

Numbers are used with anything that needs to be counted or when you need to perform mathematical operations like adding, subtracting, etc.

## Where should you put constants?

Constants can be written in methods or inside a class's body.

Unlike variables, constants declared in a class's body are still constants - they don't have a special name.

```csharp
// Classes you create will often be in a separate file.
// It's included here with the other code for demo purposes.

public class Enemy
{
    // A constant inside the 'Enemy' class.
    const int Health = 50;

    public void Attack()
    {
        Debug.Log("Enemy swung their sword.");
    }
}

// The class below is a 'Player' script created in Unity.
public class Player : MonoBehaviour
{
    void Start()
    {
        // A constant inside the 'Start' method.
        const string StartupMessage = "The game has started.";
    }
}
```

Assume you opened a script in Unity called `Player.cs` in your preferred editor: [Visual Studio](https://youtu.be/VcU2HGsxeII?si=ILXB_GVjOw_4-glK), [Visual Studio Code](https://youtu.be/bfvq_kTbnd8?si=Kg9KUKYCLUbkbyUH), or JetBrains Rider.

```csharp
public class Player : MonoBehaviour
{
    void Start()
    {
        const string name = "Crash Bandicoot";

        Debug.Log(name);
    }
}
```

You can create a constant inside the `Start` method and log it to the Unity console. Try doing so and observe the console after pressing play.

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

## Variables vs. Constants: What's the Difference?

Constants and variables have many similarities but are not identical.

| Variable | Constant |
| --- | --- |
| Can use `var`. | Must explicitly type `const`. `var` doesn't work. |
| Can change. | Stays the same. |
| Camel case naming. | Pascal case naming. |
| Built-in and class types. | Built-in types only. |
| Can be created without a value. | Must be assigned a value during creation. |


- **You have to explicitly type `const` before every constant.**

You can use the `var` keyword with variables in place of the type, but constants follow a stricter format where both the word `const` and the type must be included.

```csharp
var sbyte MaxLives = 3; // ❌ Can't use 'var' with constants.

const sbyte MaxLives = 3; // ✅ The correct way to declare a constant.
```

- **Constants can't be changed after they're created.**

A variable can be assigned a new value at a different part of your game's code, but a constant cannot.

If you want to update a constant's value, you can only do so **where the constant is declared**.

```csharp
const int MaxAmmo = 40;

// Assume the player just picked up some ammo.

MaxAmmo = 50; // ❌ Won't work. You'd have to change it above.
```

- **Constants are named using Pascal Case notation.**

Variables are named using camel case notation, while constants use Pascal case notation.

In **Camel Case notation**, the first letter of the first word is lowercase, and the first letter of every word after is uppercase e.g. `rotationSpeed`.

In **Pascal Case notation**, the first letter of every word is uppercase.

```csharp
const int MaxInventoryItems = 20;

const string Rank = "Elite";

const decimal MinSpeed = 5.0m;
```

- **You can't use classes as a constant's type.**

A variable can use both the [built-in types](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/built-in-types) in C# and classes you create as the type, but a constant can only use the built-in types.

```csharp
public class Enemy
{
    public void Attack()
    {
        Debug.Log("Enemy swung their sword.");
    }
}

Enemy ogre = new Enemy(); // ✅ Class type works with variables.

const Enemy Cyclops = new Enemy(); // ❌ Causes an error.
```

- **Constants must have a value when they're created.**

A variable can be declared without assigning a value to it, while a constant must have a value when you create it.

You'll need to assign a value to the variable at some point, but this difference shows the fluidity you have with variables compared to constants.

```csharp
int healthPotions; // ✅ Can be declared without value.

var magicPotions; // ❌ Can't use 'var' without assigning a value.

const int FireDamage; // ❌ Constants must have a value.

Debug.Log(healthPotions); // ❌ Error: Use of unassigned variable.
```

Variables work better for values you want to adjust through certain actions in your Unity game, such as the player's speed, health, or ammo.

Constants work better for values you want to stay the same throughout the entire game, such as the player's jump height in a realistic game, or the maximum number of enemies that can spawn in an area.

## How do you use constants in C#?

Since constants "_store_" values temporarily, you can reference that "_stored_" value any time by typing the constant's name.

Let's say you're making a game where the player has a fixed health amount, and picking up armor increases it temporarily.

You'll first create a constant called `PlayerHealth` and set it equal to any number. Let's use `100` for this example.

Next, log the number to the console three times while adding a separate number representing the strength of each armor piece picked up.

The output on the console will be as follows.

```csharp
const int PlayerHealth = 100;

// Assume the player just picked up light armor worth 25HP.

Debug.Log(PlayerHealth + 25); // Logs '125'.

// Assume the player just picked up medium armor worth 50HP.

Debug.Log(PlayerHealth + 50); // Logs '150'.

// Assume the player just picked up heavy armor worth 75HP.

Debug.Log(PlayerHealth + 75); // Logs '175'.
```
Using a constant here gave you three benefits:

1. **You didn't have to repeat `100`**. You can use the `PlayerHealth` constant where the number should be, and it's like the actual number is there instead.
2. **The constant's name provided more context**. Repeating `100` raises questions. Why is that number used in multiple places? What is it for? Why is it not another number like `50` or `90`?
3. **You don't have to worry about accidentally changing the player's health**. Using a constant ensures the player's health will always be `100`.

If you tried changing the `PlayerHealth` constant, for example, by setting it equal to `125`, you'll get an error, and the code won't run.

```csharp
const int PlayerHealth = 100;

// Assume the player just picked up light armor.

PlayerHealth = 125; // ❌ Not allowed!

Debug.Log(PlayerHealth); // This won't be executed.
```

**_Tip:_** Hover over a constant's name in Visual Studio or Visual Studio Code to see its type. This is useful in larger projects with many constants, and you want to know a particular constant's type.
{: .notice--info}

## Best Practices When Working with Constants

- **Ensure your constants are written using Pascal Case notation.**

This makes your game's code consistent with C# best practices and makes it easier to collaborate with other game developers since you'll be using a convention they're familiar with.

- **Avoid naming constants after special keywords in C#.**

You can't name a constant after one of the special keywords in C#.

If you adhere to the Pascal case naming convention, you can name constants after special keywords in C#, like `return` or `foreach`.

If you ignore it and use lowercase letters for your constant names that are identical to special keywords, you'll get an error, and your video game's code won't run.

```csharp
const int return = 100; // ❌ Doesn't work!

const int Return = 100; // ✅ Works fine.
```

You often don't need to name a constant after a keyword, so this won't be an issue 99.9% of the time.

In the extreme case you have no choice but to name a constant after a special keyword, you'll need to add an underscore at the beginning so C# doesn't confuse it with the special keywords.

- **Give your constants meaningful and descriptive names.**

Avoid naming constants using one letter or a combination of letters that makes no sense.

For example, if you have a constant representing the player's health, name the constant `Health` instead of just `H`.

A letter may work as a constant name when the constant represents a coordinate, such as the z-axis; however, a more effective approach is to use the letter and the word "axis".

**_Tip:_** Try to **keep constant names one to three words long**. When in doubt, a longer descriptive constant name is always better than a shorter one that makes no sense.
{: .notice--info}

```csharp
const int H = 100; // ❌ Avoid! What does 'H' stand for??

const int Health = 100; // ✅ Clearer and more descriptive.

const decimal CurrBal = 1000.00m; // ❌ Needs work. Not clear enough.

const decimal CurrentBalance = 1000.00m; // ✅ There you go!

const int z = 20; // ❔ Might work, but still vague.

const int ZAxisDisplacement = 20; // ✅ Splendid!
```

- **A constant's name cannot begin with a number or be composed of numbers alone.**

Doing so will result in an error, and the code won't run. 

If you must use a number, it should be at any position other than the beginning. There are some limitations when using special characters in constant names.

```csharp
const string 1Player = "Phoenix"; // ❌ Causes an error!

const string Player1 = "Phoenix"; // ✅ Number can be at the end.
const string Pla2yer = "Fade"; // ✅ Number can also be in the middle.
const string P3layer = "Brimstone"; // ✅ Or as the second character.

const string G#ame = "Valorant"; // ❌ Special characters not allowed anywhere...

const string G_ame = "Valorant"; // ✅ except underscores and...

const string @Game = "Valorant"; // ✅ an '@' sign at the BEGINNING ONLY.
```

- **Boolean constants often start with "_is_" or "_has_".**

A boolean constant can only be `true` or `false`, so appending "_is_" or "_has_" at the beginning makes it look like a question whose response is one or the other.

Given that booleans are like on/off switches to enable/disable different parts of your Unity game's code, they'll need to change often, so a variable might be a better choice.

Regardless, if you find a scenario where you need a boolean constant, it's good practice to append "_is_" or "_has_" to its name.

```csharp
const bool IsOnMission = true;

// A sneak peek into conditional statements.
if (IsOnMission)
    Debug.Log("Good luck, Soldier.");
```

You don't always have to start boolean constants with "_is_" or "_has_" - it's merely a recommendation for the sake of consistency.

If using these prefixes makes the constant more confusing or if a different name works better, you can name it something else.

For example, you can name the constant `PlayerIsAlive` instead of `IsPlayerAlive` if you prefer, or use `Enraged` instead of `IsEnraged`.

You'll see how these names make understanding code easier when you start working with conditional statements.

## What's the difference between a constant and a `readonly` variable?

You can only mark a variable as `readonly` when it's declared inside a class's body and not inside a method. These kinds of variables are known as fields.

A `readonly` variable is similar to a constant in that its value also cannot be changed after creation - in most places, at least.

The main difference is that a constant's value can't be changed anywhere in your game's code **except where it's declared**, while a `readonly` variable's value can be changed in two places:

1. Where it's declared.
2. In the class's constructor.

```csharp
public class Enemy
{
    // This is a variable in the class's body i.e. a field.
    private readonly string _type;

    const int Health = 50;

    // This is a class's constructor.
    public Enemy()
    {
        _type = "Tank"; // ✅ 'readonly' variable can be changed here.

        Health = 100; // ❌ Constant can't be changed here.
    }

    public void Attack()
    {
        _type = "Assault"; // ❌ Can't change it in a method.

        Health = 200; // ❌ Can't change constant here either.

        Debug.Log("Enemy swung their sword.");
    }
}
```

Classes, fields, and modifiers, such as `readonly`, are discussed in more detail in separate articles.

### Recap

- Constants are like mini-storage locations to store temporary data.

- They're named using Pascal Case notation.

- A constant's value can only be changed where it's declared but remains the same throughout your game.

- Constants can be declared inside methods or in a class's body.

- They must start with the word `const`.

This article is the second in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses numbers and their role in your game's code.

Here's the complete list:

1. [A Game Developer's Guide to Variables in C#]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %})
2. A Game Developer's Guide to Constants in C# _(you are here)_
3. [A Game Developer's Guide to Numbers in C#]({{ site.baseurl }}{% post_url 2025-09-21-game-dev-guide-to-constants-in-c-sharp %})
4. [A Game Developer's Guide to Operators in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %})
5. [A Game Developer's Guide to Strings in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %})
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