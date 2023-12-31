#Модель сущность-связь:

## Сущности:

#### Студент
Атрибуты: ИД_студента (Primary Key), Имя, Фамилия, Дата_рождения, Группа, Статус (зачислен, переведен, отчислен, в академическом отпуске), Дата_зачисления, Дата_отчисления.
#### Группа
Атрибуты: ИД_группы (Primary Key), Название_группы, Курс, Специальность.
#### Факультет
Атрибуты: ИД_факультета (Primary Key), Название_факультета.
#### Кафедра
Атрибуты: ИД_кафедры (Primary Key), Название_кафедры.
#### Учебный_план
Атрибуты: ИД_учебного_плана (Primary Key), Специальность, Количество_часов, Предмет, Курс.

## Связи:

#### Студент-Группа
Отношение: Один ко Многим (Один студент может быть в одной группе, но группа содержит множество студентов).
#### Студент-Кафедра
Отношение: Многие ко Многим (Студент может быть на разных кафедрах, кафедра может содержать множество студентов).
#### Группа-Факультет
Отношение: Один ко Многим (Одна группа принадлежит одному факультету, но факультет содержит множество групп).
#### Кафедра-Факультет
Отношение: Один ко Многим (Одна кафедра принадлежит одному факультету, но факультет содержит множество кафедр).
#### Группа-Учебный_план
Отношение: Один ко Многим (Одна группа имеет один учебный план, но на учебном плане может быть много предметов).

# Диаграмма варианта #9 в DFD:

#### Процессы:
Учет_контингента_студентов   
Автоматизация_подготовки_документов   
Поиск_и_просмотр_информации   
Оформление_документации   
Формирование_отчетов   


#### Хранилища данных:
База_данных_студентов   
Архив    
Учебный_план    
База_данных_пользователей   

#### Потоки данных:
Данные_студента   
Данные_группы   
Данные_кафедры   
Данные_учебного_плана   
Документы   
Отчеты   
Ограничения_доступа   
Данные_пользователя   

#### Внешние сущности:
Декан_факультета   
Заведующий_кафедрой   
Методист   

# Примечание
 - Процессы могут включать в себя логику и взаимодействие с базой данных.
 - Данные могут быть переданы в виде потоков данных между процессами, хранилищами данных и внешними сущностями.
 - Ограничения доступа могут быть реализованы через соответствующие проверки при обращении к базе данных.
 - Дополнительные процессы и связи могут быть добавлены в зависимости от конкретных требований и особенностей реализации.
