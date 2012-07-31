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