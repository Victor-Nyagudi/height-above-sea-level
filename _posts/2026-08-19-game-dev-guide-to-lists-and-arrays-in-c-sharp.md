---
title: A Game Developer's Guide to Lists & Arrays in C#
categories: C#
tags: beginner-c# scripting
excerpt: "Inventory items. Weapons carried. Checkpoints. These are all groups of related items in a game you should store together, and lists and arrays are the perfect data structures for that. Lists and arrays in C# are examples of collections that store items."
image:
    path: /assets/images/lists_arrays_article/lists_arrays_article_thumbnail.jpg
    thumbnail: /assets/images/lists_arrays_article/lists_arrays_article_thumbnail.jpg
---

Inventory items. Weapons carried. Checkpoints. These are all groups of related items in a game you should store together, and lists and arrays are the perfect data structures for that.

Lists and arrays in C# are examples of collections that store items. They **save you the trouble of manually creating [variables]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %}) for each item**.

For example, without collections, you'd have to manually create each inventory item and keep track of it - a very tedious and unpleasant experience.

Lists and arrays group items and provide mechanisms for adding, removing, and updating them.

This article assumes you're familiar with [classes]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-classes-in-c-sharp %}), [loops]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-loops-in-c-sharp %}), and [methods]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-methods-in-c-sharp %}) because those are the areas you'll use lists and arrays most.

If you're a visual learner, you can watch the video version below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/vxeRdUW45mk?si=NgqfnN8HIIH50G3m" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

{% include toc %}

## Arrays

### How to Use Arrays in Unity

Arrays are a collection in C# that **store a fixed number of items**. The total number of items is specified during initialization and limits the maximum number of items you can include in the array.

Once you've created an array, **you can't add or remove items from it**. You can only update the existing items to new ones.

A specified type followed by an opening and closing square bracket signifies an array in C#, e.g., `int[]` or `Weapon[]`.

An array can store items of different types, e.g., `int`, [`bool`]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-booleans-in-c-sharp %}), [`string`]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %}), or classes you created. You can even have an array that stores other arrays.

There are multiple ways to create array variables, as shown below.


```csharp
var checkpoints = new byte[10]; // <- Array with 10 empty slots.

var inventoryItems = new string[] { "Wood", "Steel" }

int[] numbers = [1, 2, 3, 4, 5];

Weapon[] weapons =
{
    // Remember class constructors??
    new Weapon("Machete"),
    new Weapon("Steel Baton"),
    new Weapon("Kukri"),
};
```

You'll need to use the `new` keyword to create an array instance since arrays inherit from the pre-existing `Array` class.

You can even use arrays as [fields and properties]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-fields-and-properties-in-c-sharp %}), method return types, or method parameters.

```csharp
public class Player
{
    private string[] _inventoryItems; // <- Array field.

    // A method with an array parameter.
    public void DiscardItems(string[] items)
    {
        Debug.Log($"{items.Length} have been discarded.");
    }
}
```

You can also create an "**empty array**" with a specified number of slots but no defined items.

"Empty arrays" could be helpful if you want to update the items later. **The array isn't technically empty** because C# fills each slot with the type's default value.

For example, if you create an array of six [numbers]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %}) but don't specify the numbers, you'll end up with an array containing six 0s because `0` is the default value for numbers in C#.

```csharp
var numbers = new int[6];

// Remember the 'foreach' loop??
foreach (var number in numbers)
    Debug.Log(number);

// Output:

// 0
// 0
// 0
// 0
// 0
// 0
```
**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

### Accessing Values in Arrays

Arrays in C# are **zero-indexed** - you count their items starting from 0. For example, in an array with five items, the first item has an index of 0, the second has an index of 1, and so on.

You can [access]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-access-modifiers-in-c-sharp %}) the items using an indexer. An **indexer** is a pair of square brackets `[]` around an item's index at the end of the array's name.

```csharp
string[] agents = { "Brimstone", "Reyna", "Phoenix" };

Debug.Log(agents[0]); // Logs 'Brimstone'.
Debug.Log(agents[1]); // Logs 'Reyna'.
Debug.Log(agents[2]); // Logs 'Phoenix'.

// ❌ Trying to access 4th item in a list of 3. Causes an error.
Debug.Log(agents[3]);
```

**_Error Warning:_** If you try accessing an item whose index is higher than the last array item or lower than the first item, you'll get an `IndexOutOfRange` error.
{: .notice--danger}

### Array Methods and Properties

Each array has a `Length` property you can access using dot notation that **returns the total items it contains**. It's useful when looping through the array's items using a `for` loop.

With the array's total as the [condition]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-conditional-statements-in-c-sharp %}), the loop executes the same number of times as the total items.

```csharp
string[] legends = { "Wraith", "Seer", "Octane" };

// 'Length' property determines how many times loop executes.
for (var i = 0; i < legends.Length; i++)
    Debug.Log(legends[i]);

// Output:

// Wraith
// Seer
// Octane
```

**_Tip:_** A `for` loop is a good choice when looping through lists and arrays if you need to know each item's index.
{: .notice--info}

Arrays have some helpful built-in methods you can call while making your game in the Unity Game Engine:

- **`Sort()`** - sorts items in the array in ascending order. Works well with numbers.

- **`Reverse()`** - reverses the order of items in an array.

- **`Clear()`** - resets all items in the array to their default values, essentially "clearing" it.

- **`IndexOf()`** - returns the index of the specified item in an array.

- **`Find()`** - searches for the first item in an array that meets a specific criterion.

## Lists

### How to Use Lists in Unity

Lists in C# are collection types that **store a flexible number of items**. Unlike arrays, you can add and remove items from a list.

The `System.Collections.Generic` namespace stores lists in C#, so you'll have to **add the `using` statement at the top of the file** if you want to use them in your Unity game's scripts.

```csharp
// This line is mandatory when using lists.
using System.Collections.Generic;

List<string> elements = ["Fire", "Ice", "Water"];

var numbers = new List<float>() { 1.0f, 2.0f, 3.0f, 4.0f, 5.0f };

var weapons = new List<Weapon>(); // An empty list.
```

**_Tip:_** A namespace stores many related classes, and `using` statements grant access to them if you're working in a separate namespace.
{: .notice--info}

You declare a list's item type between angled brackets `<>` because lists are **generic**.

Generics are a broad topic, but simply put, they provide flexibility when working with C# types by letting the game developer decide which type to use.

If you see any type surrounded by angled brackets, there's a good chance that code is using generics.

You can create a list instance using the `new` keyword and store it in a variable, just like arrays.

Lists are **genuinely empty** by default, and **you can't specify the initial number of items** because the list grows and shrinks automatically as items are added and removed.

### Accessing Values in Lists

Lists in C# are also **zero-indexed**, and their items are accessible using an indexer, like in arrays.

```csharp
using System.Collections.Generic;

List<string> craftingMaterials =
[
    "Bandages",
    "Wire",
    "Duct Tape"
];

Debug.Log(craftingMaterials[0]); // Logs 'Bandages'.
```

### List Methods and Properties

Each list has a `Count` property that **returns the total number of items in the list** and is **accessed using dot notation**.

You can also loop through a list using the `for` or `foreach` loops.

For example, if the player in your Unity game collects ammo from a crate that replenishes the ammo of all weapons, you can loop through the weapons list and update each weapon's ammo value to its maximum.

```csharp
using System.Collections.Generic;

var player = new Player();

const byte MaxAmmo = 200;

// Assume the player opened a large ammo crate...

foreach (var weapon in player.Weapons)
    weapon.ammo = MaxAmmo; // <- Replenish each weapon's ammo.
```

Some of the built-in list methods you might find helpful when making a game include:

- **`Add()`** - adds a specified item at the end of the list.

- **`Remove()`** - removes a specified item from the list.

- **`Clear()`** - removes all items from the list.

- **`Contains()`** - checks if a list contains a specified item and returns `true` if it does, or `false` if it doesn't.

- **`Reverse()`** - reverses the order of items in the list.

## Lists vs. Arrays: Which Should You Use?

| List | Array|
| --- | --- |
|  Adjustable size. | Fixed size. |
| Can be genuinely empty. | Has "empty" slots with default values. |
| Found in `System.Collections.Generic` namespace. | Found in `System` namespace. |
| `Count` property for total items. | `Length` property for total items. |
| Declared using `<>` e.g.  `List<int>` | Declared using `[]` e.g. `int[]` |
| Zero-indexed. | Zero-indexed. |

Despite the similarities between lists and arrays, there are situations where one works better than the other.

Use an **array** if:

- You're working with a **fixed number of items**.

- You **know how many items you'll be working with**.

- You can **keep track of the "empty" slots** (items with default values) when updating arrays.

Use a **list** if:

- You're working with a **dynamic number of items**.

- You plan to **add and remove items** often.

- You prefer dealing with **a genuinely empty collection** instead of one that still has values when "empty".

## Recap

- Lists and arrays are collection types that **store related items**.

- Arrays store a **fixed number** of items.

- Lists store a **dynamic number** of items.

- Both lists and arrays are **zero-indexed**, meaning you count each item's position starting from 0.

- You can **use loops to manipulate items** in lists and arrays.

This article is the fourteenth in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses how to use [dates and times]({{ site.baseurl }}{% post_url 2026-08-20-game-dev-guide-to-dates-and-times-in-c-sharp %}) in your game.

Here's the complete list of articles in the series:

1. [A Game Developer's Guide to Variables in C#]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %})
2. [A Game Developer's Guide to Constants in C#]({{ site.baseurl }}{% post_url 2025-09-21-game-dev-guide-to-constants-in-c-sharp %})
3. [A Game Developer's Guide to Numbers in C#]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %})
4. [A Game Developer's Guide to Operators in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %})
5. [A Game Developer's Guide to Strings in C#]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %})
6. [A Game Developer's Guide to Booleans in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-booleans-in-c-sharp %})
7. [A Game Developer's Guide to Enums in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-enums-in-c-sharp %})
8. [A Game Developer's Guide to Conditional Statements in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-conditional-statements-in-c-sharp %})
9. [A Game Developer's Guide to Loops in C#]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-loops-in-c-sharp %})
10. [A Game Developer's Guide to Classes in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-classes-in-c-sharp %})
11. [A Game Developer's Guide to Access Modifiers in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-access-modifiers-in-c-sharp %})
12. [A Game Developer's Guide to Fields & Properties in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-fields-and-properties-in-c-sharp %})
13. [A Game Developer's Guide to Methods in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-methods-in-c-sharp %})
14. A Game Developer's Guide to Lists & Arrays in C# _(you are here)_
15. [A Game Developer's Guide to Dates & Times in C#]({{ site.baseurl }}{% post_url 2026-08-20-game-dev-guide-to-dates-and-times-in-c-sharp %})