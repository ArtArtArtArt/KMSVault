---
status: ⚙️
tags:
 - programming/gamedev/gameEngine 
---

# communication between subsystems of a game engine

https://www.reddit.com/r/gamedev/comments/qld41j/how_to_handle_communcation_between_subsystems_of/?utm_source=pocket_mylist

Like you mentioned, an event system is a common approach from what I've seen. You can also poll a singleton input manager like how unity does it. The input manager handles events from the os and the subsystems poll the manager for current state for the frame in question