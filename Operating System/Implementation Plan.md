# Implementation plan for ActivityOS

## Native version - start by forking [GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell)

It already has the Activities button so it makes a perfect candidate for a fork.

GNOME Files (also known as Nautilus) needs to have an ability to add Linux VFS directories as Libraries which would be then be stored in a virtual tag-based file system on a higher level of abstraction. Then libraries can be properly tagged by the user or GNOME itself in case of mechanical tags which can be inferred from the file itself (think [MediaInfo](https://en.wikipedia.org/wiki/MediaInfo)).

Once tagged libraries are implemented, it's all about adding a proper UI to create and manage activities.

## Web version - implement using [WebAssembly System Interface](https://wasi.dev/)

People already have web browsers installed on their computing devices. We can ease the migration to ActivityOS by offering it as an app on the Web.

### Lazy tags

Some automatic tags are too expensive to compute every time the file is changed. Hence, it makes sense to store a flag on file modification that tag value has to be freshly computed next time it is queried. Then there can be a command similar to [`sync`](https://linux.die.net/man/8/sync) to force recomputation of all lazy tags.
