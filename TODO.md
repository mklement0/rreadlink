
* Fix the following scenario to truly report all intermediary targets

/Users/mklement/bin/fls@ -> /Users/mklement/lib/node_modules/fls/bin/fls
/Users/mklement/lib/node_modules/fls@ -> /Users/mklement/Documents/Projects/OSS/fls

That is, the symlink points to file inside a symlinked *directory*.
Currently, we only report the start- and endpoints of such a chain.

We could to the following:


    # ?? Is placing a '@' inside a path the right approach?
    /Users/mklement/bin/fls@ -> /Users/mklement/lib/node_modules/fls@/bin/fls -> /Users/mklement/Documents/Projects/OSS/fls/bin/fls

    /Users/mklement/bin/fls
    /Users/mklement/lib/node_modules/fls/bin/fls
    /Users/mklement/Documents/Projects/OSS/fls/bin/fls