When you make something with code, you're probably used to figuring out a design as you go. You write a function, you choose some arguments, and if you don't like what you see, perhaps you add a new argument to that function and test again. This [cowboy coding|https://en.wikipedia.org/wiki/Cowboy_coding] as some people like to call it can be great fun! It allows systems to emerge more organically, as you iteratively see your front-end design emerge, the design of your implementation emerges too, co-evolving with how you're feeling about the final product.
		
As you've probably noticed by now, this type of process doesn't really scale, even when you're working with just a few other people. That argument you added? You just broke a bunch of functions one of your teammates was planning and when she commits her code, now she gets merge conflicts, which cost her an hour to fix because she has to catch up to whatever design change you made. This lack of planning quickly turns into an uncoordinated mess of individual decision making. Suddenly you're spending all of your time cleaning up coordination messes instead of writing code.
		
The techniques we've discussed so far for avoiding this boil down to _specifying_ what code should do, so everyone can write code according to a plan. We've talked about [requirements specifications|requirements], which are declarations of what software must do from a users' perspective. We've also talked about [architectural specifications|architecture], which are high-level declarations of how code will be organized, encapsulated, and coordinated. At the lowest level are *functional specifications*, which are declarations about the _properties of input and output of functions in a program_.

In their simplest form, a functional specification can be a just some natural language that says what an individual function is supposed to do:
		
`javascript
// Return the smaller of the two numbers, 
// or if they're equal, the second number.
function min(a, b) {
  return a < b ? a : b;
}
`

This comment achieves the core purpose of a specification: to help other developers understand what the requirements and intended behavior of a function are. As long as everyone sticks to this "plan" (everyone calls the function with only numbers and the function always returns the smaller of them), then there shouldn't be any problems.
		
The comment above is okay, but it's not very precise. It says what is returned and what properties it has, but it only implies that numbers are allowed without saying anything about what kind of numbers. Are decimals allowed or just integers? What about not-a-number (the result of dividing 1 by 0). Or infinity?
		
To make these clearer, many languages use *static typing* to allow developers to specify types explicitly:

`javascript
// Return the smaller of the two integers, or if they're equal, the second number.
function min(int a, int b) {
  return a < b ? a : b;
}
`

Because an `int` is well-defined in most languages, the two inputs to the function are well-defined.

Of course, if the above was JavaScript code (which doesn't support static typing), JavaScript does nothing to actually verify that the data given to `min()` are actually integers. It's entirely fine with someone sending a string and an object. This probably won't do what you intended, leading to defects.
		
This brings us to a second purpose of writing functional specifications: to help _verify_ that functions, their input, and their output are correct. Tests of functions and other low-level procedures are called *unit tests*. There are many ways to use specifications to verify correctness. By far, one of the simplest and most widely used kinds of unit tests are *assertions*<clarke06>. Assertions consist of two things: 1) a check on some property of a function's input or output and 2) some action to notify about violations of these properties. For example, if we wanted to verify that the JavaScript function above had integer values as inputs, we would do this:
		
`javascript
// Return the smaller of the two numbers, or if they're equal, the second number.
function min(a, b) {
  if(!Number.isInteger(a)) 
    alert("First input to min() isn't an integer!");
  if(!Number.isInteger(b)) 
    alert("Second input to min() isn't an integer!");
  return a < b ? a : b;
}		
`
		
These two new lines of code are essentially functional specifications that declare "_If either of those inputs is not an integer, the caller of this function is doing something wrong_". This is useful to declare, but assertions have a bunch of problems: if your program _can_ send a non-integer value to min, but you never test it in a way that does, you'll never see those alerts. This form of *dynamic verification* is therefore very limited, since it provides weaker guarantees about correctness. That said, a study of the use of assertions in a large database of GitHub projects shows that use of assertions _is_ related to fewer defects<casalnuovo15b> (though note that I said "related": we have no evidence that assertions actually prevent defects. It may be possible that developers who use assertions are just better at avoiding defects.)

Assertions are related to the broader category of *error handling* language features. Error handling includes assertions, but also programming language features like exceptions and exception handlers. Error handling is a form of specification in that _checking_ for errors usually entails explicitly specifying the conditions that determine an error. For example, in the code above, the condition `Number.isInteger(a)` specifies that the parameter `a` must be an integer. Other exception handling code such as the Java `throws` statement indicates the cases in which errors can occur and the corresponding `catch` statement indicates what is to done about errors. It is difficult to implement good exception handling that provides granular, clear ways of recovering from errors<chen09>. Evidence shows that modern developers are still exceptionally bad at designing for errors; one study found that errors are not designed for, few errors are tested for, and exception handling is often overly general, providing little ability for users to understand errors or for developers to debug them<ebert15>. These difficulties appear to be because it is difficult to imagine the vast range of errors that can occur<maxion00>.
		
Researchers have invented many forms of specification that require more work and more thought to write, but can be used to make stronger guarantees about correctness<woodcock09>. For example, many languages support the expression of formal *pre-conditions* and *post-conditions* that represent contracts that must be kept for the program to be correct. (*Formal* means mathematical, facilitating mathematical proofs that these conditions are met). Because these contracts are essentially mathematical promises, we can build tools that automatically read a function's code and verify that what it computes exhibits those mathematical properties using automated theorem proving systems. For example, suppose we wrote some formal specifications for our example above to replace our assertions (using a fictional notation for illustration purposes):

`javascript
// pre-conditions: a in Integers, b in Integers
// post-conditions: result <= a and result <= b
function min(a, b) {
  return a < b ? a : b;
}		
`
		
The annotations above require that, no matter what, the inputs have to be integers and the output has to be less than or equal to both values. The automatic theorem prover can then start with the claim that result is always less than or equal to both and begin searching for a counterexample. Can you find a counterexample? Really try. Think about what you're doing while you try: you're probably experimenting with different inputs to identify arguments that violate the contract. That's similar to what automatic theorem provers do, but they use many tricks to explore large possible spaces of inputs all at once, and they do it very quickly.

There are definite tradeoffs with writing detailed, formal specifications. The benefits are clear: many companies have written formal functional specifications in order to make _completely_ unambiguous the required behavior of their code, particularly systems that are capable of killing people or losing money, such as flight automation software, banking systems, and even compilers that create executables from code<woodcock09>. In these settings, it's worth the effort of being 100% certain that the program is correct because if it's not, people can die. Specifications can have other benefits. The very act of writing down what you expect a function to do in the form of test cases can slow developers down, causing to reflect more carefully and systematically about exactly what they expect a function to do<fucci16>. Perhaps if this is true in general, there's value in simply stepping back before you write a function, mapping out pre-conditions and post-conditions in the form of simple natural language comments, and _then_ writing the function to match your intentions.

Writing formal specifications can also have downsides. When the consequences of software failure aren't so high, the difficulty and time required to write and maintain functional specifications may not be worth the effort<petre13>. These barriers deter many developers from writing them<schiller14>. Formal specifications can also warp the types of data that developers work with. For example, it is much easier to write formal specifications about Boolean values and integers than string values. This can lead engineers to be overly reductive in how they model data (e.g., using binary models of gender instead of more inclusive non-binary and multidimensional ones).