---
title: "How to Become a Better Programmer"
date: 2025-06-23
---
*23 June 2025*

We are constantly bombarded by information on social media, with fast tips or silver bullets claiming to teach us how to become extraordinary programmers. Recently, I've seen many posts talking about how to be a 10x developer with this type of generic advice. But in my opinion, this advice only overwhelms people who are just starting out in the programming market, because it seems easy to follow these tips, learn a hyped programming language, and start delivering software. Luckily, there are many articles and community content demystifying this subject.

In this text, I would like to share with you my thoughts and experiences on how to become a better programmer.

## Write Less Code

Yeah, exactly what you read: write less code. The logic is simple — the less code you write, the lower the chance of bugs. An unnecessary amount of code in your project will bring many problems when debugging, fixing, and implementing new features. Today, we have many tools for versioning and tracking changes in our repositories, so every piece of unnecessary code should be removed from the codebase. If one day we need that code, we can use the repository history to find it — don't worry. It's important to write new code as short as possible, and this doesn't just mean using fewer lines; we need to write simple, easy-to-read, and well-organized code.

In my opinion, there is nothing more satisfying in software development than deleting legacy code and refactoring poorly written code. Whenever possible, try to do this while working on code-related tasks. You don't need to actively search for things to delete in the legacy code — just create the habit of removing unnecessary parts and making small improvements as part of your routine work. In the category of unnecessary things, you might consider:

* Unnecessary logic operator;

```python
# bad
if expression:
	return True
else:
	return False

#good
return expression
```

* Duplicated code;

```python
#bad. This can be found a lot within loops context.
if foo:
	do_something()
if foo:
	do_something_else()
if foo:
	do_more()

#good
if foo:
	do_something()
	do_something_else()
	do_more()
```

* Dead code;

```python
#dead code
def a():
	print('I will never be called :(')

print('Hello!')
```

* Verbose code;

```python
#bad
def is_valid(char):
	if char != None:
		return char == 'VALID';
	else:
		return False

#good
def is_valid2(char):
	return char != None and char == 'VALID'
```

* Unnecessary comments;

```python
#loop from zero to ten and print them
for i in range(0, 10):
    print(i)
```
* Blank chars and non standardized code.

![Less Is More](/images/less-is-more.jpg)

> Remember, less is more!

## Read and Understand Code

Whenever I start working on a new project, I follow the default behavior of reading the documentation to understand which code patterns, libraries, and frameworks are used within the project. If you're working with legacy code or on a new project, the documentation might not help you much at first. In that case, you'll need to start reading the code to understand how to implement what you need.

I like to use a reverse method when reading code. In this approach, you need to have a specific goal in mind. It might be a function you need to change, an error message shown in the logs, or something you're searching for. With a goal in hand, you can search for relevant terms in the codebase. Once you find references, you can open the files and begin reading the code by following the call stack.

For me, this is a good way to read and understand code, because we start with a small, focused piece of "raw code." As we move up the call stack, we begin to understand the abstractions that are used.

## Bug Busters!

Be excited to solve bugs — even the ones you didn't create. I know that working on bugs is sometimes considered "dirty work," but bugs have a lot to teach us. The harder they are to solve, the more we learn. The perception of difficulty can vary from person to person, but don't worry — focus on building the habit of finding bugs, enjoy solving them, and embrace the challenge!

Become a bug buster!

## Know How to Debug

Putting a `System.out.println` or `console.log` in your code is a simple and easy way to debug a function. But make no mistake — you may fall into a "brute-force" debugging mode. We should avoid that, because in this scenario, we often waste time looking for things that are not related to the issue.

Learn how to use the best tools to debug the problem you're facing. These days, we have many debugging tools that integrate easily with our development environments. Take advantage of AI as well — these tools can speed up your searches and suggest potential paths to solve the issue.

## Don't Be a Perfectionist

When we think about ourselves, perfectionism often holds us back, because we feel that our work is never finished — which generates anxiety. We must learn how to deal with this situation and keep in mind that our work will never be truly "finished." So, what are my thoughts about it?

- Create a simple and clear work plan for each activity
- Define what "done" means for each task
- Create automated tests that validate your definition of done before you start coding
- Code until all your test cases pass
- And last but not least: don't work more than necessary!

When we think about other people's work, perfectionism can turn us into harsh judges. Be open-minded — in programming, there are many ways to solve the same problem. When evaluating someone else's code, we must set aside our personal preferences and focus only on what may impact system behavior, performance, or consistency.

## Coding is About People

It might seem a little strange, but code is about people. We write code for others. Programming is both technically and socially challenging. Therefore, we need to constantly improve our communication skills. A good programmer communicates well — clearly, frequently, respectfully, at the right level, and using the appropriate method.

## Suggested Reading

Goodliffe, Pete. *Becoming a Better Programmer*. O'Reilly Media, 2014.


***That's all folks!*** 👋