---
title: "Create your custom interactive shell with python 🐍"
slug: "create-your-custom-interactive-shell-with-python"
date: 2022-01-19T12:52:43+01:00
draft: false
categories: ["Python"]
tags: ["python", "advanced-features"]
socialShareLink: true
image: "cover.png"
shareButtons: true
---

It can happen that, sometimes, you need a CLI for you application, and maybe could be
nice to have a custom interactive shell with command completion and history. Python has the
``Cmd`` class within the [cmd](https://docs.python.org/3/library/cmd.html) module that
provides a simple framework for writing line-oriented command interpreters.

## The skeleton of the shell

```python
from cmd import Cmd

class MyPrompt(Cmd):
    pass

MyPrompt().cmdloop()
```

The ``Cmd.cmdloop()`` repeatedly issue a prompt, accept input, parse an initial
prefix off the received input, and dispatch to action methods, passing them
the remainder of the line as argument.

Basically when we run the script above it will display a default prompt:

```bash
(Cmd)
The ``Cmd`` includes the ``help`` or ``?`` command to get your interactive shell help:
```

```bash

(Cmd) help

Documented commands (type help <topic>):
========================================
help

(Cmd) ?

Documented commands (type help <topic>):
========================================
help

(Cmd)

If you would like to exit the application you need to press ``Ctlr-C`` and get a ``KeyboardInterrupt``.
```

## Prompt and Intro

The default prompt text is ``(Cmd)`` but it can be overridden using the prompt
attribute of the class.

Furthermore we can set a text to be the banner (or the welcome message for example),
that is the text message shown when we launch our application.

```python
from cmd import Cmd

class MyPrompt(Cmd):
    prompt = "myshell>"
    intro = "Welcome!! Type ? or help for the commands list."
    pass

MyPrompt().cmdloop()
```

## Complete example

Now I'd like to show you a complete example of a custom interactive shell.
Imagine you wanna create a command to compute a sum of bunch of numbers (e.g. `1,4,5,78,23`).

I'm gonna create a `do_sum` method that will compute the sum of the numbers.

```python
from cmd import Cmd


class MyPrompt(Cmd):
    prompt = "myshell> "
    intro = "Welcome to MY shell! Type ? to list commands"

    def onecmd(self, line):
        try:
            return super().onecmd(line)
        except Exception as e:
            print(f"{e}")
            return False  # don't stop

    def do_exit(self, inp):
        print("Bye")
        return True

    def help_exit(self):
        print("exit the application. Shorthand: x q Ctrl-D.")

    def default(self, inp):
        if inp == "q":
            return self.do_exit(inp)

        print("Default: {}".format(inp))

    def help_sum(self):
        print("Run a sum")

    def do_sum(self, input):
        lst_input = [int(n) for n in input.split(",")]
        print(f"The sum is: {sum(lst_input)}")

    do_EOF = do_exit
    help_EOF = help_exit


if __name__ == "__main__":
    MyPrompt().cmdloop()
```

and see it in action:

```bash
~ python -m shell
Welcome to MY shell! Type ? to list commands
myshell> sum 1,2,3,4,5
The sum is: 15
myshell> sum "a,dsfg"
invalid literal for int() with base 10: '"a'
```

As you can see the first command return a valid and meaningful output. The second one fails due to the wrong output and it returns the error trace of the python interpreter. That's nice huh? 😎

Taking a look at the code snippet above you can notice the `onecmd` method within the `MyPromopt` class. 

```python
    def onecmd(self, line):
        try:
            return super().onecmd(line)
        except Exception as e:
            print(f"{e}")
            return False  # don't stop
```

That method, that extends the one of the super class, is called when the user enters a command, and in case of an exception print the exception. This is a very useful feature to have when you are developing a command line application because in case of an error whatsoever, it won't crash the application, and you can decide you custom fallback action.

The other method `default` is called every time a command is entered and it does not correspond to any of the `do_*` methods.

What about the `do_EOF` and `help_EOF`? You might have noticed that `Ctrl-d`, prints ``*** Unknown syntax: EOF``.
That's because Ctrl-d send an EOF (End Of File) signal and by default Cmd does not know what to do with it.

The solution is to implement the do_EOF method that will be called when the user presses `Ctl-d`. As we already have a do_exit method, we can just assign that to the do_EOF and have both do the same. In order to provide help for the EOF, we can include a function called help_EOF that is assigned the help_exit function.

IMHO this is a great built-in feature, very useful when you wanna create a command line application as a public interface of you library.

On top of the `cmd` module a lot of 3rd party apps have been created. I'd like to mention [cmd2](https://github.com/python-cmd2/cmd2) that can be defined a custom `cmd` module with steroids 😀.

I hope you enjoied this article! See you at next episode 👋.
