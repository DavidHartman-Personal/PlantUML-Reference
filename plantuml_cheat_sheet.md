---
layout: default
title:  PlantUML
---

[PlantUML](http://plantuml.sourceforge.net/) is a component that allows to quickly write.
This is cheat sheet of PlantUML to use frequently.

Tempaltes/Examples:

[component-template.puml](Component/component-template.puml) - Shows component diagram/template.  Includes grouping, etc.


## Basic

## Examples

## Common

Notes and Comments.
[Title](images/title/png)

|   keyword    |       usage       |image                                        |
|:------------:|:-----------------:|:--------------------------------------------|
|   `title`    |       Title       |![Title](images/parts/title.png "Title")     |
|`note left :` |    Notes Left     |![Title](images/parts/note_left.png "Title") |
|`note right :`|    Notes Right    |![Title](images/parts/note_right.png "Title")|
|     `' `     |Single-line Comment|                                             |
|   `/' '/`    |   Block Comment   |                                             |


### Code

```plantuml
@startuml
title Notes and Comments
node one
note left: this is a note on the left side

node two
note right: this is a note on the right side
@enduml
```

### Draw

![basic_common](/draw_uml/assets/img/diagrams/basic/common.png)

## Archimate Sprites

Participants and Sequence Actors

![archimate_sprites_1](images/archimate_sprites_1.png "Archimate Icons")

```plantuml
@startuml
participant Participant as Foo
actor       Actor       as Foo1
boundary    Boundary    as Foo2
control     Control     as Foo3
entity      Entity      as Foo4
database    Database    as Foo5
collections Collections as Foo6
queue       Queue       as Foo7
Foo -> Foo1 : To actor 
Foo -> Foo2 : To boundary
Foo -> Foo3 : To control
Foo -> Foo4 : To entity
Foo -> Foo5 : To database
Foo -> Foo6 : To collections
Foo -> Foo7: To queue
@enduml

```

## Arrow

Arrow direction.

| keyword    | usage   | image
|:----------:|:-------:|
| `-up->`    | Up      | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/up_line.png)
| `-down->`  | Down    | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/down_line.png)
| `-left->`  | Left    | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/left_line.png)
| `-right->` | Right   | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/right_line.png)

### Code

```
up -up-> right
-right-> down
-down-> left
-left-> up
```

### Draw

![basic_participant](/draw_uml/assets/img/diagrams/basic/arrow.png)


# UML

## Use Case

Represent the required functions.

|keyword|     usage     |image                                                             |
|:-----:|:-------------:|:-----------------------------------------------------------------|
| `( )` |   Use Case    |![parts_usecase](/draw_uml/assets/img/diagrams/parts/usecase.png) |
| `->`  |      Use      |![parts_usecase](/draw_uml/assets/img/diagrams/parts/use_line.png)|
| `.>`  |Extend, Include|![parts_usecase](/draw_uml/assets/img/diagrams/parts/ext_line.png)|


* [others](http://plantuml.sourceforge.net/usecase.html)

### Code

```
actor Promoter
actor Entrant

Promoter --> (Create Event)
Promoter -> (Attend Event)

Entrant --> (Find Event)
(Attend Event) <- Entrant

(Attend Event) <.. (Create Member)  : <<include>>
```

### Draw

![usecase_diagram](/draw_uml/assets/img/diagrams/usecase.png)

## Activity

Represent the state of the process.

|keyword | usage  |image                                                                 |
|:------:|:------:|:---------------------------------------------------------------------|
| `" "`  |Activity|![parts_usecase](/draw_uml/assets/img/diagrams/parts/activity.png)    |
|`(*) ->`|Initial |![parts_usecase](/draw_uml/assets/img/diagrams/parts/initial_line.png)|
|`-> (*)`| Final  |![parts_usecase](/draw_uml/assets/img/diagrams/parts/final_line.png)  |
[]

* [others](http://plantuml.sourceforge.net/activity.html)

### Code

```
(*) --> "Find Event"
"Find Event" -> "Attend Event"

if "Capacity?" then
  ->[ok] "Create Ticket"
else
  -->[full] if "Standby?" then
    ->[ok] "Standby Ticket"
  else
    -->[no] "Cancel Ticket"
    "Cancel Ticket" --> (*)
  endif
endif

"Create Ticket" --> ==show==
"Standby Ticket" --> ==show==
==show== --> "Show Ticket"
"Show Ticket" --> (*)
```

### Draw

![activity_diagram](/draw_uml/assets/img/diagrams/activity.png)

## State

Represent the state of the objects.

| keyword    | usage   | image
|:----------:|:-------:|
|  `[*] ->`  | Initial | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/initial_line.png)
|  `-> [*]`  | Final   | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/final_line.png)

* [others](http://plantuml.sourceforge.net/state.html)

### Code

```
[*] --> active

active -right-> inactive : disable
inactive -left-> active  : enable

inactive --> closed  : close
active --> closed  : close

closed --> [*]
```

### Draw

![state_diagram](/draw_uml/assets/img/diagrams/state.png)

## Sequence

Represent the messages and  orders of the interacts.

| keyword  | usage   | image
|:--------:|:-------:|
| `->`     | Message | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/message_line.png)
| `<--`    | Return  | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/return_line.png)

* [others](http://plantuml.sourceforge.net/sequence.html)

### Code

```
actor Entrant

Entrant -> Ticket : Attend Event Request

activate Ticket
Ticket -> Member : Create Member Request

activate Member
Member -> Member : Create Member
Ticket <-- Member : Create Member Response
deactivate Member

Ticket -> Ticket : Create Ticket
Entrant <-- Ticket : Attend Event Response
deactivate Ticket
```

### Draw

![sequence_diagram](/draw_uml/assets/img/diagrams/sequence.png)

## Object

Represent the logical view of the object.

| keyword  | usage       | image
|:--------:|:-----------:|
| `object` | Object      | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/object.png)
| `<|-`    | Extension   | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/extension_line.png)
| `*-`     | Composition | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/composition_line.png)
| `o-`     | Agregation  | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/agregation_line.png)

* [others](http://plantuml.sourceforge.net/objects.html)

### Code

```
object User
object Group
object Member

object Event
object Ticket

User . Group
User o.. Member
Group o.. Member

Group o. Event
Event o.. Ticket
Member . Ticket
```

### Draw

![object_diagram](/draw_uml/assets/img/diagrams/object.png)

## Class

Represent the logical view of the class.

| keyword | usage     | image
|:-------:|:---------:|
| `class` | Class     | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/class.png)
| `+`     | Public    | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/public_visibility.png)
| `-`     | Private   | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/private_visibility.png)
| `#`     | Protected | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/protected_visibility.png)
| `~`     | Package   | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/package_visibility.png)

* [others](http://plantuml.sourceforge.net/class.html)

### Code

```
class User {
  username
  password
  +sign_in()
}

class Group {
  name
}

class Member {
  roles
}

User .. Member
Group .. Member
```

### Draw

![class_diagram](/draw_uml/assets/img/diagrams/class.png)

## Component

Represent the dependency of the components.

| keyword    | usage      | image
|:----------:|:----------:|
| `[ ]`      | Component  | ![parts_usecase](/draw_uml/assets/img/diagrams/parts/component.png)
| `package`  | Package    | ![parts_usecase](/draw_uml/assets/img/diagrams/package/package.png)
| `frame`    | Frame      | ![parts_usecase](/draw_uml/assets/img/diagrams/package/frame.png)
| `folder`   | Folder     | ![parts_usecase](/draw_uml/assets/img/diagrams/package/folder.png)
| `database` | Database   | ![parts_usecase](/draw_uml/assets/img/diagrams/package/database.png)
| `node`     | Node       | ![parts_usecase](/draw_uml/assets/img/diagrams/package/node.png)
| `cloud`    | Cloud      | ![parts_usecase](/draw_uml/assets/img/diagrams/package/cloud.png)

* [others](http://plantuml.sourceforge.net/component.html)

### Code

```
cloud "Cloud" {
  package "Package" {
    [register]
    frame "frame" {
      [backup]
    }
  }
}

node "Node" {
  database "Database" {
    [store]
  }
  folder "Folder" {
    [File]
  }
}

[register] .. [store] : HTTP
[backup] .. [File] : FTP
```

### Draw

![component_diagram](/draw_uml/assets/img/diagrams/component.png)


## Colors
We can add colors to Arrows, Icons, Sprites, Components, Packages, etc.
PlantUML support Hexadecimal colors or colors that are already defined.

Site Reference: http://plantuml.com/skinparam

### Code

```
' =================
' == Declaration ==
' =================

[Component 1]

node "Node 1" {
    package "Package 1" #Orange {
        [Component 4]
        [Component 3]
    }
    [Component 2]
}



' ====================
' == Implementation ==
' ====================


node "Node 1" {
    [Component 2] .[#Green]-> [Component 4]
    [Component 3] <-left-> [Component 4]
    [Component 4] -- [Component 1]
}
```

### Draw
![component_diagram](/draw_uml/assets/img/diagrams/colors.png)

## Legends

Legend can contain only text, or some tables.
This example contain a table with some HTML inside and OpenIconic.

OpenIconic Reference: http://plantuml.com/openiconic

### Code

```
legend
    |= Color |= Type |= Description |
    | <size:11><back:#Crimson>           </back></size>|    <&arrow-right> | Example 1 |
    | <size:11><back:#LightSeaGreen>           </back></size>|    <&arrow-right> | Example 2 |
    | <size:11><back:#DarkGreen>           </back></size>|    <&arrow-right> | Example 3 |
    | <size:11><back:#YellowGreen>           </back></size>|    <&box> | Example 4 |
    | <size:11><back:#Chocolate>           </back></size>|    <&box> | Example 5 |
endlegend
```

### Draw
![component_diagram](/draw_uml/assets/img/diagrams/legend.png)


## Constants
It's possible to declare constants that will help us for example to include files or other *.puml

PS: when you use it remove ${}, thats only there for the example

### Code
```
!define ${VARIABLE NAME} ${VARIABLE VALUE}
```

## Sprites & Includes
There are a lot of useful sprites and images that we can use.
In the next example you have all the ways to implement components using this open source library.

### Code
```
!include <font-awesome/common>

!define ICONURL https://raw.githubusercontent.com/Roemer/plantuml-office/master/office2014
!includeurl ICONURL/Servers/application_server.puml

' =================
' == Declaration ==
' =================

OFF_APPLICATION_SERVER([Component 1], "Component 1", component, #Green)

node "Node 1" {
    package "Package 1" #Orange {
        OFF_APPLICATION_SERVER([Component 4], "Component 4")
        OFF_APPLICATION_SERVER(Component3, "Component 3", component)
    }
    OFF_APPLICATION_SERVER([Component 2])
}



' ====================
' == Implementation ==
' ====================


node "Node 1" {
    [Component 2] .[#Green]-> [Component 4]
    Component3 <-left-> [Component 4]
    [Component 4] -- [Component 1]
}
```

### Draw
![component_diagram](/draw_uml/assets/img/diagrams/sprites.png)
SAVE TO CACHER