---
layout: default
title: "Change TOR exit node"
lang: en
date: 2024-10-21
categories: TOR python urwid invoke
---
## What's the problem ? ##

Sometimes the web resource you want to access is restricted to a particular geographic area, especially due to rights issues, such as those encountered with sporting events.

To solve this problem you can either move to the country in question, which can be expensive, or use the [TOR browser](https://www.torproject.org).

By default, the TOR browser selects an exit node (the computer that accesses the resource) in a randomly selected country. This exit node can be set by editing the browser's configuration file named *torrc*.

If you want to access different geographics areas, it becomes tedious to edit this file manually. The `change_exit_node` script allows you to make this change from the command line or through a graphical interface.

The source code is available [here](https://github.com/gillesxr/change_exit_node).

## The not so direct solution ##

It would be simpler to just type in terminal the following:

`sed -i 's/ExitNodes {[a-zA-Z]\+}/ExitNodes {us}/1' torrc`

But with this so called problem, I have yet another excuse to use Python ! And I've been wanting to use the following Python modules for a while:

- [Invoke](https://www.pyinvoke.org/) provides a clean and high level API for running shell command.
- [Urwid](https://urwid.org/), is a console user interface library for Python.

### The CLI interface ###

With **Invoke**, you create command with the `@task` decorator:

```
@task(help={'torrc': 'Tor configuration file.', 'country': 'The exit node country name.'})
def exitto(ctx, torrc: typing.TextIO, country: str) -> None:
    country_code = get_node_from_country(country)
    if change_node(torrc, country_code) == True:
        print(f'New Tor exit node: {country!r}.')
```

And you can invoke this new command in terminal with:

`invoke exitto $TOR_PATH/torrc 'Italy'`

### The GUI interface ###

**Urwid** has everythig you need for a modern graphics library as:

- It handles many of difficult and tedious tasks.
- It has loosely coupled component, designed to be extended by the user.
- It has different event loops to integrate with [Asyncio](https://docs.python.org/3/library/asyncio.html), [Twisted](https://twisted.org/), [Glib](https://docs.gtk.org/glib/), [Tornado](https://www.tornadoweb.org/en/stable/) and [ZMQ](https://pyzmq.readthedocs.io/en/latest/) libraries.

As an example, here is a definition of a button bar dynamically build with the list of labels passed in argument:

```
class ButtonBar:

    def __init__(self, parent: W, labels: list[str]) -> None:
        """Create a button bar from the labels list in parameter."""
        self._parent = parent
        self.buttons = self._create_bar(labels)

    def _create_bar(self, labels: list[str]) -> list[B]:
        button_bar = []
        for index, label in enumerate(labels):
            btn = urwid.Button(f'{label}', on_press=self._button_press, align='center')
            btn.code = index
            button_bar.append(btn)
        return urwid.GridFlow(button_bar, 25, 3, 1, urwid.CENTER)

    def _button_press(self, button: B) -> None:
        self._parent.button_press(button.code)
```

The buttons are named from the labels list and a code, an integer,  is associated with each button. This code allows to map a callback function with each button to determine its action.

## Closing words ##

With this little post, I hope I have piqued your curiosity for these Python modules. Feel free to check out the [source code](https://github.com/gillesxr/change_exit_node) to tickle with it.
In a future post, I get into another Python graphics library named [Kivy](https://kivy.org/) and we will see how to design a custom widget.
