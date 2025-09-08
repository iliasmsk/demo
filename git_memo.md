@startuml
hide footbox
skinparam sequenceMessageAlign center
skinparam sequenceArrowThickness 2
skinparam roundcorner 10
skinparam ParticipantPadding 20

participant User
participant Folder	
participant Index
participant Local
participant Remote

rnote across #FFF2CC: ИНИЦИАЦИЯ
User -> Folder: git init
rnote over Folder
Папка .git
end note
User -> Folder: git status
rnote over Folder
Статус репозитория
end note
User -> Folder: git log -p <path/filename.md>
rnote over Folder
Посмотреть всю историю файла
end note
Remote -> Folder: git pull = git fetch + git merge
rnote over Folder
Посмотреть и применить
end note

rnote across #FFF2CC: ПУБЛИКАЦИЯ
User -> Folder: Модификация файла
rnote over Folder
"modified"
end note
Folder -> Index: git add <file>
rnote over Index
"staged"
end note
Index -> Local: git commit - m <"Сообщение">
Local -> Remote: git push

rnote across #FFF2CC: ОТКАТЫ
Folder --> Folder: git restore <file>
rnote over Folder
unmodified, 1 файл
end note
Index --> Folder: git restore --staged <file>
rnote over Folder
"modified"
end note
Local --> Index: git reset --soft HEAD~1
rnote over Index
"staged"
end note
Local --> Folder: git reset --mixed HEAD~1
rnote over Folder
"modified"
end note
Local --[#red]> Folder: git reset --hard HEAD~1
rnote over Folder
unmodified, все файлы!
end note
@enduml
