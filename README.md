the trouble with wayland

wayland is often described as "new" and "modern." in reality, however, wayland was initially released in september of 2008. it has taken a great deal of time to reach its current state, with wayland now generally functioning on many systems. wayland... is not new.

one of the primary rules of linux and a tenet of foss is that we do not break user space. this is a very simple rule. it is basic and easy to follow.

and the trouble with wayland is that it breaks this rule.

let's examine the pros and cons. what makes wayland appealing? what makes it unappealing?

wayland combines the display server and compositor into a single function. in x-windowing, these are separate features, along with the window manager as a client-side process. while wayland simplifies this, it also reduces the feature availability of both window management and compositing. so even as the process is streamlined, the results are also more limited.

in wayland, the compositor receives pixel data directly from clients, whereas in x-windowing, the compositor must fetch all pixel data. this introduces latency in x-windowing, but not in wayland. however, this latency is measured in milliseconds, far below the threshold of human sensitivity. you cannot notice, see, or experience this speed difference, which invalidates the argument that wayland is faster.

wayland delegates rendering to be performed client-side. x-windowing can allow rendering from the client or handle it with its compositor. with wayland, some rendering may appear smoother, but x-windowing can perform multiple instances of rendering and offer more features and functionality, while wayland remains limited in its capabilities.

wayland does not support sessions, selections, and drag and drop. these must be managed solely by the desktop environment. x-windowing can handle all the familiar features because the x server communicates directly with the client-side and the kernel. wayland allows the kernel to communicate directly with the client. this has been one of the strongest arguments in favor of wayland. indeed, it was the argument that initially gained support for wayland. it simplifies the process and removes the middleman. however, in practice, it is an oversimplification. wayland is limited by its inability to handle basic display features, and the lack of an intermediary in communication restricts what a desktop environment can offer the end user.

wayland isolates the i/o of window to api communications, allowing communication only between an active application and the display at a time. this has been an argument in favor of wayland, claiming it provides better security than x-windowing. however, this argument is misleading. for one, x-windowing was patched years ago to limit display access from applications, a point that wayland proponents often overlook and instead suggest that the x server does not do so (yet, the x server does). furthermore, an api must communicate with the display to produce a gui application. with wayland, it does not need to go through the built-in securities of x-windowing. since the display must be accessed, whether all at once or one at a time, the end result is the same.

the above provides insight into the pros and cons of wayland and x-windowing. from this alone, one might conclude that it should be a user choice based on individual needs and preferences. however, it isn't. wayland is intended to fully replace x-windowing.

and here is where we encounter the trouble with wayland: it breaks apis, which violates the very first and primary rule of linux. it breaks user space.

quoting linus torvalds:

    the biggest thing any program can do is not the technical details of the program itself; it’s how useful the program is to users.

    so any time any program (like the kernel or any other project) breaks the user experience, to me, that’s the absolute worst failure that a software project can make.

without the users, any project is nothing. it is meaningless without a user base because any project is meant to be useful and helpful for those who use it.

on systems using wayland, certain applications like gnome-screenshot are broken. this is why some distributions exclude specific packages and instead include alternative solutions with fewer features and functionality built into the shell. using wayland, nvidia support can be problematic, requiring distributions to default back to x-windowing to restore functionality. wayland does not respect ewmh protocols and breaks cli tools like xprop, xrandr, and wmctrl, preventing user control and access to display management features like refresh rate and resolution.

wayland disrupts x11 applications, with a temporary solution in the form of xwayland, which provides only basic support for these applications on wayland. it also breaks screen-sharing and remote desktop applications, window management—hence why wayland is not supported on xfce or many other desktop environments—and accessibility tools and assistive technologies, which is a significant issue.

wayland also compromises many features of multi-monitor support, such as display hotplugging, resolution management, display arrangement, and other functionalities.

the core problem is that whenever wayland breaks something, the blame is shifted onto everyone else. they claim that app developers need to make wayland compliant, distributions need to conform to their standards, and users must adapt to wayland. the responsibility is placed on all non-wayland parties to comply with wayland's requirements. everything that breaks requires workarounds or waiting for others to provide fixes.

this contradicts the essence of linux: do not break user space. if an api breaks user space, it must be reverted. no regressions. wayland disregards the user base that gives linux its purpose because wayland is not for the users but for the developers. it disrupts users' workflows and their expectations of application features and functionality. while there are some advantages, in the end, wayland shifts the blame for its issues onto the users, who were given no choice and whose input was not considered.

they expect us to accept what they offer. whether you think wayland is better or x is better becomes irrelevant. what matters is the users, and wayland's disregard for users mirrors the direction of other developers. much like microsoft and google, wayland represents the very things people turned to linux to avoid. linux was chosen because it upholds the rule: do not break user space.

that is the trouble with wayland.
