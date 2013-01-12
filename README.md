# PDV (phpDocumentor for Vim)

This is a fork of a mirror of PDV (http://www.vim.org/scripts/script.php?script_id=1355). PDV works fairly well,
however I wanted to customize it some to our workflow and standards at iMarc. For example, we don't use packages,
only write PHP 5 code, etc.

## Usage

The usage is the same. You can install via Vundle (BundleInstall 'khamer/PDV--phpDocumentor-for-Vim') or just by downloading and such. To use, you can `:call` `PhpDocSingle()` or `PhpDocRange()`. The examples from the original documentation are:

```vim
inoremap <C-P> <ESC>:call PhpDocSingle()<CR>
nnoremap <C-P> :call PhpDocSingle()<CR>
vnoremap <C-P> :call PhpDocRange()<CR>
```
In my own vim configuration, I'm currently using 

```vim
"" PDV - php Documentor
nnoremap <C-s> :call PhpDocSingle()<CR>
vnoremap <C-s> :call PhpDocRange()<CR>
```

Enjoy.

## Personal modifications

### Git integration 

```php
/**
 * Controller_Foo class
 *
 * @extends Controller_Bar
 *
 * @author    My Name <myemail+my_project@plopmail.com>
 * @copyright 2013
 *
 * @package   App
 *
 * @version   GIT: $Id: 15a8918d246530ec0dbd8ac0760018a314d3d9ef $
 * @update    GIT: $Date: Sat Jan 5 12:05:36 2013 +0100$
 */
class Controller_Foo extends Controller_Bar
{
    ... 
}
```

### Customize for your needs

In your `.vimrc` file :

#### Git keywords

```vim
let g:pdv_cfg_Version  = "GIT: $Id$"
let g:pdv_cfg_Update   = "GIT: $Date$"
```
in addition to rb script like :

```ruby
#! /usr/bin/env ruby

# Git keyword expander for source files:
# 
# Usage : expand_git "<name>" "<format>"
# 
# Example : expand_git "Date" "%ad" in git repo
# see http://git-scm.com/docs/git-log#_pretty_formats for allowed format
# 
# Add to your .git/config repo :
# [filter "dater"]
# 	smudge = expand_git "Date" "%ad"
# 	clean = perl -pe \"s/\\\\\\$Date[^\\\\\\$]*\\\\\\$/\\\\\\$Date\\\\\\$/\"
# 
# And to your .gitattributes
# *.php ident
# *.php filter=dater

info = `git log --pretty=format:"#{ARGV[1]}" -1`
if ARGV[0] == 'raw'
    puts info.to_s
else
	data = STDIN.read
    puts data.gsub('$' + ARGV[0] + '$', '$'+ARGV[0] + ': ' + info.to_s + '$')
end
```

in your $PATH.

> This script can be called in your snippets too :
> 
> ```vim
> snippet     update
> abbr        @update GIT <date>
> alias       upd, @up
> options     head
>     @update GIT: `system('expand_git "raw" "%ad"')`
> ```

### Default values

```vim
let g:pdv_cfg_Author = "My Name Here <myemail@plopmail.com>"
```

> Using 
> 
> ```vim
> let g:pdv_cfg_ProjectName = "amazingstuff"
> ```
> your mail adress will automagically use the `myemail+amazingstuff@plopmail.com` mail alias.

In addition, 

```vim
let g:pdv_cfg_Author_link = "http://mywebsite.fr mywebsite.fr"
```

add the `{@link}` tag :

```php
 ...
 * @author    My Name Here <myemail+amazingstuff@plopmail.com> {@link http://mywebsite.fr mywebsite.fr}
 ...
```

Various default commons infos :

```vim
let g:pdv_cfg_Copyright   = "©Oime 2012-" + strftime("%Y")
let g:pdv_cfg_ReturnVal   = "mixed"
let g:pdv_cfg_Package     = "App"
let g:pdv_cfg_Type        = "mixed"
```

#### Default usage (1|0)

Overwrite them in your `.vimrc` config file:

```vim
" Globals
let g:pdv_cfg_use_AuthorLink  = 0
let g:pdv_cfg_use_Package     = 1
let g:pdv_cfg_use_ProjectName = 1

" Git integration
let g:pdv_cfg_use_Changes     = 0
let g:pdv_cfg_use_Commit      = 0
let g:pdv_cfg_use_Update      = 1
let g:pdv_cfg_use_Version     = 1
let g:pdv_cfg_use_Revision    = 0
```
