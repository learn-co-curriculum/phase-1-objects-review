# Objects Review

## Learning Goals

- Review JavaScript `Object`s
- Review how to access values stored in an `Object`

## Introduction

Objects In JavaScript give us a way to store data that can range from very
simple to deeply nested and complex. As you continue through the program, you
will find yourself writing code that accesses and modifies objects often. It can
be a bit tricky at first, but as with pretty much everything you're learning,
the more you practice the easier it will get.

In this lesson, we'll review the basics of what objects are and how to work with
them. You will also get an chance to practice accessing object properties.

## What is an Object

A JavaScript `Object` is a data structure that consists of one or more
_properties_ bounded by curly braces. Each property consists of two elements, a
`key` and a `value`:

```js
const obj = { key: value };
```

The values can be of any data type, including primitive values, arrays, and
other objects.

If an object has multiple properties, they are separated by commas:

```js
const obj = {
  key1: value1,
  key2: value2,
};
```

Objects can also have keys that point to a _function_ as their value:

```js
const obj = {
  key1: "value1",
  key2: "value2",
  key3: function() {
    console.log("I am a method")
  },
};
```

Because `key3` points to a function, we refer to it as a `method` rather than a
`property`.

An object containing a key that points to another object is referred to as a
_nested_ object.

```js
const obj = {
  key1: value1,
  key2: value2,
  key3: {
    innerKey: innerValue,
  },
};
```

There is no limit to how deeply nested our objects can be.

## Accessing Values Stored in Objects

There are two options for accessing values stored in an Object: _dot notation_
and _bracket notation_.

### Dot Notation

Let's consider this Object:

```js
const address = {
  street: {
    line1: "11 Broadway",
    line2: "2nd Floor",
  },
  city: "New York",
  state: "NY",
  zipCode: "10004",
};
```

Note that `address` has four properties at the top level, with keys `street`,
`city`, `state`, and `zipCode`. The `street` key points to a nested object with
`line1` and `line2` keys.

To access the value associated with the properties at the top level using dot
notation, you would simply append a dot then the name of the key to the variable
name:

```js
address.street;
//=> { line1: "11 Broadway", line2: "2nd Floor" }

address.city;
//=> "New York"

address.state;
//=> "NY"

address.zipCode;
//=> "10004"
```

Note that `address.street` returns the nested object. To access those values,
you first need to access the key that points to the inner object ("street"),
followed by another dot and the key for the nested value you want:

```js
address.street.line1;
//=> "11 Broadway"

address.street.line2;
//=> "2nd Floor"
```

With more deeply nested Objects, you can continue to "drill down", adding a dot
and a key name at each level.

We also access _methods_ using dot notation. Let's add a method to our `address`
object:

```js
const address = {
  street: {
    line1: "11 Broadway",
    line2: "2nd Floor",
  },
  city: "New York",
  state: "NY",
  zipCode: "10004",
  whereILive: function () {
    console.log("I live in NY!")
  },
};
```

```js
address.whereILive();
// => I live in NY!
```

Adding the parentheses _executes_ the method. If we just used
`address.whereILive`, that would return the method itself:

```js
address.whereILive;
// => f () { console.log("I live in NY!") }
```

### Bracket Notation

With bracket notation, the variable name is followed by a pair of square
brackets containing the name of the key **inside quotes**. For nested Objects,
you chain the square brackets together:

```js
address["street"];
//=> { line1: "11 Broadway", line2: "2nd Floor" }

address["street"]["line1"];
//=> "11 Broadway"

address["street"]["line2"];
//=> "2nd Floor"

address["city"];
//=> "New York"

address["state"];
//=> "NY"

address["zipCode"];
//=> "10004"
```

We recommend using dot notation to access values in Objects any time you can.
Dot notation is cleaner and easier to read. But there are a couple of cases in
which dot notation will not work.

The first case is if you are using keys that don't follow JavaScript's variable
naming rules, e.g., if they contain spaces, punctuation or symbols or start with
a number. If they do, you'll need to use bracket notation and wrap the key name
in quotes. But as long as you avoid nonstandard key names, dot notation should
work fine most of the time.

The second case is if you're accessing properties dynamically, using a variable
name. We'll learn more about this in the next lesson. Before we move on, though,
let's summarize how to use dot notation and bracket notation:

#### Using Dot Notation

```js
address.state;
// => "NY"
```

When using dot notation, JavaScript treats what comes after the dot as a bare
word, similar to how variable names are treated. When you run the code above,
JavaScript first looks for a _variable_ with the name `address`, then, within
the object, looks for a _key_ with the name `state`.

#### Using Bracket Notation with a Literal Value

```js
address["state"];
// => "NY"
```

This line of code works exactly the same as the dot notation version. With
bracket notation, because the value in the brackets is enclosed in quotes,
JavaScript will look for a key with the literal name `state`.

#### Using Bracket Notation with a Bare Word

```js
address[state];
```

Here, JavaScript is going to _evaluate_ what's inside the brackets, i.e., it's
going to look for a _variable_ called `state` and use that variable's value as
the key name. In our example, this will return `undefined`, because there is no
variable with the name `state`. If, on the other hand, we stored the value
"state" in a variable, we could then use that variable in the square brackets
and it would return the value we're looking for:

```js
const whatIWant = "state";
address[whatIWant];
// => "NY
```

The example above is a little silly: why would we create a variable to hold the
name of a key and access the property using the variable rather than the key
name itself? In general — i.e., when we're accessing the values manually — we
wouldn't. But if we want to access the properties in our object _dynamically_,
we need to use variables. We'll learn how to do that in the next lesson.

## Practice Accessing Information in a Complex Object

The `petHotelGuests` object below is how we keep track of — you guessed it — the
current guests of our pet hotel. Let's practice accessing information in our
object.

```js
const petHotelGuests = {
  dogs: [
    { name: "Spinach",
      breed: "Shiba Inu",
      "age in years": 5,
      commands: ["sit", "stay", "shake"],
      speak: function () {
        console.log("");
      },
    },
    { name: "Stella",
      breed: "Miniature Schnauzer",
      "age in years": 15,
      commands: ["sit", "down"],
      speak: function () {
        console.log("ArfArfArf");
      }
    },
    { name: "Tater",
      breed: "Mutt",
      "age in years": 0,
      commands: [],
      speak: function () {
        console.log("Bowwow");
      }
    }
  ],
  cats: [
    { name: "Tashi",
      breed: "Maine Coon",
      "age in years": 2,
      speak: function () {
        console.log("Purrrrrrr");
      }
    },
    {
      name: "Pongo",
      breed: "Domestic Shorthair",
      "age in years": 9,
      speak: function () {
        console.log("mrrow?");
      }
    }

  ],
  guineaPigs: [
    {
      name: "Bingo",
      breed: "American",
      "age in years": 3,
      speak: function () {
        console.log("Wheek wheek");
      }
    }
  ],
  other: [
    { name: "Fluffy",
      species: "Hamster",
      "age in years": 1,
      speak: function () {
        console.log("Squeeeee");
      }
    }
  ]
}
```

<details><summary><b>Access the name of the first dog guest</b></summary>
  <code>const dogsArray = petHotelGuests.dogs;</code><br/>
  <code>const firstDog = dogsArray[0];</code><br/>
  <code>firstDog.name;</code><br/>
  <p>Note that we've created a variable to save the value at each step here. This is not required, of course: you <em>could</em> get the value needed with a single line of code. However, when you're learning, saving intermediate values can make your code easier to understand and help you catch errors more easily. Until you feel comfortable accessing values in complicated objects, we recommend saving intermediate values as you go.</p> 
</details>

<details><summary><b>Access the age of the <em>last</em> cat guest. Make sure your code works no matter how many cat guests we currently have.</b></summary>
  <code>const catsArray = petHotelGuests.cats;</code><br/>
  <code>const lastCat = catsArray[catsArray.length - 1];</code><br/>
  <code>lastCat["age in years"];</code><br/>
  <p>Here we're using the <code>length</code> property of the array to dynamically access the last element.</p> 
</details>

<details><summary><b>List the species of the first "other" guest and have them speak</b></summary>
  <code>const firstOther = petHotelGuests.other[0];</code><br/>
  <code>firstOther.species;</code><br/>
  <code>firstOther.speak();</code><br/>
  <p>Here we were feeling a bit more comfortable accessing information in our object so we only saved one intermediate result instead of two.</p>
</details>

Try out a few others on your own before moving on!

## Conclusion

In this lesson, we reviewed the basics of objects and got an opportunity to
practice accessing object properties and executing methods. Make sure you're
comfortable with the examples in this lesson before moving on. It will make it
easier to understand the more complex material we'll be tackling next.

## Resources

- [MDN: Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
