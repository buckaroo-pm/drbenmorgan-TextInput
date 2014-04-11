TextInput
=========

Readline/Editline replacement from CERN's [ROOT software](http://root.cern.ch). This repository is a subtree split from the [github mirror of ROOT](https://github.com/root-mirror/root). Commits are not squashed to
retain info on history. The master branch is for local development, the
upstream branch will retain the pristine sources from the mirror, to
be updated on a semi regular basis!

Purpose
=======

Read and edit text lines, and write what was read.

This library is a simplistic alternative to readline / editline. It offers
less functionality but it has a more liberal license (see [LICENSE.TXT](LICENSE.txt) in
the topmost) directory, it has no external dependencies, and it works on
all platforms that I tested:

- Linux
- Windows (probably >= 2000)
- MacOS
- Solaris

Adding other platforms is trivial.

Internal Design
===============

[TextInput.h](TextInput.h) contains the main interface. The reading can be extended by
adding classes that derive from [`textinput::Reader`](Reader.h); the displaying can be extended
by deriving from [`textinput::Display`](Display.h).

There can be multiple readers and multiple displays. All displays are
equal, all readers are equal. All displays show the input of all
readers. The terminal / console implementations for readers and
displays are provided. Both readers and displays only attach while
textinput is acively reading input. As soon as the input is done (enter
was pressed), they detach from the terminal, allowing the application
to take control of the terminal, and even to crash without leaving the
terminal in a non-default state.

The editor provides basic emacs-like keybinding, as known from e.g.
bash. It supports ^O, ^R (for now without regex), and most word-centric
editing commands. See [`textinput::KeyBinding`](KeyBinding.h) for details.

KeyBinding maps the InputData read from the Reader to `Editor::Commands`.
The Editor performs the requested editing actions, and the Displays
are informed about the changes. TextInput gives access to the read
state ("are we done?") and the input.

Why no [N]Curses?
-----------------

Because of platform independence (well, one could still have a
TerminalDisplayCurses) and because nowadays this is actually rarely
needed. Sure, it's the "right" way of interfacing terminals. But the
number of terminal types in the wild has siginifantly decreased, so
just hard-coding escape sequences became a viable alternative.

References
==========

These pages helped when writing libtextinput:

- http://tldp.org/LDP/lpg/node129.html
- http://rtfm.etla.org/xterm/ctlseq.html
- http://frexx.de/xterm-256-notes

Thanks a lot to the authors for creating these useful pages!

Axel Naumann <axel@cern.ch>, May 2011


