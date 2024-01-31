This will likely remain as a "snippet" document for useful nvim-related commands I've found.


# Concealment Mode
Concealment allows bullet points and other markdown-related elements to be automatically converted to their equivalent unicode character. More importantly, it can be used in latex:


![[Pasted image 20240114131200.png]]

Relevant config:
```lua
vim.g.tex_conceal = 'abdmgs'
```

# Copy to windows clipboard

```
"*yy
```


Delete until next bracket:
```
d t}
```


$$




$$