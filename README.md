cosco.vim
=========

**Co**mma and **s**emi-**co**lon insertion bliss for vim.

*Cosco's official vim.org page: http://www.vim.org/scripts/script.php?script_id=4758*

## What Cosco does:

Appends, substitutes or removes a comma or a semi-colon to the end of your line, based on its context.

It:

* Takes into consideration previous and next lines endings, as well line indentations.
* Ignores blank lines.
* Will maintain your cursor's original position.

The best way to describe it is with examples.

## Demo / Examples

Examples (as well this plugin) were created with javascript in mind (but the plugin works for any kind of file).

[![Click to watch the video](http://img.youtube.com/vi/xCSjdqf8sOY/0.jpg)](http://www.youtube.com/watch?v=xCSjdqf8sOY)

*(Click the image to watch the video)*

## Dependencies

This plugin depends on [tpope/vim-repeat](https://github.com/tpope/vim-repeat) being installed in order to have the repeat functionality.

## Installation

1. Add `lfilho/cosco.vim` to your [Plug](https://github.com/junegunn/vim-plug), [Vundle](https://github.com/gmarik/vundle), [NeoBundle](https://github.com/Shougo/neobundle.vim), [pathogen](https://github.com/tpope/vim-pathogen), or [manually copy the files](http://superuser.com/a/404820)... You know the deal.
2. Run your Plugn/Vundle/NeoBundle/pathogen process of updating / installing new bundles... (Links above should help you)
3. [Use it](#usage)
4. Profit!

## Usage

Cosco command won't override any mappings or commands you might already have. You have to add them yourself. (Good vim plugin writing practice!).
Here you can find two examples on how to do this. Put them on your `.vimrc`.

### Using it via command

Go to the target line then: `:CommaOrSemiColon`

### Using it via mappings

An example mapping, using the key combo `<Leader>;` for both `normal` and `insert` modes:

```VimL
autocmd FileType javascript,css,YOUR_LANG nnoremap <silent> <Leader>; <Plug>(cosco-commaOrSemiColon)
autocmd FileType javascript,css,YOUR_LANG inoremap <silent> <Leader>; <c-o><Plug>(cosco-commaOrSemiColon)
```

and then you can just type `<Leader>;`.

### Repeating it

You can repeat it with `.` key as long as you have [tpope/vim-repeat](https://github.com/tpope/vim-repeat) installed.

## Auto CommaOrSemicolon Insertion Mode (Experimental)

Auto insertion of a comma or a semicolon is also supported through the function:

```vim
:call AutoCommaOrSemiColon()
```
To activate the AutoCommaOrSemiColon by default add the following line to your `.vimrc`:

```vim
let g:auto_comma_or_semicolon = 1     " Default : 0
```

For faster toggle you can use the command:

```vim
:AutoCommaOrSemiColonToggle
```
or better map it to the desireable key-bindings,`F9` for example:

```vim
nmap <F9> :AutoCommaOrSemiColonToggle<CR>
```
This will show a message about the current state of the auto insetion mode (ON / OFF).
By default what triggers the auto insertion is leaving insert mode (`InsertLeave` event). This can be modified by changing the desired events in the events list:

```vim
let g:auto_comma_or_semicolon_events = ["InsertLeave"]
```
__**Warning**__:

> *This feature is currently experimental and still not mature enough to work for many vim events (e.g:* "TextChangedI"*) or in many places in your code, so use with care.*

## Tests

Tests are done with [vim-unittest](https://github.com/h1mesuke/vim-unittest).

## Known caveats

```javascript
){
    'use strict';

    var foo = 2,
        bar = null;
```

Will change the `use strict` line ending to a comma (it thinks we are inside a hash declaration). Can't really address this issue without a `var` (specific to javascript) check. Might be resolved if we develop a language extension to this plugin.

## TODO and wish list

* Write plugin's vim documentation
* Write all the examples possible
* Improve test coverage
* Write mappings examples using autocommand grouping
* Write a better javascript integration, possible reading from an option .eslint and/or .jshint file (settings for comma dangling, etc)
