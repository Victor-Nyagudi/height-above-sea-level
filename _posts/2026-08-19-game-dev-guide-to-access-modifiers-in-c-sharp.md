---
title: A Game Developer's Guide to Access Modifiers in C#
categories: C#
tags: beginner-c# scripting
excerpt: "Access modifiers restrict or authorize access to certain parts of the game you're building in the Unity Game Engine. For example, you wouldn't want the player in a fantasy game to swing their sword every time they opened a door."
image:
    path: /assets/images/access_modifiers_article/access_modifiers_article_thumbnail.jpg
    thumbnail: /assets/images/access_modifiers_article/access_modifiers_article_thumbnail.jpg
---

Access modifiers **restrict or authorize access** to certain parts of the game you're building in the [Unity Game Engine](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL).

Controlling access is important because, as you add more gameplay mechanics, user interface (UI) behavior, and assets, the code becomes more complex, and the risk of introducing bugs increases.

For example, you wouldn't want the player in a fantasy game to swing their sword every time they opened a door.

You can use an access modifier to restrict access to the code that swings the sword only to the combat section, preventing unintended access by other areas, such as object interactions.

This article builds on the [classes article]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-classes-in-c-sharp %}) and assumes you're familiar with other C# concepts, such as [variables]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %}), [operators]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-operators-in-c-sharp %}), and [strings]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %}).

If you're a visual learner, you can watch the video version below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/m-lhhtfG1tE?si=wPXywbQ4MIz4uaRg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

{% include toc %}

## Access Modifiers in C# Explained

The following are the four common types of access modifiers in C#, organized from least restrictive to most:

1. **`public`** _(least restrictive)_

2. **`internal`**

3. **`protected`**

4. **`private`** _(most restrictive)_

There are three [other access modifiers](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers#:~:text=internal%3A%20Only%20code%20in%20the%20same%20assembly,file%20can%20access%20the%20type%20or%20member.), but you'll only ever need them in niche scenarios: `protected internal`, `private protected`, and `file`.

## `public`

Any class, [enum]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-enums-in-c-sharp %}), method, etc., marked `public` is **accessible from virtually anywhere** in your Unity game's code.

A class is a good candidate to declare `public` because it needs to interact with other classes for the game to work correctly.

Instead of using a more restrictive access modifier on the whole class when you want to limit access to some of its contents, you can keep the class `public` and apply the restrictive access modifier individually to each item.

```csharp
public class Weapon
{
    private string _damage; // <- This is a field.

    public string Name { get; set; } // This is a property.

    public void Upgrade() // <- This is a method.
    {
        Debug.Log("The weapon has been upgraded.");
    }
}
```

## `protected`

Any class or its members marked `protected` can only be **accessed from within the class or its derived classes**.

The classes article mentioned **inheritance**, one of the core C# programming concepts.

A class inheriting from another becomes the **child/derived class**, and the class it inherits from becomes the **parent/base class**.

Let's say you want to make a game in Unity that has three types of enemies: a light minion, a heavy minion, and an archer.

All these enemies will have a couple of things in common.

- A specific amount of health.

- A light attack.

- A heavy attack.

If you had scripts for each enemy, you'd end up repeating the same code for the health and attacks of each enemy type.

Code duplication increases the likelihood of introducing bugs into your game should you need to make adjustments to the code handling attacks.

Furthermore, if you wanted to add a special move to all enemies, you'd have to do so in three different places.

With inheritance, you can store all related code in an `Enemy` class and have the other scripts inherit it.

If you ever need to adjust the common behavior in all enemies, you'd do so in one place, and the changes would reflect in all the scripts.

```csharp
// You can create classes that don't derive from 'MonoBehaviour'.
public class Enemy
{
    public sbyte Health { get; set; }

    public void LightAttack()
    {
        Debug.Log("Enemy performed a light attack.");
    }

    public void HeavyAttack()
    {
        Debug.Log("Enemy performed a heavy attack.");
    }
}

public class LightMinion : Enemy
{
    /*
        * This class inherits 'Health', 'LightAttack', and 'HeavyAttack' from the
        'Enemy' class above.
    */
}

public class HeavyMinion : Enemy
{
    // This class also inherits code from the 'Enemy' class.
}
```

**_Tip:_** When you create a script in Unity, it automatically inherits from the `MonoBehaviour` class, granting you access to all its `public` or `protected` members.
{: .notice--info}

If you marked any `Enemy` class members as `protected`, you can only access them from **within** the `Enemy` class or the other three child classes.

```csharp
public class Enemy
{
    protected sbyte Health { get; set; } // <- 'protected' property.

    // Other code goes here...
}

public class LightMinion : Enemy { }

public class GameManager : MonoBehaviour
{
    void Start()
    {
        var minion = new LightMinion();

        Debug.Log(minion.Health); // ❌ 'Health' is inaccessible.
    }
}
```

This access modifier can be helpful if you want to limit control of a group of related classes to just the group.

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

## `private`

Any class members marked `private` can only be **accessed from within the class**.

For example, methods in a class that affect the player's movement are a good candidate to be marked `private` because you wouldn't want other parts of your Unity game's code to interfere with how the player moves.

Fields should also be `private` because they're **implementation details** - information that anything outside the class doesn't need to know.

**_Tip:_** Any class members without an access modifier are `private` by default.
{: .notice--info}

If you want to expose certain information in a class, you should use a `public` property instead. A separate article discusses properties in more detail.

```csharp
public class Player : MonoBehaviour
{
    private sbyte _healthPotions = 10; // ✅ Fields should be 'private'.

    public int Ammo { get; set; } = 300; // A 'public' property.

    // This method has a 'private' access modifier by default.
    void Strafe()
    {
        Debug.Log("The player is strafing.");
    }
}
```

**A common mistake in many Unity tutorials is making a field `public` solely to expose it in the Unity Editor**.
{: .notice--warning}

This approach works for short demos with little to no systems working together, but it could be troublesome for larger projects.

Keep the field `private` and place the `[SerializeField]` attribute above/before it so you can use it in the Unity Editor while reducing the risk of unintentionally introducing bugs to your game.

```csharp
public class Player : MonoBehaviour
{
    public sbyte _health; // ❌ Fields should be 'private'.

    [SerializeField] // ✅ Field is 'private' but still visible in Unity.
    private byte _speed;

    // ✅ The attribute can also be placed before the field.
    [SerializeField] private float _rotationSpeed;
}
```

By doing so, you're also adhering to the **encapsulation principle** - the act of hiding a class's implementation details and restricting access to its members.

**_Tip:_** You can't instantiate a class with a `private` constructor outside the class; only inside it. The **singleton design pattern** uses this approach.
{: .notice--info}

## `internal`

Any code marked `internal` can only be **accessed from within the same assembly**.

```csharp
internal class Soldier // <- 'internal' access modifier.
{
    public byte Health { get; set; }

    public bool IsArmed { get; set; }

    public void FireGun()
    {
        Debug.Log("The soldier fired their gun.");
    }
}
```

A **namespace** stores many related classes, and an **assembly** stores many namespaces. An assembly is what eventually becomes the executable (`.exe`) that you open to run the final game.

This access modifier may be helpful in large games with complex systems and large codebases.

Most games you'll build in Unity will be fine using either `internal` or `public` for the code you want to be accessible from anywhere.

## Bonus

There are other keywords C# doesn't consider to be access modifiers, but they behave similarly, and, to some degree, control access to code in your game.

### `sealed`

The `sealed` modifier, when applied to a class, **prevents other classes from inheriting from it**.

Sealing a class can be helpful if you're sure that deriving/inheriting from a particular class could lead to unintended behavior in your game.

```csharp
public sealed class PlayerOne { } // A sealed class.

// ❌ Can't inherit from a 'sealed' class.
public class PlayerTwo : PlayerOne { }
```

### `static`

The `static` modifier lets you **use class members without creating an instance of the class**.

It can be useful when working with utility classes - classes that store shared, helpful methods you'd otherwise repeat in multiple places.

```csharp
public static class Utilities
{
    public static string PlayerName { get; set; } = "Kyle Crane";
}

public class GameManager : MonoBehaviour
{
    void Start()
    {
        Debug.Log(Utilities.PlayerName); // Logs 'Kyle Crane'.
    }
}
```

**_Tip:_** A class can have `static` members and not be `static`, but a class declared as `static` can only have `static` members.
{: .notice--info}

### `readonly`

The `readonly` modifier, when applied to a class's fields, means **you can only change the field's value in the class's constructor**.

```csharp
public class Player
{
    private readonly byte _shields = 200;

    public void BoostStats()
    {
        _shields = 400; // ❌ 'shields' is a read-only field.
    }
}
```

## Recap

- Access modifiers **restrict or authorize access to different parts of your game's code**.

- The four most common access modifiers you'll use are `public`, `internal`, `protected`, and `private`.

- `public` grants the **most access**, while `private` is the **most restrictive**.

- Use the `[SerializeField]` attribute if you must **expose a field in the Unity Editor**, but keep it `private`.

- The `sealed`, `static`, and `readonly` modifiers also affect how code is accessed but aren't explicitly access modifiers.

This article is the eleventh in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses fields and properties in C# and their role in making a game in Unity.

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
11. A Game Developer's Guide to Access Modifiers in C# _(you are here)_
12. [A Game Developer's Guide to Fields & Properties in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-fields-and-properties-in-c-sharp %})
13. [A Game Developer's Guide to Methods in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-methods-in-c-sharp %})
14. [A Game Developer's Guide to Lists & Arrays in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-lists-and-arrays-in-c-sharp %})
15. [A Game Developer's Guide to Dates & Times in C#]({{ site.baseurl }}{% post_url 2026-08-20-game-dev-guide-to-dates-and-times-in-c-sharp %})