# Aufgabe 2.1

## Kontext verstehen

> **Wer sind die primären Nutzenden des Systems?**

- Someone who wants to play "6 Nimmt" or other cardgame online, probably young people, in search for a quick online cardgame and don't have a real card in presence

> **Weshalb wollen die Nutzenden das System einsetzen(Motivation)?**

- To kill some time, have fun during their fragmented spare time(On traveling, on bus or train)

> **Wofür wollen die Nutzenden das System einsetzen(Aufgaben)?**

**I just list some the possible use cases, not all the use cases have to be implemented in the end, just an overview**

- Registration(not necessary but it is easy to implement and it can be optimized)
- Login and Logout
- Choose one of cardgames from the list(optional stuff, extensible, not necessary to have such list)
- Choose one play room to enter
	1. create a new empty room(become the room-owner and have the right to start the game when there are enough players in the room)
	2. enter an already existing room(become a guest, wait for the room-owner to start the game)
- In the game:
	1. player can discard one card every round
	2. player can quit in the middle of the game(how to handle this, we have 2 choices: 1. The server will take the place of the player; 2. Just end up the game without winner)
	3. there should be one countdown for every player to show the time limit, after that time, computer will randomly choose one card to discard.

> **In welcher Umgebung wollen die Nutzenden das System einsetzen(Umgebung/Kontext)?**

- When someone wants to kill their free time(on traveling, on bus, train or some other public vehicle).
- When people attending a party and want to do something to have fun(on a home party, tandom partner party or something else).

## Aufgaben analysieren

> Entwickeln Sie ein Verständnis für die Art und Weise der Aufgabenbewältigung, indem Sie eine Hierarchische Taskanalyse (HTA) für die ermittelten Aufgaben Ihres Systems durchführen.

- Use case of registration login and logout

```plantuml
left to right direction
skinparam packageStyle rectangle
actor Benutzer
rectangle Anmelden_Login_Logout_System {
	Benutzer --> (anmelden)
	Benutzer --> (log in)
	Benutzer --> (log out)
}
```

- Use case of enter a room

@startuml
left to right direction
skinparam packageStyle rectangle
actor Benutzer
rectangle Raum_eintreten_austreten {
	Benutzer --> (Raum Liste ansehen)
	Benutzer --> (Raum eintreten)
	Benutzer --> (Raum austreten)
	(Raum eintreten) <-- (einen neuen Raum erstellen) 
	(Raum eintreten) <-- (einen bestehenden Raum eintreten)
	(einen neuen Raum erstellen) <.. (Game starten) : extend
	(einen bestehenden Raum eintreten) <.. (bereit machen): extend
}
@enduml

- Use case of playing game

@startuml
left to right direction
skinparam packageStyle rectangle
actor Benutzer
rectangle Game_spielen {
	Benutzer --> (Karten spielen)
	Benutzer --> (Game beenden)
}
@enduml

---

- Hierarchical Task Analysis (HTA)

- HTA of Registration

@startuml
artifact registration
artifact [input user name]
artifact [input pwd]
artifact [click "register" button]
registration --> [input user name]
registration --> [input pwd]
registration --> [click "register" button]
@enduml

@startwbs
* Business Process Modelling WBS
** Launch the project
*** Complete Stakeholder Research
*** Initial Implementation Plan
** Design phase
*** Model of AsIs Processes Completed
**** Model of AsIs Processes Completed1
**** Model of AsIs Processes Completed2
*** Measure AsIs performance metrics
*** Identify Quick Wins
** Complete innovate phase
@endwbs

