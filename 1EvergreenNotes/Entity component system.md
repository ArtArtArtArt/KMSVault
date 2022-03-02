#programming/gamedev #interview 

A popular blog series by Adam Martin define what he believes to be an Entity Component System.

Martin's definitions and terminology:[[2]](https://en.wikipedia.org/wiki/Entity_component_system#cite_note-ES-MMOG-2-2)

-   Entity: The entity is a general-purpose object. Usually, it only consists of a unique id. They "tag every coarse gameObject as a separate item". Implementations typically use a plain integer for this.[[6]](https://en.wikipedia.org/wiki/Entity_component_system#cite_note-ESWiki-6)
-   Component: the raw data for one aspect of the object, and how it interacts with the world. "Labels the Entity as possessing this particular aspect". Implementations typically use [structs](https://en.wikipedia.org/wiki/C_structures_and_unions "C structures and unions"), [classes](https://en.wikipedia.org/wiki/C%2B%2B_classes "C++ classes"), or [associative arrays](https://en.wikipedia.org/wiki/Associative_array "Associative array").[[6]](https://en.wikipedia.org/wiki/Entity_component_system#cite_note-ESWiki-6)
-   System: "Each System runs continuously (as though each System had its own private thread) and performs global actions on every Entity that possesses a Component or Components that match that Systems query."

