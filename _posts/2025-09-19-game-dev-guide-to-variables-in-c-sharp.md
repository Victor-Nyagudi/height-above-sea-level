---
title: A Game Developer's Guide to Variables in C#
categories: C#
tags: beginner-c# scripting
image:
    path: /assets/images/variables_article/variables_article_header_img.jpg
    thumbnail: /assets/images/variables_article/variables_article_thumbnail.jpg
---

A variable in C# can be thought of as **a mini storage location for temporary data you plan on reusing** while building a video game in the [Unity Game Engine](https://youtu.be/kOo1CaDdCF0?si=m_SoO0x0rxHZoHEL).

Variables are fundamental to any video game and make up a large percentage of the code you'll write, whether by hand or using visual scripting tools.

If you're a visual learner, you can watch the video version of this post below.

<div class="responsive-embed responsive-embed-16by9">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/lm5JnW-yNng?si=GB3tonPVpoQQQbko" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## How do you create a variable in C#?

There are three simple steps to creating a variable.

1. Write the variable's type.

2. Write the variable's name.

3. Give the variable a value.

```csharp
// 'int' is the type.
// 'number' is the name.
// '1' is the value.
int number = 1;

int anotherNumber = 2;

string name = "Tom";

bool isLearning = true;
```

The variable's type can be one of the pre-existing types in C#, such as `int`, `string`, or `bool`, otherwise known as **primitive types**, or types you create via classes.

**_Tip:_** The act of creating a variable is also known as "declaring a variable".
{: .notice--info}

Even though you can give the variable any name you want, there are certain restrictions to keep in mind and [naming conventions](https://youtu.be/UPNLmdRekFA?si=zxP9c2h1uytXMqWK) you should be aware of. These are discussed below.

A variable is assigned a value using one equal sign (=) after the variable's name, followed by the value. Different types have their values written in different ways.

### String Variables

A [string]({{ site.baseurl }}/c%23/game-dev-guide-to-strings-in-c-sharp) is written using two double quotes (") and, optionally, characters between them. Strings in C# are used to work with text.

```csharp
string name = "Kratos";

string hometown = "Sparta";

string son = "Atreus";
```

### Boolean Variables

A boolean value is written using either the `true` or `false` keywords. Booleans are like on/off switches that toggle different parts of your code on or off.

```csharp
bool isOnline = true;

bool isCooking = false;

bool hasInternet = true;
```

### Number Variables

A [number]({{ site.baseurl }}/c%23/game-dev-guide-to-numbers-in-c-sharp) value is written as a regular number with no extra formatting.

Numbers are used with anything that needs to be counted or when you need to perform mathematical operations like adding, subtracting, etc.

```csharp
int lives = 3;

// 'float' is a type used with decimal numbers.
float speed = 0.0f;

int attackDamage = 499;
```

### Custom Variable Types

The types you create will often be from the classes you also create.

For example, if you create a `Weapon` class to handle weapons in your game, you can store one "copy", commonly called an instance, in a variable.

```csharp
// Classes you create will often be in a separate file.
// It's included here with the other code for demo purposes.
public class Weapon
{
    private int _damage;

    public void Upgrade()
    {
        Debug.Log("Weapon upgraded to Level 2 damage.");
    }
}

// The class below is a 'Player' script created in Unity.
public class Player : MonoBehaviour
{
    void Start()
    {
        // 'axe' and 'sword' are variables.
        Weapon axe = new Weapon();
        Weapon sword = new Weapon();
    }
}
```

Classes are discussed in more detail in a separate post.

## Where should you put variables?

Variables are often written inside methods, but they can also be created inside a class's body. Variables created in a class's body have another name: fields.

```csharp
public class Weapon
{
    // This is a variable in the class's body i.e. a field.
    private int _damage;

    public void Upgrade()
    {
        // A variable in the 'Upgrade' method's body.
        int currentLevel = 1;

        Debug.Log("Weapon upgraded to Level 2 damage.");
    }
}
```

Fields are often used with properties, another type of variable in the class's body, to make games in Unity. These two are discussed in more detail in separate posts.

Speaking of Unity, the following code is what you see whenever you open a script in [Visual Studio](https://youtu.be/VcU2HGsxeII?si=ILXB_GVjOw_4-glK), [Visual Studio Code](https://youtu.be/bfvq_kTbnd8?si=WeKs4Cn5ttEO3Ki2), or JetBrains Rider. Assume the script you created is called `Player`.

```csharp
public class Player : MonoBehaviour
{
    void Start()
    {
        string name = "Captain Price";

        Debug.Log(name);
    }
}
```

You can create a variable inside the `Start` method and log it to the Unity console. Try doing so and observe the console after pressing play. What do you think this code will log?

**Interested in making games in Unity?** [Become a patron](https://www.patreon.com/cw/heightabovesealevel) on Patreon and gain access to cheat sheets, behind-the-scenes content, advanced scripting videos, and more.
{: .notice--primary}

## What is `var`? Why is it used with variables?

`var` is one of the special keywords in C#. It's used when creating variables as a shorter and less repetitive way compared to constantly repeating a variable's type.

Let's say you wanted to create three strings to store a character's first, middle, and last name.

You'd have to declare the `string` type before each of the variables, but with `var`, you don't need to repeat it. You can also use it with other types, such as numbers and booleans.

```csharp
string firstName = "Elena";
string middleName = "Joelle";
string lastName = "Fisher";

// Rewritten using 'var' keyword.
// These are all still 'string' types.

var firstName = "Elena";
var middleName = "Joelle";
var lastName = "Fisher";
```
Using `var` instead of manually writing each variable's type comes down to personal preference.

If you're working on a project with others, there might be documentation outlining which approach to use, so it's best to consult it.

If you're working on a personal project, you can use `var`, explicitly declare the types, or use a mix of both. Using both is safe and won't cause bugs.

By using `var`, you're telling the C# compiler to figure out what the variable's type is based on what you write on the right side of the equal sign.

If you used the correct syntax, for example, double quotes for strings, the compiler will recognize that you want to use a string and assign the type for you behind the scenes.

**_Tip:_** Hover over a variable's name in Visual Studio or Visual Studio Code to see its type. This is useful in larger projects with many different variables when you want to know a particular variable's type.
{: .notice--info}

Some of the other special keywords in C# include `return`, used in methods, `for`, `while`, and `foreach`, used in loops, and `public`, used to modify access to different parts of your code.

## How do you use variables in C#?

Since variables "_store_" values temporarily, you can reference that "_stored_" value any time by typing the variable's name.

Let's say you want to log different variations of a speed multiplier to the Unity console, for example, the number multiplied by two, three, four, etc.

You'll first create a variable called `speedMultiplier` and set it equal to any number. Let's use 1 for this example.

Next, log the number to the console three times while multiplying it by a separate number each time. The output on the console will be as follows.

```csharp
// Can you guess what type this variable is?
// Hint: Look at the previous code in this post.
var speedMultiplier = 1;

Debug.Log(speedMultiplier * 2); // Logs '2'.

Debug.Log(speedMultiplier * 3); // Logs '3'.

Debug.Log(speedMultiplier * 4); // Logs '4'.
```

Using a variable here gave you two benefits:

1. **You didn't have to repeat 1**. You can just use the `speedMultiplier` variable where the number should be, and it's like the actual number is there instead.

2. **The variable's name provided more context**. Repeating 1 raises questions. Why is that number used in multiple places? What is it for? Why is it not another number like 12 or 91?

You can also change variables any time if you want. Let's say the speed multiplier is supposed to increase to 3 every time the player picks up a speed booster.

To do so, update the `speedMultiplier` by changing the number to the right of the equal sign. This is also called "assigning it a new value".

```csharp
var speedMultiplier = 1;

// Assume the player just picked up a speed booster.

speedMultiplier = 3;

Debug.Log(speedMultiplier); // Logs '3'.
```

Variables can be used in multiple ways, but these two are common and provide a good starting point for using variables during game development in the Unity Game Engine.

## Best Practices When Working with Variables

- **Variables in C# are written using camel case notation**, where the first letter of the first word is lowercase, and the first letter of each word after that is uppercase.

```csharp
string title = "Big Boss";

float gameProgress = 46.7f;

var assaultRifle = new Weapon();
```

- **You can't name a variable after one of the special keywords in C#.**

Trying to do so will result in an error, and your video game's code won't run.

You often don't need to name a variable after a special keyword, so this won't be an issue 99.9% of the time.

In the extreme case you have no choice but to name a variable after a special keyword, you'll need to add an underscore at the beginning so C# doesn't confuse it with the special keywords.

```csharp
int return = 2; // ❌ Doesn't work!

int _return = 5; // ✅ Much better.
```

- **Give your variables meaningful and descriptive names.**

Avoid naming variables using one letter or a combination of letters that makes no sense.

For example, if you have a variable representing a player's speed, name the variable `speed` instead of just `s`.

A letter may work as a variable name when the variable represents a coordinate, such as the x or y axis; however, a more effective approach is to use the letter and the word "axis" e.g. `xAxis`.

**_Tip:_** Try and **keep variable names one to three words long**. When in doubt, a longer descriptive variable name is always better than a shorter one that makes no sense.
{: .notice--info}

```csharp
float s = 10.0f; // ❌ Avoid! What does 's' stand for??

float speed = 10.0f; // ✅ Cleaner and more descriptive.

int ammCnt = 100; // ❌ Needs work. Not clear enough.

int ammoCount = 100; // ✅ Now we're talking!

int x = 25; // ❔ Might work, but still vague.

int xAxisDisplacement = 25; // ✅ Perfect!
```

- **A variable's name cannot begin with a number or be composed of numbers alone.**

Doing so will result in an error, and the code won't run.

If you must use a number, it should be at any position other than the beginning.

There are some limitations when using special characters in variable names.

```csharp
string 1name = "Ikora"; // ❌ Causes an error.

string name1 = "Ikora"; // ✅ Number can be at the end.
string na1me = "Rey"; // ✅ Number can also be in the middle.
string n1ame = "Destiny"; // ✅ Or as the second character.

var n?me = "Ikora"; // ❌ Special characters not allowed anywhere except...

var n_ame = "Destiny"; // ✅ when the character is an underscore...

var @name = "Destiny"; // ✅ or an '@' sign at the BEGINNING ONLY.
```

- **Boolean variables often start with "is" or "has".**

Given a boolean variable can only be `true` or `false`, appending "_is_" or "_has_" at the beginning makes it look like a question whose response is one or the other.

For example, if you want to know if the player has picked a power-up, you can create a boolean variable called `hasPowerUp`.

If the player `hasPowerUp`, then the variable is `true`, and you can boost the player's attack damage.

If the player doesn't have a power-up, then the answer to the "hasPowerUp?" question is `false`, so the player's attack damage stays at the default number.

```csharp
var attackDamage = 5;

var hasPowerUp = false;

// Here's a sneak peek into conditional statements.
if (hasPowerUp)
    attackDamage = 10;
```

You don't always have to start boolean variables with "_is_" or "_has_" - it's merely a recommendation for the sake of consistency.

If using these prefixes makes the variable more confusing or if a different name works better, you can name them something else.

For example, you can name the variable `playerIsGrounded` instead of `isPlayerGrounded` if you prefer, or use `powerUpPicked` instead of `hasPowerUp`.

You'll see how these names make understanding code easier when you start working with conditional statements.

## How can I practice using variables in C#?

You can [practice using variables](https://youtu.be/oFoM-Eq96C8?si=L7m5JfMLFJI4EDGc) by logging different types of variables to the console and seeing how they appear, doing simple arithmetic and logging the result, or updating them in different ways.

Variables are one of the many concepts in the interconnected world of C#, so you'll see more use cases the more you use the programming language.

### Recap

- Variables are like **mini-storage locations to store temporary data**.

- They're **named using Camel Case notation**.

- You can use `var` instead of a variable's type when creating it.

- Variables are often **declared inside methods** but can be **declared within a class's body**.

- Boolean variables often start with "_is_" or "_has_".

Once you feel you have a good grasp of variables, read the next article on [constants in C#]({{ site.baseurl }}/c%23/game-dev-guide-to-constants-in-c-sharp).

This article is the first in a series breaking down common C# concepts used in game development with the Unity Game Engine.

The next one discusses constants and their role in your game's code.

Here's the complete list:

1. A Game Developer's Guide to Variables in C# _(you are here)_
2. [A Game Developer's Guide to Constants in C#]({{ site.baseurl }}/c%23/game-dev-guide-to-constants-in-c-sharp)
3. [A Game Developer's Guide to Numbers in C#]({{ site.baseurl }}/c%23/game-dev-guide-to-numbers-in-c-sharp)
4. [A Game Developer's Guide to Operators in C#]({{ site.baseurl }}/c%23/game-dev-guide-to-operators-in-c-sharp)
5. [A Game Developer's Guide to Strings in C#]({{ site.baseurl }}/c%23/game-dev-guide-to-strings-in-c-sharp)
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