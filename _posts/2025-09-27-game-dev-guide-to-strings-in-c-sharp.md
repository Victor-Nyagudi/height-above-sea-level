---
title: A Game Developer's Guide to Strings in C#
categories: C#
tags: beginner-c# scripting
excerpt: "Whether you're working with non-playable character (NPC) names or text in your game's user interface (UI), you'll most likely run into strings in C#. Strings store and manipulate text."
image:
    path: /assets/images/strings_article/strings_article_header_img.jpg
    thumbnail: /assets/images/strings_article/strings_article_thumbnail.jpg
---

Whether you're working with non-playable character (NPC) names or text in your game's user interface (UI), you'll most likely run into strings in C#.

Strings store and manipulate text. They're the foundation of the majority of text-related code you'll write for your game made in the [Unity Game Engine](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL).

This article assumes you have some knowledge of [variables]({{ site.baseurl }}/c%23/game-dev-guide-to-variables-in-c-sharp), [constants]({{ site.baseurl }}/c%23/game-dev-guide-to-constants-in-c-sharp), and [operators]({{ site.baseurl }}/c%23/game-dev-guide-to-operators-in-c-sharp), but if you're not familiar with them, read the linked articles first.

If you're a visual learner, you can watch the video version below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/5TVhfwAB4kU?si=f_yR3JXaCEJ0nDxm" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## How do you use strings?

You'll first need to create a `string` variable before you can use it.

String variables are written using double quotes and, optionally, some text between them.

```csharp
string legend = "Wraith";

var game = "Apex Legends";
```

Most characters are allowed between the double quotes, but there are some special ones called [**escape characters**](#escape-characters) you should be aware of, which are discussed later in the post.

## What's the difference between a `char` and a `string`?

A `char` is a type in C# that's similar to a `string` but is not identical. Here are some of the differences.

| `char` | `string` |
| --- | --- |
| Stores only one character. | Can store one or more characters. |
| Written using single quotes. (' ') | Written using double quotes. (" ") |
| You can't loop through a `char`. | You can loop through a `string`. |

```csharp
char letter = 'H';
var grade = 'B';

// ❌ Strings in C# must use double quotes (" ").
string acronym = 'HASL';

// ✅ A 'string' can have multiple characters.
string letters = "HA";

// ❌ 'char' can only store one character.
char multipleLetters = 'HA';
```

**_Tip:_** When looping through a string, each character in the string will be of type `char`.
{: .notice--info}

## Working with Strings

Strings in C# are **immutable** - once you create them, you can't change them.

Let's say the player in your game can carry a sword that deals elemental damage; the elements being fire, ice, and electricity.

They can toggle each element by pressing a button, and the UI should update accordingly.

If you have a `string` variable called `activeElement` that displays the active element, changing it from `Fire` to `Ice` doesn't update the string - **it creates a new one** and assigns it to `activeElement`.

```csharp
var elementalDamage = "Fire";

// Assume player changed element.

elementalDamage = "Ice"; // ❔ This creates a new string.

// Assume player changed the element again.

elementalDamage = "Electricity"; // ❔ Another string is created.
```

A new string is created because strings are immutable - you can't change them - so you now end up with two strings in your Unity game's code, but are only using one.

Constantly changing strings in this way can harm your game's performance because **unused strings still consume resources**.

You could store the elements in the three different constants, then switch between them instead of constantly updating one `string` variable.

```csharp
// Enums can work too, but that's covered later.

const string Fire = "Fire";
const string Ice = "Ice";
const string Electricity = "Electricity";

// Classes are covered in detail later, but
// just go with this for now.
var viking = new Player();

// Assume the player changed the element.

viking.ElementalDamage = Fire;

// Player changed element again.

viking.ElementalDamage = Ice;
```

An enum could also work in this case, but that is covered in more detail in a separate article.

### `StringBuilder`

C# has a built-in type called a `StringBuilder` you can use for many string changes with a significantly reduced performance cost.

For example, if you want to add up to 5 stars at the end of the player's name if they complete a level perfectly, you can use `StringBuilder` to append the stars next to the player's name.

```csharp
using System.Text; // This line is required.

var sonicResult = new StringBuilder("Sonic");

// A loop can work here.
// Lines below are repeated for demo purposes.

sonicResult.Append("⭐");
sonicResult.Append("⭐");
sonicResult.Append("⭐");

Debug.Log(sonicResult); // Logs 'Sonic⭐⭐⭐'.
```

The process of joining strings together is called **concatenation**.

Aside from `StringBuilder`, you can also use the `+` operator to join two or more strings.

Using the operator is fine for joining a few strings, but it isn't as performant as `StringBuilder` for many string operations.

```csharp
var firstWord = "San";
var space = " ";
var secondWord = "Andreas";

// Logs 'San Andreas'.
Debug.Log(firstWord + space + secondWord);
```
**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

## Interpolated Strings

Let's say you have the word "_wood_" and a number next to it in your Unity game's UI. Every time the player collects some wood, the number should increase.

You can use an interpolated string to display both the number and the word "_wood_" such that as the number changes, the string shows the updated number.

**_Tip:_** Interpolated strings are part of [**format strings**](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/strings/#format-strings) - strings whose content is determined dynamically when the game is running.
{: .notice--info}

Interpolated strings **must** begin with a `$`, and the variable counting wood collected **must** be surrounded by curly braces "{ }".

```csharp
var totalWood = 10;

// Logs 'You have 10 wood in your inventory'.
Debug.Log($"You have {totalWood} wood in your inventory.");

totalWood += 20; // Player picked up '20' wood.

// Logs 'You have 30 wood in your inventory'.
Debug.Log($"You have {totalWood} wood in your inventory.");
```

This is different from assigning a `string` variable a new value and doesn't have as big a performance hit.

## Escape Characters

If you try writing double quotes inside a string, you'll get an error because C# doesn't understand all the double quotes you're using - all it knows is that a string should only have double quotes at the beginning and end.

You may also notice that pressing <kbd>Enter</kbd> when creating a string variable doesn't move the text to the next line in your game.

These **unique characters that behave differently when placed inside a string** are called [escape characters](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/strings/#string-escape-sequences).

**_Tip:_** Pressing <kbd>Enter</kbd>, <kbd>Space</kbd>, or <kbd>Tab</kbd> creates a character. You can't see it, but it's there.
{: .notice--info}

To use them in a string, you **must** place a backslash "\\" before them.

For example, you can add a backslash to the double quotes in your string variable so it's displayed correctly when the NPCs in your game are quoting words someone else said.

If you want text to move to the next line, you can add `\n` where you want the new line to begin.

```csharp
// ❌ Doesn't work! You must escape double quotes inside string.
var npcDialogue = "The dragon said, "Bring me a sacrifice!"";

// ✅ No errors here.
var npcDialogue = "The dragon said, \"Bring me a sacrifice!\"";

Debug.Log(npcDialogue); // The dragon said, "Bring me a sacrifice!"
```

The act of adding a backslash before characters is called "**escaping the characters**".

If you want to include a literal backslash in your string variable, you'll also need to escape it.

## Verbatim Strings

If placing backslashes sounds tedious, you can use a string variation known as a **verbatim string**.

Replace the backslash before a double quote in a string with another double quote in a verbatim string, and both work the same.

You can also press <kbd>Enter</kbd> to move text to the next line instead of writing `\n`.

```csharp
var regularString = "The dragon said, \"Bring me a sacrifice!\"";

// ❔ Verbatim string doesn't need '\'. It replaces it with an extra double quote.
var verbatimString = @"The dragon said, ""Bring me a sacrifice!""";

Debug.Log(regularString);
Debug.Log(verbatimString);

// Both these strings will log the following:
// The dragon said, "Bring me a sacrifice!"
```

If you want to eliminate most of the extra formatting, you can use a **raw string literal** that lets you write escape characters as usual.

Raw string literals start and end with three double quotes.

```csharp
// ✅ '\' doesn't need to be escaped.
var rawStringLiteral = """Backslash can be put in here: \""";

// ❌ Causes an error. '\' must be escaped i.e. written as '\\'.
var regularString = "Backslash can be put in here: \";
```

[Raw string literals have some rules](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/strings/#raw-string-literals) you'll need to follow to prevent causing errors in your game's code.

**_Tip:_** You can also insert variables inside verbatim strings and raw string literals by starting with `$` and wrapping the variable in curly braces "{ }".
{: .notice--info}

## Some Useful String Methods

Methods are covered in more detail in a separate post, but it's worth mentioning some of them now to give you more context on how to better work with strings.

Here are some useful built-in string methods you'll use when making a game in Unity.

- **`StartsWith()`**: checks if a string starts with a specified character or word.

- **`EndsWith()`**: checks if a string ends with a specified character or word.

- **`Trim()`**, **`TrimEnd()`**, **`TrimStart()`**: removes spaces from the string's beginning and end, the end alone, or the beginning alone, respectively.

- **`Split()`**: splits the string into words or characters.

- **`ToUpper()`**, **`ToLower()`**: converts all the letters to uppercase or lowercase, respectively.

```csharp
var game = "Stardew Valley";

Debug.Log(game.StartsWith("v")); // Logs 'false'.
Debug.Log(game.EndsWith("y")); // Logs 'true'.

Debug.Log(game.ToUpper()); // Logs 'STARDEW VALLEY'.
Debug.Log(game.ToLower()); // Logs 'stardew valley'.

var assassin = " Ezio Auditore ";

Debug.Log(assassin.TrimEnd()); // Logs ' Ezio Auditore'.
Debug.Log(assassin.TrimStart()); // Logs 'Ezio Auditore '.
Debug.Log(assassin.Trim()); // Logs 'Ezio Auditore'.
```

### Recap

- Strings in C# are used when working with text.

- They are **immutable** - once you create them, you can't change them.

- Use the `StringBuilder` class when making many string changes for better performance.

- **Escape characters** in a string are characters that must have a backslash "\\" before them to work correctly.

- You can use **interpolated strings** for values that change while the game is running.

This post is the fifth in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses how to use booleans and is a prerequisite for working with conditional statements.

If you feel comfortable with strings and are ready for the next challenge when working with text, check out [regular expressions](https://youtu.be/Jd3YyiJj8aM?si=Bol89ziajIyO9488).

Here's the full list of posts in the series:

1. [A Game Developer's Guide to Variables in C#]({{ site.baseurl }}/c%23/game-dev-guide-to-variables-in-c-sharp)
2. [A Game Developer's Guide to Constants in C#]({{ site.baseurl }}/c%23/game-dev-guide-to-constants-in-c-sharp)
3. [A Game Developer's Guide to Numbers in C#]({{ site.baseurl }}/c%23/game-dev-guide-to-numbers-in-c-sharp)
4. [A Game Developer's Guide to Operators in C#]({{ site.baseurl }}/c%23/game-dev-guide-to-operators-in-c-sharp)
5. A Game Developer's Guide to Strings in C# _(you are here)_
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