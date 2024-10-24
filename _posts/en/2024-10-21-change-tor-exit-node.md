---
layout: default
title: "Change TOR exit node"
lang: en
date: 2024-10-21
---
## What's the problem ? ##

Sometimes the web resource you want to access is restricted to a particular geographic area, especially due to rights issues, such as those encountered with sporting events.

To solve this problem you can either move to the country in question, which can be expensive, or use the [TOR browser](https://www.torproject.org).

By default, the TOR browser selects an exit node (the computer that accesses the resource) in a randomly selected country. This exit node can be set by editing the browser's configuration file named *torrc*.

If you want to access different geographics areas, it becomes tedious to edit this file manually. The `change_exit_node` script allows you to make this change from the command line or through a graphical interface.
