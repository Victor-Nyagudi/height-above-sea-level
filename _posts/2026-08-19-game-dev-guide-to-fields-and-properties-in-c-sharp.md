---
title: A Game Developer's Guide to Fields & Properties in C#
categories: C#
tags: beginner-c# scripting
excerpt: "Fields and properties tell you more about a class. They're technically variables, so they're like mini-storage locations for any information related to the class. Since classes are declared using nouns, think of fields and properties as the adjectives."
image:
    path: /assets/images/fields_properties_article/fields_properties_article_thumbnail.jpg
    thumbnail: /assets/images/fields_properties_article/fields_properties_article_thumbnail.jpg
---

Fields and properties **tell you more about a class**. They're technically [variables]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %}), so they're like mini-storage locations for any information related to the class.

Since classes are declared using nouns, think of fields and properties as the adjectives.

For example, if the game you're making in the [Unity Game Engine](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL) has non-playable villager characters (NPCs), you can create a `Villager` class to store all the code related to villagers.

Each villager will need a name, an occupation, and some money. These three will become the `Villager` class's fields or properties because they're telling us more about each villager.

This article assumes you understand how to work with [classes]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-classes-in-c-sharp %}) and [access modifiers]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-access-modifiers-in-c-sharp %}) in C#.

If you're a visual learner, you can watch the video version below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/OzFI5Bw-CW4?si=iJ5GnSgYSpUl6q3D" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

{% include toc %}

## Fields in C# Explained

Fields are part of a class's implementation and should therefore be marked `private`. Doing otherwise isn't guaranteed to break your game's code, but it's a recommended practice to prevent bugs.

```csharp
public class EnemySoldier
{
    // These are fields.
    private sbyte _health;

    private string _role;
}
```

**_Tip:_** If you don't assign a field a value, the type's default value is used. `false` is the default value for [booleans]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-booleans-in-c-sharp %}), `0` for [numbers]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %}), etc.
{: .notice--info}

**Implementation details** are details other classes shouldn't know or interact with.

For example, if you have a `Player` class that controls the main character, it'll likely have a field called `_health` representing the player's remaining health.

You wouldn't want the player's health to decrease whenever they open a door because only the `Player` class should interact with that value.

That's why you declare the `_health` field as `private`. If you changed the access modifier to `public`, the code that opens doors would now have access to the field and could accidentally manipulate it.

Placing related code inside a class while restricting access to certain parts to hide implementation details is known as **encapsulation** in programming.

Regardless, there'll be times you want to expose some information to other classes or methods, and you can do so using [properties](#properties-in-c-explained).

**_Tip:_** Since you can use a field and a variable in a method, the underscore helps you distinguish them.
{: .notice--info}

### Fields vs. Variables: What's the difference?

| Fields | Variables |
| --- | --- |
| Declared directly in classes. | Declared in methods. |
| Prefixed with underscore (`_`). | No underscore prefix. |
| Access modifier mandatory. | No access modifier. | 

Fields are declared similarly to variables except:

- You declare fields **directly in the class**, but you declare variables in methods.

- Fields and variables use the Camel Case [naming convention](https://youtu.be/UPNLmdRekFA?si=ZS0wX2z-Hze60nE7), but **fields begin with an underscore**.

- Fields **must have an access modifier**, while variables shouldn't.

### Why Use a Field?

Fields let you **reuse code within the class**.

For example, the player in your Unity game could have a speed value that changes every time they pick up a speed booster or run across muddy terrain.

This speed can be 5 miles per hour for demo purposes, and the `Player` class will have methods to increase and decrease the speed.

Without a field, you'd have to create a variable in each method to represent the initial speed, assign 5 to the variable, and adjust it in multiple places.

```csharp
public class Player
{
    // Remember what access modifier this method will have??
    int IncreaseSpeed()
    {
        var speed = 5;

        speed += 5; // Remember this operator??

        return speed;
    }

    private int DecreaseSpeed()
    {
        var speed = 5; // <- This variable is created in two places.

        speed -= 5;

        return speed;
    }
}
```

This kind of code is fragile because if you change the initial speed to 10 in one method and leave it at 5 in another, the initial speed is inconsistent.

A better approach would be to declare a `_speed` field and use it in the methods, so you can adjust the initial speed in one place and have the change reflected everywhere.

```csharp
public class Player
{
    private int _speed = 5; // <- Field is created once.

    int IncreaseSpeed()
    {
        _speed += 5;

        return _speed;
    }

    private int DecreaseSpeed()
    {
        _speed -= 5;

        return _speed;
    }
}
```

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

### Field Initialization

The process of **giving a field a value** is known as field initialization. It occurs on the same line you create the field, inside the class's constructor, or in a method.

```csharp
public class HealingItem
{
    private sbyte _healthAdded = 50; // <- Initialized on creation line.

    private string _type;

    private bool _isAvailable;

    public HealingItem(string customType)
    {
        _type = customType; // <- Field initialized in class constructor.
    }

    public void MakeAvailable()
    {
        _isAvailable = true; // Field initialized in a method.
    }
}
```

In addition to the access modifier, you can also mark a field as `readonly`.

You can initialize a `readonly` field in **only two places**:

- On the same line that you declared it.

- In the class's constructor

```csharp
public class Tank
{
    // ✅ 'readonly' field can be initialized here.
    private readonly byte _shields = 250;

    public Tank(byte customShields)
    {
        // ✅ The field can also be initialized in the constructor.
        _shields = customShields;
    }

    public void BoostDefense()
    {
        _shields = 500; // ❌ Can't initialize the field here.
    }
}
```

**_Tip:_** If you initialize a `readonly` field on the line you declared it **and** in the class's constructor, the initialization in **the class's constructor overrides the earlier one**.
{: .notice--info}

### Fields in the Unity Editor

**A common mistake in Unity tutorials** is declaring a field as `public` solely to expose it in the Unity Editor. Doing so may show it in the Unity Editor, but it could open the door for bugs in your Unity game's code in the future.

A better solution is to keep the field `private` and place the **`[SerializeField]` attribute** above it to expose it in the _Inspector_ window so you can manipulate it while respecting the encapsulation principle.

```csharp
public class Player : MonoBehaviour
{
    public float _speed; // ❌ Fields should be 'private'.

    [SerializeField] // ✅ Shows field in Unity while still 'private'.
    private float _rotationSpeed;

    // ✅ The attribute can be placed on the same line.
    [SerializeField] int _damage;
}
```

## Properties in C# Explained

Properties are similar to fields, but unlike fields, they're **`public` by default** and **use getters and setters (accessors)**.

If you need to expose certain parts of a class to other classes, it's better to use a property instead of a field.

The earlier example mentioned a `Villager` class for NPCs. Let's say you want to spawn farmer villagers in a particular area.

Before you spawn any villagers, you'll first need to know their occupation. If their occupation is `private`, there's no way for the code spawning NPCs to know which villager is a farmer.

Instead of using a `private` field for the occupation, use a `public` property. Using a property automatically **creates a `private` backing field behind the scenes**.

```csharp
public class Villager
{
    // These are properties.
    public string Name { get; set; }

    public string Occupation { get; set; }

    public int MoneyHeld { get; set; }
}
```

The `get` and `set` keywords are getters and setters that **retrieve and update the value of the `private` backing field** accordingly.

**_Tip:_** Properties are **named using the Pascal Case convention**, where the first letter of each word is uppercase.
{: .notice--info}

With a property, you don't have to worry about interfering with implementation details because the property acts as a buffer between the inner class logic and the outside world.

You can think of the `private` backing field as being inside a building, and the property is the window that lets you see inside without entering the building.

### Getters and Setters

The `get` keyword represents a property's getter. It retrieves the `private` backing field's value so the outside world can see it. The setter sets and updates the `private` backing field.

For example, you could use a property to represent each villager's remaining money and update it whenever they sell items.

You can make adjustments when getting or setting a property's value inside the getter and setter code blocks.

There are no code blocks for the properties in the code above because they're **auto-implemented**.

They don't make any adjustments when getting or setting the value of the `private` backing field. They only retrieve and set it. Nothing more.

Here's what they look like when written with code blocks.

```csharp
public class Village
{
    // Auto-implemented property.
    public string Occupation { get; set; }

    // #region Long version of an auto-implemented property.
    private string _name; // <- 'private' backing field.

    public string Name // <- Property
    {
        get { return _name; }
        set { _name = value; }
    }
    // #endregion
}
```

Let's say your Unity game has an active perk granting villagers a 50% bonus on all sold items. You can adjust the setter's code to multiply the value you provided by 1.5.

```csharp
public class Villager
{
    public bool PerkIsActive { get; set; } = false;

    private float _moneyHeld; // 'private' backing field.

    public float MoneyHeld // <- Property.
    {
        get { return _moneyHeld; }

        set
        {
            if (PerkIsActive)
                _moneyHeld = value * 1.5; // <- Apply 50% bonus.

            else
                _moneyHeld = value; // <- No bonus if perk is inactive.
        }
    }
}
```

**_Tip:_** If all this is still confusing, the video version above does a great job of explaining it with more examples.
{: .notice--info}

If you need to, **you can also use access modifiers, such as `private`, `protected`, etc., on getters and setters** to control what code can interact with them.

There are other ways to achieve these gameplay mechanics, and tweaking properties is merely one of them.

## Fields vs. Properties: Which Should You Use?

| Field | Property |
| --- | --- |
| Should be `private`. | `public` by default. |
| Camel case prefixed with underscore naming. | Pascal case naming. |
| No getters and setters. | Has getters and setters. |
| Can be exposed in Unity Editor. | Can't be exposed in Unity Editor. |

Despite their similarities, fields and properties work better in different scenarios.

Use a **field** if:

- You have **code that should only be accessible within the class**.

- You want to **adjust a value in the Unity Editor**. Properties currently can't be exposed in the Unity Editor.

Use a **property** if:

- **Other parts of the code need access** to the class's information.

- You want to **make some adjustments when getting or setting fields**.

## Recap

- A field is **a variable declared directly inside a class**.

- Fields are **implementation details** and should be `private`.

- A property is **a mechanism for retrieving or manipulating a `private` backing field**.

- Properties are `public` by default.

- Use the `[SerializeField]` attribute instead of making a field `public` to expose it in the Unity Editor.

This article is the twelfth in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses how to use methods to perform specific actions in your game's code.

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
12. A Game Developer's Guide to Fields & Properties in C# _(you are here)_
13. [A Game Developer's Guide to Methods in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-methods-in-c-sharp %})
14. [A Game Developer's Guide to Lists & Arrays in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-lists-and-arrays-in-c-sharp %})
15. [A Game Developer's Guide to Dates & Times in C#]({{ site.baseurl }}{% post_url 2026-08-20-game-dev-guide-to-dates-and-times-in-c-sharp %})