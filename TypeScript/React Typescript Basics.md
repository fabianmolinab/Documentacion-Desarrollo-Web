# React TypeScript: Basics and Best Practices

Fechas: January 16, 2022 1:38 PM
Tipos: Lectura
URL: https://blog.bitsrc.io/react-typescript-cheetsheet-2b6fa2cecfe2

There is no single “right” way of writing React code using TypeScript. 
 As with other technologies, if your code compiles and works, you probably did something right

That being said, there are “best practices” that you’d want to consider following, especially when writing code others will have to either [read or re-use for their own purposes](https://bit.dev/).

So, here I’m going to list some useful code-snippets that follow said “best practices”. There are a lot of them, some that you might’ve used already in the past and some that might be new. Just go through the list and make mental notes. Bookmarking this article for future reference might be a good idea as well.

## Making your components ready for sharing, with TypeScript

Example: browsing through shared React components in bit.dev

**[Bit.dev](https://bit.dev/)** has become a very popular alternative to traditional component libraries as it offers a way to “harvest” and share individual components from any codebase (to a single component hub).

By building projects using React with TS, you make sure your components are easily comprehensible to other developers (as well as to your future self). That is absolutely crucial for making them ready for sharing. It’s a great way to write maintainable code and optimize your team collaboration.

**Learn more about sharing and reusing React TS components across repos [here](https://blog.bitsrc.io/maximizing-code-reuse-in-react-35ee20ad362c):**

## create-react-app with TypeScript

```
$ npx create-react-app your-app-name --template typescript
```

If you’re more of a fan of Yarn, you can use the following command:

```
$ yarn create react-app your-app-name --template typescript
```

In either case, notice how we’re not directly using the app, rather, we’re using other tools that will download the latest version of the app whenever it’s required. This helps ensure you’re not using an outdated version.

Some of the very interesting tidbits added by TS to the language are:

## Interfaces

One of the many benefits TypeScript brings to the table, is access to constructs such as this, which allows you to define the interface of your components or even any other complex objects you might want to use with them, such as the shape your `Props` object will have (i.e how many properties and their types).

The above code ensures that whoever uses your components needs to add exactly 3 properties:

- text: which needs to be a String
- type: which needs to be a ButtonType option (I’ll cover Enums in a second)
- action: which is a simple function

> Note that we “extended” the FC (Functional Component) type with our own custom interface. That gives our function all the generic functional component definitions such as the ‘children’ prop and a return type that must be assignable to JSX.Element.
> 

If you ignore one of them or send something that’s not compatible, both the TypeScript compiler and your IDE (assuming you’re using a JavaScript specific IDE, such as Code) will notify you and won’t allow you to continue until you fix it.

> A better way to define our ExtendedButton element would be to extend a native HTML button element type like so:
> 

> But more on that topic later in this post…
> 
> 
> Also, note that when working with [Bit.dev](https://bit.dev/) or [react-docgen](https://github.com/reactjs/react-docgen), the following syntax is required to [auto-generate docs](https://blog.bitsrc.io/maximizing-code-reuse-in-react-35ee20ad362c):
> 

(The props are defined directly and explicitly using `:IButtonProps` in addition to defining the component with `:React.FC<IButtonProps>`)

## Enums

Just like with Interfaces, Enums allow you to define a set of related constants as part of a single entity.

Importing and using Enums:

Please note that *unlike* Interfaces or Types, Enums will get translated into plain JavaScript. So, for example, this:

```
Optional = "optional",Irrelevant = "irrelevant"
```

will transform into this:

```
(function (SelectableButtonTypes) {SelectableButtonTypes["Optional"] = "optional";SelectableButtonTypes["Irrelevant"] = "irrelevant";
```

A common question that newcomers to TypeScript have is whether they should be using Interfaces or Type Aliases for different parts of their code — after all, the [official documentation](https://www.typescriptlang.org/docs/handbook/advanced-types.html#interfaces-vs-type-aliases) is a bit unclear regarding that topic.

Truth is, although these entities are conceptually different, in practice, they are quite similar:

1. They can both be extended.

2. They can both be used to define the shape of objects.

3. They both can be implemented in the same way.

The only extra feature Interfaces bring to the table (that Type aliases don’t), is “*declaration merging”* which means you can define the same interface several times and with each definition, the properties get merged:

Part of the benefits of using Interfaces is that you’re able to enforce the properties of your props for your components. However, thanks to the optional syntax available through TypeScript, you can also define optional props, like this:

Hooks are the new mechanics React provides to interact with several of its features (such as the state) without the need to define a class.

## Adding type check to hooks

Hooks such as `useState` receive a parameter and correctly return the state (again, that’s for this case) and a function to set it.

Thanks to TypeScript’s type validation, you can enforce the type (or interface) of the initial value of the state, like this:

## Nullable values to hooks

However, if the initial value for your hook can potentially be a `null`, then the above example will fail. For these cases, TypeScript allows you to set an optional type as well, making sure you’re covered from all sides.

That way you’re ensuring you keep type checks, but allow for those scenarios where the initial value can come as `null`.

Much like the way you define generic functions and interfaces in TypeScript, you can define generic components, allowing you to re-use them for different data types. You can do this for props and states as well.

You can then use the component either by taking advantage of type inference or directly specifying the data types, likes so:

For the latter, note that if your list contains strings instead of numbers, TypeScript will throw an error during the transpilation process.

Sometimes, your components function and behave like native HTML elements (on steroids). For example, a “borederd box” (which is simply a component that always renders a `div` with a default border) or a “big submit” (which again, is nothing but your good old submit button with a default size and maybe some custom behavior).

For these scenarios, it’s best to define your component type as a native HTML element or an extension of it.

As you can see, I’ve extended HTML’s default props and added a new one: “title” for my specific needs.

As you probably know, React provides its own set of events, which is why you can’t directly use the good old HTML Events. That being said, you do have access to all the useful UI events you need, so much so in fact, that they have the same names as well, so make sure you reference them directly like `React.MouseEvent` or just remember to import them from React like so:

```
import React, { Component, MouseEvent } from 'react';
```

The benefits of using TypeScript here, is that we can also use Generics (like in the previous example) to restrict the elements a particular event handler can be used on.

For example, the following code will not work:

And you’ll see an error message similar to the following:

You can, however, use unions to allow a single handler to be re-used by multiple components:

Finally, for the last tip, I wanted to mention React’s **index.d.ts** and the **global.d.ts** files. They’re both installed when you add React to your project (if you used npm, you’ll find them inside the **npm_modules/@types/react** folder.

These files contain type and interface definitions used by React, so if you need to understand the props of one particular type (or simply which types React makes available), you can open these files and review their content.

For example:

There you can see a small section of the index.d.ts file, showing the different signatures for the `createElement` function.

There is a lot more you can achieve by using TypeScript as part of your React toolchain, so if you saw at least one snippet that you liked here, consider reading up on how to [gradually migrate your React projects to TypeScript](https://blog.bitsrc.io/react-js-to-typescript-how-to-migrate-gradually-d82026126d29?source=activity---post_recommended) or even learn [how to design your own React TypeScript libraries here.](https://blog.bitsrc.io/how-to-build-a-modular-react-typescript-library-3dca7eee1ad)

Either way, I hope you got something out of this article, and feel free to leave any other tips or tricks you’ve picked up over the years of using TypeScript for your React projects!

*See you on the next one!*