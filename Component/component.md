## Component Diagram

Let's have few examples.

## Components
Components must be bracketed.

You can also use the ``component`` keyword to define a
component.
And you can define an alias, using the ``as``
keyword.  This alias will be used later, when defining relations.

```plantuml
@startuml

[First component]
[Another component] as Comp2
component Comp3
component [Last\ncomponent] as Comp4

@enduml
```


## Interfaces

Interface can be defined using the ``()`` symbol (because this looks like a circle).

You can also use the ``interface`` keyword to define an interface.
And you can define an alias, using the ``as`` keyword.
This alias will be used latter, when defining relations.

We will see latter that interface definition is optional.
```plantuml
@startuml

() "First Interface"
() "Another interface" as Interf2
interface Interf3
interface "Last\ninterface" as Interf4

[component]
footer //Adding "component" to force diagram to be a **component diagram**//
@enduml
```


## Basic example



Links between elements are made using combinations of dotted line
(``..``), straight line (``--``), and arrows (``-->``)
symbols.
```plantuml
@startuml

DataAccess - [First Component]
[First Component] ..> HTTP : use

@enduml
```


## Using notes

You can use the
``note left of`` , ``note right of`` ,
``note top of`` , ``note bottom of``
keywords to define notes related to a single object.

```plantuml
@startuml
[Component] as C

note top of C: A top note

note bottom of C
  A bottom note can also
  be on several lines
end note

note left of C
  A left note can also
  be on several lines
end note

note right of C: A right note
@enduml
```

A note can be also defined alone with the ``note``
keywords, then linked to other objects using the ``..`` symbol or whatever arrow symbol (``-``, ``--``, ...).
```plantuml
@startuml
[Component] as C

note as N
  A floating note can also
  be on several lines
end note

C .. N
@enduml
```

Another note example:
```plantuml
@startuml

interface "Data Access" as DA

DA - [First Component]
[First Component] ..> HTTP : use

note left of HTTP : Web Service only

note right of [First Component]
  A note can also
  be on several lines
end note

@enduml
```


## Grouping Components

You can use several keywords to group components and interfaces together:
* ``package``
* ``node``
* ``folder``
* ``frame``
* ``cloud``
* ``database``

```plantuml
@startuml

package "Some Group" {
  HTTP - [First Component]
  [Another Component]
}

node "Other Groups" {
  FTP - [Second Component]
  [First Component] --> FTP
}

cloud {
  [Example 1]
}


database "MySql" {
  folder "This is my folder" {
    [Folder 3]
  }
  frame "Foo" {
    [Frame 4]
  }
}


[Another Component] --> [Example 1]
[Example 1] --> [Folder 3]
[Folder 3] --> [Frame 4]

@enduml
```


## Changing arrows direction


By default, links between classes have two dashes ``--`` and are vertically oriented.
It is possible to use horizontal link by putting a single dash (or dot) like this:

```plantuml
@startuml
[Component] --> Interface1
[Component] -> Interface2
@enduml
```

You can also change directions by reversing the link:

```plantuml
@startuml
Interface1 <-- [Component]
Interface2 <- [Component]
@enduml
```

It is also possible to change arrow direction by adding ``left``, ``right``, ``up``
or ``down`` keywords inside the arrow:

```plantuml
@startuml
[Component] -left-> left
[Component] -right-> right
[Component] -up-> up
[Component] -down-> down
@enduml
```

You can shorten the arrow by using only the first character of the direction (for example, ``-d-`` instead of
``-down-``)
or the two first characters (``-do-``).

Please note that you should not abuse this functionality : *Graphviz* gives usually good results without tweaking.


And with the [`left to right direction`](use-case-diagram#d551e48d272b2b07) parameter:
```plantuml
@startuml
left to right direction
[Component] -left-> left
[Component] -right-> right
[Component] -up-> up
[Component] -down-> down
@enduml
```


## Use UML2 notation

By default *(from v1.2020.13-14)*, UML2 notation is used.

```plantuml
@startuml

interface "Data Access" as DA

DA - [First Component]
[First Component] ..> HTTP : use

@enduml
```


## Use UML1 notation

The ``skinparam componentStyle uml1`` command is used to switch to UML1 notation.
```plantuml
@startuml
skinparam componentStyle uml1

interface "Data Access" as DA

DA - [First Component]
[First Component] ..> HTTP : use

@enduml
```


## Use rectangle notation (remove UML notation)

The ``skinparam componentStyle rectangle`` command is used to switch to rectangle notation *(without any UML notation)*.
```plantuml
@startuml
skinparam componentStyle rectangle

interface "Data Access" as DA

DA - [First Component]
[First Component] ..> HTTP : use

@enduml
```


## Long description
It is possible to put description on several lines using square brackets.
```plantuml
@startuml
component comp1 [
This component
has a long comment
on several lines
]
@enduml
```


## Individual colors


You can specify a color after component definition.
```plantuml
@startuml
component  [Web Server] #Yellow
@enduml
```


## Using Sprite in Stereotype
You can use sprites within stereotype components.
```plantuml
@startuml
sprite $businessProcess [16x16/16] {
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFF0FFFFF
FFFFFFFFFF00FFFF
FF00000000000FFF
FF000000000000FF
FF00000000000FFF
FFFFFFFFFF00FFFF
FFFFFFFFFF0FFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
FFFFFFFFFFFFFFFF
}


rectangle " End to End\nbusiness process" <<$businessProcess>> {
 rectangle "inner process 1" <<$businessProcess>> as src
 rectangle "inner process 2" <<$businessProcess>> as tgt
 src -> tgt
}
@enduml
```



## Skinparam

You can use the [skinparam](skinparam)
command to change colors and fonts for the drawing.

You can use this command :
* In the diagram definition, like any other commands;
* In an [included file](preprocessing);
* In a configuration file, provided in the [command line](command-line) or the [Ant task](ant-task).

You can define specific color and fonts for stereotyped components and interfaces.

```plantuml
@startuml

skinparam interface {
  backgroundColor RosyBrown
  borderColor orange
}

skinparam component {
  FontSize 13
  BackgroundColor<<Apache>> Pink
  BorderColor<<Apache>> #FF6655
  FontName Courier
  BorderColor black
  BackgroundColor gold
  ArrowFontName Impact
  ArrowColor #FF6655
  ArrowFontColor #777777
}

() "Data Access" as DA
Component "Web Server" as WS << Apache >>

DA - [First Component]
[First Component] ..> () HTTP : use
HTTP - WS

@enduml
```

```plantuml
@startuml
[AA] <<static lib>>
[BB] <<shared lib>>
[CC] <<static lib>>

node node1
node node2 <<shared node>>
database Production

skinparam component {
    backgroundColor<<static lib>> DarkKhaki
    backgroundColor<<shared lib>> Green
}

skinparam node {
borderColor Green
backgroundColor Yellow
backgroundColor<<shared node>> Magenta
}
skinparam databaseBackgroundColor Aqua

@enduml
```


## Specific SkinParameter

### componentStyle

* By default (or with `skinparam componentStyle uml2`), you have an icon for component
```plantuml
@startuml
skinparam BackgroundColor transparent
skinparam componentStyle uml2
component A {
   component "A.1" {
}
   component A.44 {
      [A4.1]
}
   component "A.2"
   [A.3]
   component A.5 [
A.5]
   component A.6 [
]
}
[a]->[b]
@enduml
```
* If you want to suppress it, and to have only the rectangle, you can use `skinparam componentStyle rectangle`
```plantuml
@startuml
skinparam BackgroundColor transparent
skinparam componentStyle rectangle
component A {
   component "A.1" {
}
   component A.44 {
      [A4.1]
}
   component "A.2"
   [A.3]
   component A.5 [
A.5]
   component A.6 [
]
}
[a]->[b]
@enduml
```

*[Ref. [10798](https://forum.plantuml.net/10798)]*


## Hide or Remove unlinked component

By default, all components are displayed:
```plantuml
@startuml
component C1
component C2
component C3
C1 -- C2
@enduml
```

But you can:
* `hide @unlinked` components:
```plantuml
@startuml
component C1
component C2
component C3
C1 -- C2

hide @unlinked
@enduml
```

* or `remove @unlinked` components:
```plantuml
@startuml
component C1
component C2
component C3
C1 -- C2

remove @unlinked
@enduml
```


*[Ref. [QA-11052](https://forum.plantuml.net/11052)]*


## Hide, Remove or Restore tagged component or wildcard

You can put `$tags` (using `$`) on components, then remove, hide or restore components either individually or by tags.

By default, all components are displayed:
```plantuml
@startuml
component C1 $tag13
component C2
component C3 $tag13
C1 -- C2
@enduml
```

But you can:
* `hide $tag13` components:
```plantuml
@startuml
component C1 $tag13
component C2
component C3 $tag13
C1 -- C2

hide $tag13
@enduml
```

* or `remove $tag13` components:
```plantuml
@startuml
component C1 $tag13
component C2
component C3 $tag13
C1 -- C2

remove $tag13
@enduml
```

* or `remove $tag13 and restore $tag1` components:
```plantuml
@startuml
component C1 $tag13 $tag1
component C2
component C3 $tag13
C1 -- C2

remove $tag13
restore $tag1
@enduml
```

* or ``remove * and restore $tag1`` components:
```plantuml
@startuml
component C1 $tag13 $tag1
component C2
component C3 $tag13
C1 -- C2

remove *
restore $tag1
@enduml
```

*[Ref. [QA-7337](https://forum.plantuml.net/7337) and [QA-11052](https://forum.plantuml.net/11052)]*


SAVE TO CACHER