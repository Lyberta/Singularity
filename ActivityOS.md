# ActivityOS

## Idea

Design an operating system from scratch that maximizes productivity from every user's thought and action. Basically, the operating system acts as "inverse biocomputer" where real biocomputer - human brain - slides perfectly inside and they cooperate in harmony. Perfectly balanced, as all things should be.

So it has to be designed very differently from all the operating systems of old. First step is recognizing how horrifically tragic and anti-human the desktop metaphor is. It is based on the idea of traditional office where humans are put as enslaved cogs in the machine. Desktop metaphor is designed to enslave and ruin productivity of the user. It must go.

So the second step when designing a true humane operating system is recognizing that knowledge is a graph. The same piece of information - the same file - can be arrived at via different ontological categories. For example, a user may be interested in going through all of the photos taken at their birthday party or all the photos containing a certain person in it. So what happens if said person happens to be at that birthday party? Yes, the photos of that person would belong in both "My Nth birthday" and "John Doe" categories.

One can imagine many other different overlaps. Like "Rock music", "Music for fitness", "Music in a specific key"... Legal documents can be categorized by a certain person, year, legal entity...

So file system has to form a knowledge graph. And at the time of writing the best format to represent such graph is [Web Ontology Language](https://en.wikipedia.org/wiki/Web_Ontology_Language).

Third step is recognizing how users actually use computers. Sure, in plenty of cases it can be a simple app but in general case the user would like to open several apps that would either cooperate automatically via some form of inter-process communication or the user would manually adjust each app to achieve their goal. Such collection of apps (among other things) is called "activity" - hence ActivityOS.

And let's forget about traditional desktops, laptops, smartphones... what about daily tasks? We are building an operating system for maximum productivity, right? Well, imagine the user going inside their kitchen at a specific time - the operating system would figure out based on the real life coordinates and time of day that it needs to switch to an activity called "cooking" with a template "dinner". It would launch an app for managing recipes showing the list of tasty meals for dinner, an app for managing the products in the fridge showing how much of each ingredient is in the user's fridge and maybe show warnings if some of them are low or missing and a button to order a replacement from a nearby grocery store, a music player app with a cooking playlist to set the right mood, maybe query the smart home system to adjust the lighting a bit, highlighting the cooking table to help the user cook... Of course, each app can be carefully pinned in the AR interface, such as recipe browser near the cooking table, fridge management app near the fridge, etc.

As you can see, activities can be pretty complicated, context-sensitive based of user's location, time of day, weekday, other people nearby, they may involve launching many apps at once with different files loaded, they may involve switching certain low-level services such as gaming activity removing limiters allowing overclocking the CPU and GPU for maximum performance, sleeping activity downclocking the system and slowing down the fans...

Finally, the input device. Well, graph-based file system and activities can be put into old form factors. One can easily imagine ActivityOS running on a desktop PC, laptop, tablet, smartphone, smartwatch... However, they are all bound by legacy input devices. We have our bodies and our voice. Maximum productivity will be achieved by running ActivityOS on a device similar to [Apple Vision Pro](https://en.wikipedia.org/wiki/Apple_Vision_Pro) and [Neuralink](https://en.wikipedia.org/wiki/Neuralink).

## Activity

Activity is a certain set of actions the user wants to perform. "Listening to music", "watching a movie", "playing a video game", "creative writing", "composing music", "video creation", "programming" are all usual activities.

Each activity has one or several virtual desktops and a set of programs that need to be launched, sometimes in a specific order. Also, each activity has a set of files the user would want to access, called a "library".

## Library

Library is a set of files and their corresponding metadata. The most important metadata is, of course, tags. Tags are user-defined and exist so the user can easily filter files by tag. Also, tags define what kind of actions can be performed.

## Tag

Tag is a certain ontological category the files belong to. It can be something like "Pop music" or "Girlfriend". Tags themselves can also belong into tags. "Pop music" would belong into "Music" and "Girlfriend" would belong to "People".

Some tags can be smart and imply certain properties. "Image" implies "Resolution", "Bit depth", "Color space" and others. "Person" imples "First name", "Last name", "Location", "Time zone" and others.

## Action

An action is a set of commands that must be executed with the given file. Actions are defined by the current activity, file tags and file extension. There is a default action too. Clicking on a video file in the "watching a movie" activity should open it in a video player, however, doing the same in the "video editing" activity should add it to project instead.

## Keep things fluid, avoid rigid heirarchies

At the top level there should be a set of activities, libraries, tags and actions. Each activity can have more than 1 library. Each library can belong into more than 1 activity. Etc. It's all graphs, not trees.

## Implementation details

There are 2 modes of implementing this system: transitional mode and pure mode. Transitional mode is designed to run on top on an existing OS. Pure mode gives full control to the ActivityOS. Linux kernel can still be used just like on Android, at least initially.

Actually, [GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell) seems to be the best base to start coordinated ActivityOS efforts as it already has the Activities button.

GNOME Files (also known as Nautilus) needs to have an ability to add Linux VFS directories as Libraries which would be then be stored in a virtual tag-based file system on a higher level of abstraction. Then libraries can be properly tagged by the user or GNOME itself in case of mechanical tags which can be inferred from the file itself (think [MediaInfo](https://en.wikipedia.org/wiki/MediaInfo)).

Once tagged libraries are implemented, it's all about adding a proper UI to create and manage activities.
