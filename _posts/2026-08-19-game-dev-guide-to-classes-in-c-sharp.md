---
title: A Game Developer's Guide to Classes in C#
categories: Scripting
tags: beginner-c-sharp
excerpt: "Classes are the building blocks of any game you'll make in the Unity Game Engine. They interact with each other to create amazing gameplay mechanics. Each class in your game should handle one thing."
image:
    path: /assets/images/classes_article/classes_article_thumbnail.jpg
    thumbnail: /assets/images/classes_article/classes_article_thumbnail.jpg
---

Classes are the **building blocks** of any game you'll make in the [Unity Game Engine](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL). They interact with each other to create amazing gameplay mechanics.

**Each class in your game should handle one thing**. For example, code related to the main character, such as movement, attacking, and remaining health, will be inside one class.

Code related to an enemy ogre, such as its health, damage output, and attacks, will be in a separate class.

This article assumes you're familiar with [variables]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %}), [booleans]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-booleans-in-c-sharp %}), [numbers]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %}), and [strings]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %}).

If you're a visual learner, you can watch the video version below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/I7GYjvfSgIU?si=q2VMSeHJoLtTCZUe" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

{% include toc %}

## Classes in C# Explained

Adding a script in Unity automatically opens it in [Visual Studio](https://youtu.be/VcU2HGsxeII?si=jLs3V6OQ2aW5pIjl) or your preferred code editor with a class named the same as the script.

**A class in C# is like a blueprint**. When you create a class, you're creating a blueprint for how you'll use it in your game.

A **namespace** stores many related classes, and an **assembly** stores many namespaces. An assembly is like a large container and eventually becomes the executable file (`.exe`) that you open to run the final game.

Let's say you want to add an enemy ogre to your Unity game. After adding its 3D model to the scene, you'll attach an `Enemy` script to it.

Here's what the script `Enemy.cs` initially looks like when you open it.

```csharp
// These are 'using' statements that grant you access to code in other namespaces.
using System.Collections;
using System.Collections.Generic;
using UnityEngine; // <- 'UnityEngine' is a namespace.

public class Enemy : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {

    }

    // Update is called once per frame
    void Update()
    {

    }
}
```

The class in the script is composed of three parts:

1. **`public`** - the [access modifier]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-access-modifiers-in-c-sharp %}).

2. **`class`** - the special keyword required for class creation.

3. **`Enemy`** - the user-defined class name.

The `public` access modifier in your `Enemy` class **specifies its access level**. Using it makes the class accessible to other classes in the code.

There are other access modifiers, such as `private`, `protected`, and `internal`, discussed in more detail in a separate article.

It's mandatory to use the `class` keyword to specify that you want to create a class because other parts of the code can also start with an access modifier.

`Enemy` is the class's name and is derived from the name you used when creating the script in Unity. **Classes should be named using Pascal Case**, where the first letter of each word is upper case.

**_Tip:_** It's better to create and rename scripts in the Unity Game Engine rather than in a code editor to prevent unnecessary naming conflicts, especially when using version control like [Git](https://youtube.com/playlist?list=PLKCFltnebRSUjtriObooAkMeYmJ7ppgX7&si=6b7ANjcmCGAazEvT).
{: .notice--info}

### Class Inheritance

The colon (:) and `MonoBehaviour` aren't part of the `Enemy` class because they're part of a programming concept called **inheritance**.

`MonoBehaviour` is a class Unity provides for you to use when coding. It exists by default and lets you connect the code you write to the Unity Game Engine's code so you can manipulate 3D models, [lights]({{ site.baseurl }}{% post_url 2025-11-01-baking-lights-in-unity-getting-started %}), [audio]({{ site.baseurl }}{% post_url 2025-10-02-free-music-sfx-for-unity-games %}), visual effects, etc, before or while the game is running.

When you place a colon followed by the name of another class after your class, you can inherit the code from that other class **if that other class's access modifier permits it**.

Inheritance is why there are two [methods]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-methods-in-c-sharp %}) in the `Enemy` class you didn't add - `Start` and `Update` - because the `Enemy` class **inherited** them from the `MonoBehaviour` class.

**_Tip:_** Inheritance is one of the pillars of **object-oriented programming**.
{: .notice--info}

## What goes inside a class in Unity?

A class **tells us more about the GameObject it's attached to** and **what it can do**.

When creating a class, you should ask yourself two questions:

1. What do I need to know about the GameObject this class is associated with?

2. What is the GameObject this class is attached to supposed to do?

### Fields

You've just created an enemy, so what do you need to know about it? Well, an enemy often needs some health, a name, a difficulty level, and a way to show they're armed or not.

You can accomplish this by adding [fields]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-fields-and-properties-in-c-sharp %}) to the `Enemy` class representing that information. Simply put, **fields are variables declared directly in a class**.

```csharp
using UnityEngine; // This is mandatory to access MonoBehaviour.

public class Enemy : MonoBehaviour
{
    // These are fields.
    private sbyte _health = 100;

    private string _name = "Ogre";

    private byte _difficulty;

    private bool _isArmed;

    void Start() { } // Start is called before the first frame update

    void Update() { } // Update is called once per frame
}
```

**_Tip:_** You can also declare [constants]({{ site.baseurl }}{% post_url 2025-09-21-game-dev-guide-to-constants-in-c-sharp %}) directly inside a class. These constants don't get a special name - they're still just constants.
{: .notice--info}

A field is composed of three mandatory parts and one optional part:

1. **`private`** - the access modifier.

2. **`string`** - the field's type that can also be an `int`, `bool`, etc.  

3. **`_health`** - the field's name.

4. **An optional assigned value**. The field uses the type's default value if this is missing, e.g., `false` for booleans, or `0` for numbers.

**Fields are named using the camelCase convention prefixed with an underscore** e.g. `_woodCollected` to distinguish them from the other variables inside the class.

Fields also have an access modifier, but unlike classes, **fields should be `private`** because **they store information that other classes shouldn't know about**. A separate article discusses this in more detail.

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

### Methods

To answer the second question, an enemy should be able to attack, flee, or chase the player. You can accomplish this by adding methods to the class.

```csharp
using UnityEngine; // <- This is mandatory to access MonoBehaviour.

public class Enemy : MonoBehaviour
{
    // These are fields.
    private sbyte _health = 100;

    private string _name = "Ogre";

    private byte _difficulty;

    private bool _isArmed;

    // These are methods, including the inherited 'Start' and 'Update' methods.
    public void Attack(int damage)
    {
        // Remember interpolated strings??
        Debug.Log($"The enemy attacked and dealt {damage} damage.");
    }

    public void Flee()
    {
        Debug.Log("The target is too strong. Retreat!");
    }

    void Start() { } // Start is called before the first frame update

    void Update() { } // Update is called once per frame
}
```

A method is composed of three mandatory parts and one optional part:

1. **`public`** - the access modifier.

2. **`void`** - what the method returns after execution.

3. **`Attack`** - the method's name.

4. **`Parameters (optional)`** - more information provided to the method that influences its execution.

A method can have different access modifiers depending on your Unity game's needs.

A `void` return type means **a method does something but doesn't result in any value**. A method can return an `int`, `string`, or `bool`, among others.

Parameters are placed in the method's parentheses and are composed of **the parameter's type and a name**. A separate article discusses methods in more detail.

**_Tip:_** Some developers call method parameters "**method arguments**".
{: .notice--info}

You can add other types to a class in C#, such as events, delegates, or [enums]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-enums-in-c-sharp %}), which won't be covered here, but this article mentions them to give you more context on working with classes.

All the items inside a class are collectively called the **class's members**.

## How do you use a class in Unity?

Now that you've answered the two main questions when creating a class and are satisfied with the result, the blueprint is complete, and you can start using it.

At this point, the `Enemy` class doesn't do anything because you haven't used it yet. It's like having a complete blueprint to a house, but no house.

You'll need to use the `new` keyword to create an enemy in the code, which will connect to the ogre's GameObject via the script component.

You can do this in the `Start` method because, remember, Unity provides the `Start` and `Update` methods to let you **perform the actions before or while the game is running**.

```csharp
using UnityEngine; // <- This is mandatory to access MonoBehaviour.

public class Enemy : MonoBehaviour
{
    // Field made 'public' for demo purposes. They should be 'private'.
    public string _name = "Ogre";

    // Other methods excluded for brevity.

    // Start is called before the first frame update
    void Start()
    {
        var ogre = new Enemy();

        ogre.Attack();

        Debug.Log(ogre._name); // Logs 'Ogre' to the console.
    }

    void Update() { } // Update is called once per frame
}
```

The process of using the `new` keyword to create an enemy is called **instantiating the `Enemy` class** or **creating an instance of the `Enemy` class**; the equivalent of using the house's blueprint to build a new house.

Placing a period after the class instance gives you access to all the items with a `public` access modifier in the class. This means of accessing class members is called **dot notation**.

For demonstration purposes, you can make the fields `public` to see their values after logging them to the console.

**_Tip_**: If you want to **expose a class's information to other classes**, you can use a [property]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-fields-and-properties-in-c-sharp %}) instead of a field.
{: .notice--info}

Placing parentheses after accessing a class's method **calls the method**, i.e., executes the code inside it. Calling a method is also known as **invoking the method**.

## Class Constructor

The parentheses after the class's name represent its **constructor**. If you don't define one, C# automatically creates a default constructor for you. A class's constructor **determines how you construct class instances**.

You're currently creating an enemy with some predefined values based on what you specified in the `Enemy` class.

If you wanted to adjust each enemy's health as you create them, you can add a constructor with a health parameter, and then include the new health in the parentheses while instantiating the class.

```csharp
using UnityEngine; // This is mandatory to access MonoBehaviour.

public class Enemy : MonoBehaviour
{
    // Field made 'public' for demo purposes.
    public sbyte _health;

    // This is a constructor.
    public Enemy(sbyte customHealth)
    {
        /*
            * Assigns custom health provided during instantiation to
            * the '_health' field.
        */
        _health = customHealth;
    }

    void Start()
    {
        // 250 is the custom health provided during instantiation.
        var ogre = new Enemy(250);

        Debug.Log(ogre._health); // Logs 250 to the console.
    }

    void Update() { }
}
```

**_Tip:_** You can have multiple constructors based on how many different things you want to adjust during instantiation.
{: .notice--info}

In addition to a constructor, you can manually override each of the class's public fields or properties using the **early object initialization syntax**.

```csharp
using UnityEngine; // This is mandatory to access MonoBehaviour.

public class Enemy : MonoBehaviour
{
    // Field made 'public' for demo purposes.
    public sbyte _health;

    // This is a property.
    public string Name { get; set; }

    void Start()
    {
        var ogre = new Enemy()
        {
            _health = 200, // <- Early object initialization.
            Name = "Shrek"
        };

        Debug.Log(ogre.Name); // Logs 'Shrek' to the console.
    }

    void Update() { } // Update is called once per frame
}
```

## Recap

- Classes are like blueprints and are **the building blocks of each game**.

- A **namespace** stores many related classes.

- A class can store fields, properties, methods, events, and other types in C#, collectively called **class members**.

- You can **create an instance of a class** using the `new` keyword.

- `public` class members in an instance are **accessed using dot notation**.

This article is the tenth in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses how to use [access modifiers]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-access-modifiers-in-c-sharp %}) to control access to different parts of your game's code.

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
10. A Game Developer's Guide to Classes in C# _(you are here)_
11. [A Game Developer's Guide to Access Modifiers in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-access-modifiers-in-c-sharp %})
12. [A Game Developer's Guide to Fields & Properties in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-fields-and-properties-in-c-sharp %})
13. [A Game Developer's Guide to Methods in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-methods-in-c-sharp %})
14. [A Game Developer's Guide to Lists & Arrays in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-lists-and-arrays-in-c-sharp %})
15. [A Game Developer's Guide to Dates & Times in C#]({{ site.baseurl }}{% post_url 2026-08-20-game-dev-guide-to-dates-and-times-in-c-sharp %})