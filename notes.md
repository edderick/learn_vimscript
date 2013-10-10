Learn VimScript The Hard Way
============================

http://learnvimscriptthehardway.stevelosh.com/

A few quick notes about things that I read in the book.

Echoing
-------

+ :ec[ho], prints a message (to the status line?) 
+ :echom[sg], prints a message to the status line, and the message-history
+ :messages, shows messages from :echom

These commands are good for debugging

Comments 
--------

One can add comments using a double quote :)

Options
-------

There are boolean options, e.g.

+ :set number and conversely :set nonumber
+ This behavior is apparently common to all boolean options 
+ :set nu[mber]! will toggle the value
+ :set nu[mber]? will report the value => "number" or "nonumber"

And those that take values, e.g.

+ set numberwidth=10 
+ set numberwidth? will report the value

And as an added bonus, you can even specify multiple values at once!

A little aside, :set relativenumber is fairly cool. 

Mapping
-------

Mapping lets you tell Vim: When I press this key, don'' do that; do this.

###Normal Mode Mapping

+ :map - x makes - do what x did
+ It would seem that these mapping will cascade... :D

To handle special characters, one can use <keyname>, e.g.

+ :map <space> viw, space selects a word
+ :map <c-d> dd, ctrl+d deletes a line

When writing these kinds of statements, a comment helps clarify intent.

###Modal Mapping

To use a mapping in each different mode, one can use: 

+ :nmap - for normal mode
+ :vmap - for visual mode 
+ :imap - for insert mode

Note: With imap, it will literally paste in the key combo! 
+ :imap <c-d> dd, will just paste in dd!
+ :imap <c-d> <esc>ddi does what you probably expected

Bonus: :imap <c-u> <esc>vUi, sets <c-u> to set to uppercase.
(Also U in visual mode set the word to uppercase.

###Unmapping

One can unmap, using unmap, and variants of it:

+ nunmap
+ iunmap
+ vunmap

###Recursion

If you do something like:

:nmap dd O<esc>jddk

then it will enter into a recursive cycle for ever. (Which you can end with 
<c-c>)

*And that is why they invented :noremap!*

:noremap, stands for non-recursive map. It just maps to whatever it would map to if there were no mappings before. It also has the typical friends that one might come to expect. :nnoremap, :vnoremap and :inoremap.

*ALWAYS USE NOREMAP*
It just isn''t worth the hassle!

Leaders
-------

Doing these crazy mappings leads to clobbering. Which is why we use the concept
of leaders, a rarely used character that we place at the beginning or our
mapping.

Good news: vim supports leaders! 

+ let mapleader = ","
+ :nnoremap <leader>d dd

Three good reasons to use the leader key:

+ May want to be able to use the leader key later on
+ If someone wants to copy your .vimrc, they can use their own leader
+ Lots of plugins use leaders, +1 for familiarity

###Local Leader

Local leaders take on meaning only for a certain type of file. 

+ :let maplocalleader = "\\"

Note: The value of leader must be declared before the mapping is created!

Editing Yo .vimrc
-----------------

Don''t want to lose context just to edit the .vimrc

+ :nnoremap <leader>ev :vsplit $MYVIMRC<cr>
+ :nnoremap <leader>sv :source $MYVIMRC<cr>

Now you can edit, and source the .vimrc super fast :)

Abbreviations
-------------

These are like mappings, but meant for insert mode. 

+ iabbr[ev] and and

There exists: :set iskeyword?

Abbreviations can of course be used for more things than just spelling
corrections: One example might be sysout to System.out.println();

###Difference Between Mapping and Abbr

Mappings are not context sensitive, abbreviations are, e.g.

+ :abbr bar baz => foobar stays as foobar
+ :inoremap bar baz => foobar becomes foobaz

More Mappings
-------------


