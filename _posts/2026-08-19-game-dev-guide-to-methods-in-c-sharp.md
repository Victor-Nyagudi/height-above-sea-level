---
title: A Game Developer's Guide to Methods in C#
categories: C#
tags: beginner-c# scripting
excerpt: "Methods, sometimes called functions, perform actions in a game. If you want the player to run, jump, attack, heal, reload, or perform any other action, you'll most likely use one. Methods are named using verbs - words that represent actions."
image:
    path: /assets/images/methods_article/methods_article_thumbnail.jpg
    thumbnail: /assets/images/methods_article/methods_article_thumbnail.jpg
---

Methods, sometimes called functions, **perform actions in a game**. If you want the player to run, jump, attack, heal, reload, or perform any other action, you'll most likely use one.

Methods are **named using verbs** - words that represent actions. Examples include `Run`, `Jump`, `Attack`, or `Reload`.

This article assumes you're familiar with [classes]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-classes-in-c-sharp %}), [access modifiers]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-access-modifiers-in-c-sharp %}), and [variables]({{ site.baseurl }}{% post_url 2025-09-19-game-dev-guide-to-variables-in-c-sharp %}).

If you're a visual learner, you can watch the video version below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/6LvkfBS10YM?si=4pfIkarp9yTvRGNO" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

{% include toc %}

## How to Use C# Methods in Unity

You typically declare methods in a class along with [fields and properties]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-fields-and-properties-in-c-sharp %}). These are collectively known as **class members**.

A method consists of three mandatory sections and an optional one:

1. **Access modifier** - can be `public`, `private`, etc.

2. **Return type** - determines whether a method performs an action or performs an action and returns the result.

3. **Name** - each method needs a name.

4. **Parameters (optional)** - values used to alter the method's behavior. Each parameter requires a type and a name.

These four sections are the **method signature**.

```csharp
/*
    * 'public' - access modifier
    * 'void' - return type
    * 'Run' - name
    * 'speed' - parameter
*/
public void Run(float speed)
{
    Debug.Log($"The player is running at {speed} miles per hour.");
}
```

**_Tip:_** Methods are named using the Pascal Case [naming convention](https://youtu.be/UPNLmdRekFA?si=VT5ONjd2_T-RxCwb), where the first letter of each word is upper case.
{: .notice--info}

You can name a method anything you want, but it's best practice to **name it based on the action it performs**.

Parameters should also have descriptive, meaningful names, not ambiguous single letters.

Methods declared inside a class without the `static` modifier are called **instance methods**. You can only use them after creating an instance of the class.

If a method is `public`, you can access it using **dot notation** on the class instance and invoke it by placing an opening and a closing parentheses after its name.

**Invoking a method** executes the code between its curly braces. If you don't invoke a method, the code inside it never executes.

**_Tip:_** Invoking a method is also known as "**calling a method**".
{: .notice--info}

```csharp
public class Player
{
    public void Run() // <- This is an instance method.
    {
        Debug.Log("The player is running.");
    }
}

var playerOne = new Player(); // <- Create a 'Player' instance.

playerOne.Run(); // <- Call/Invoke the 'Run' method.
```

A **`void` return type** means the method performs an action and doesn't return a result.

Any other type, such as `int`, `bool`, `string`, etc., means **the method returns a value of that type**.

For example, if you had an `Add` method that adds two [numbers]({{ site.baseurl }}{% post_url 2025-09-24-game-dev-guide-to-numbers-in-c-sharp %}), you'd want to use the total in other parts of the code, wouldn't you?

You can use the `return` keyword to **return the result to the code that called the method**, and it can use the result elsewhere.

```csharp
public class Calculator
{
    public int Add(int firstNumber, int secondNumber)
    {
        // Returns the result of the addition.
        return firstNumber + secondNumber;
    }
}

var calculator = new Calculator();
var result = calculator.Add(1, 2);

Debug.Log(result); // <- Logs '3' to the console.
```

### `Start` and `Update` Methods in Unity

Every [time]({{ site.baseurl }}{% post_url 2026-08-20-game-dev-guide-to-dates-and-times-in-c-sharp %}) you create a script in Unity and open it, there are usually two methods inside the class: `Start` and `Update`.

These methods exist because the script **inherits** from the `MonoBehaviour` class, hence the colon (:) and the name "_MonoBehaviour_" after your class's name to signify inheritance.

The **`Start` method is called before the first frame**, and is a good place to initialize values, access components attached to a GameObject, or perform initial setup.

Try logging a message in the Unity console in this method. The console logs the message once because Unity calls `Start` once.

```csharp
public class Vehicle : MonoBehaviour
{
    // Start is called before the first frame update.
    void Start()
    {
        Debug.Log("A simple message to be logged.");
    }

    // Update is called once per frame.
    void Update() { }
}
```

The **`Update` method is called on every frame** and is a good place to perform actions that occur continuously in your Unity game, such as movement or updating time on a clock.

Logging a message to the Unity console in this method writes it continuously until you deactivate the script because `Update` is **called on every frame**, and there are multiple frames per second when the game is running.

You don't have to create an instance of your class or the `MonoBehaviour` class to call these methods because Unity handles that for you.

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

## `static` Methods

You can use methods declared as `static` **from the class directly without creating an instance**.

`static` methods can be helpful for classes that contain short, convenient methods you can use in different areas of the code without having to instantiate the class often.

```csharp
public class Utilities
{
    public static void LogColoredMessage() // <- 'static' method
    {
        Debug.Log("<color='cyan'>Hello</color>")
    }
}

public class GameManager : MonoBehaviour
{
    void Start()
    {
        // You can use 'static' methods without instantiating the class.
        Utilities.LogColoredMessage();
    }
}
```

Other class members, such as properties and fields, can also be marked `static` and used in the same way.

**_Tip:_** A non-static class can have `static` members, but if a class is marked `static`, all its members must also be marked `static`.
{: .notice--info}

## Method Parameters

Method parameters, sometimes called **method arguments**, are **values supplied by the code that calls the method**.

**_Tip:_** To avoid confusion, use the word "_parameters_" when describing the values before calling the method and "_arguments_" during or after you call the method.
{: .notice--info}

The `Add` method mentioned earlier requires the code that calls it to supply the two values it should add.

If you tried calling the method without supplying those values, you'd get an error because it requires them to execute.

It's up to you, the game developer, to decide if a method should receive external values. You can always create one with no parameters.

If you're unsure whether a method needs parameters or not, ask yourself the following questions:

1. **Can the method work as intended without other values?** If yes, you don't need parameters. Otherwise, you do.

2. **Do you want other code to alter the method's behavior?** If yes, you need parameters. Otherwise, you don't.

### Optional Parameters/Arguments

If you have a method with parameters and you want it to have **some default behavior even when it doesn't receive any values**, you can use optional parameters.

Optional parameters, sometimes called default parameters, are **parameters assigned predefined values where you create the method**.

If the code calling the method doesn't supply a value, the method uses the default values.

```csharp
public class Calculator
{
    // 1 and 2 are the default/optional parameter values.
    public int Multiply(int firstNumber = 1, int secondNumber = 2)
    {
        return firstNumber * secondNumber;
    }
}

var calculator = new Calculator();
var result = calculator.Multiply(); // <- No values supplied.

Debug.Log(result); // Logs '2' because C# used the default values of 1 and 2.
```

Optional parameters are helpful when you want to give external code the option to change a method's behavior.

For example, suppose the main character in your Unity game uses a light attack by default when you press the square button and a heavy attack when you press the square button and the right trigger. In that case, you can use an optional parameter to accomplish this.

```csharp
public class Player
{
    // 'type' is an optional parameter.
    public void Attack(string type = "Light")
    {
        Debug.Log($"The player performed a {type} attack.");
    }
}
```

**_Tip:_** If you use optional parameters with required parameters together, **the optional ones must come after the required ones**.
{: .notice--info}

### Named Parameters/Arguments

When calling a method in C#, you must supply values in the order they are declared.

For example, if the first parameter is a [string]({{ site.baseurl }}{% post_url 2025-09-27-game-dev-guide-to-strings-in-c-sharp %}) and the second is a [boolean]({{ site.baseurl }}{% post_url 2026-08-18-game-dev-guide-to-booleans-in-c-sharp %}), the code calling the method must supply a `string` value first then a `bool` value. **Changing the order results in an error**.

These are called **positional parameters**. They receive values in the order they're declared.

If you forget the order, you can use **named arguments**. Named arguments can be **supplied in any order as long as all your arguments are named**. Each argument must use the same name as the parameter.

```csharp
public class Player
{
    public void Attack(string type, byte damage, bool IsElemental)
    {
        // Code to perform an attack goes here...
    }
}

var playerOne = new Player();

// You can supply named arguments in any order.
playerOne.Attack(type: "Heavy", IsElemental: true, damage: 200);
```

If you want to **use both named and positional arguments**, you must supply the values in the same order as the method parameters, and named arguments must be towards the end.

## Method Overloading

If you want a variation of a method, for example, an attack that deals regular damage and another that deals elemental damage, you can overload the method.

Method overloading involves **creating multiple methods with the same name but different parameters and potentially different return types**.

```csharp
public class Player
{
    public void Attack()
    {
        // Code to perform regular attack goes here...
    }

    public void Attack(string element) // <- Method overload.
    {
        // Code to perform elemental attack goes here...
    }
}

var playerOne = new Player();

playerOne.Attack(); // <- Calls the first attack method.
playerOne.Attack(element: "Fire"); // <- Calls the second attack method.
```

Each method with the same name is called a **method overload**, and you can use the overloads similarly to the first one, adjusting the arguments accordingly.

For example, if you have two overloads - the first with one parameter and another with two - and supply one argument when calling the method, the first overload is automatically used. If you provide two, C# uses the second.

## Scope

Variables declared inside a method are only accessible within that method. Trying to use them anywhere else causes an error.

**The area in which a variable, method, field, etc., is accessible is called its scope**.

**_Tip:_** As a rule of thumb, think of the curly braces surrounding code blocks as a fence. **Anything the fence surrounds is usable only in that area**. Anything outside it can enter and leave the area at any time.
{: .notice--info}

## Recap

- Methods **perform actions in a game**.

- They're named using the **Pascal Case naming convention**.

- A **method's signature** consists of its access modifier, return type, name, and any declared parameters.

- Methods can have **optional and named parameters**.

- A method can be **overloaded to create variations**.

This article is the thirteenth in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses how to use [lists and arrays]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-lists-and-arrays-in-c-sharp %}) to work with groups of items in your game.

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
13. A Game Developer's Guide to Methods in C# _(you are here)_
14. [A Game Developer's Guide to Lists & Arrays in C#]({{ site.baseurl }}{% post_url 2026-08-19-game-dev-guide-to-lists-and-arrays-in-c-sharp %})
15. [A Game Developer's Guide to Dates & Times in C#]({{ site.baseurl }}{% post_url 2026-08-20-game-dev-guide-to-dates-and-times-in-c-sharp %})