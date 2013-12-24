nlua
====

Do you hate yourself and/or freedom? You might be interested in this project then. It's a fork (or maybe a branch) of GNU nano 2.3.2 with hacky Lua scriptability. By 'scriptability', I mean the ability to programmatically filter, modify, and generate raw input before it gets processed by nano -- about as hacky as it gets, but also kind of powerful in a way.

**Build**

    $ # First, make sure liblua 5.2 development files are on your system
    $
    $ sudo apt-get install liblua5.2-dev    # or equivalent
    $
    $ # Now you're ready.
    $
    $ git clone https://github.com/adsr/nlua.git
    $ cd nlua
    $ ./autogen.sh
    $ ./configure --enable-nlua
    $ make
    $ 
    $ # The nlua binary is now at ./src/nano
    $
    $ sudo make install    # Only do this if you want to replace /usr/bin/nano

**Run**

In your nanorc file, e.g., `~/.nanorc`, add a line like the following...

    lua "/home/adam/.nanolua"

...which specifies a Lua script to execute at runtime. Make sure it's an absolute path.

The Lua script is a just a regular Lua script with two special functions, `nlua_filter_input` and `nlua_unget_input`. `nlua_filter_input` is invoked when a user sends input to nano. You can either swallow it, modify it, or let the input pass through unaltered. You can also generate more input with `nlua_unget_input` which stuffs nano's internal key buffer. Take a look at `.nanolua` in this repo for some examples.
