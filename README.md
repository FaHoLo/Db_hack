# Правим электронный дневник

Проект предназначен для работы с базой данных школьного электронного [дневника](https://github.com/devmanorg/e-diary).

### Список скриптов

1. `fix_marks(child_name)` - исправляет все отрицательный оценки ученика на пятерки.
2. `remove_chastisements(child_name)` - удаляет все замечания ученика.
3. `create_commendation(child_name, subject_name)` - добавляет похвалу ученику на последнем уроке выбранного предмета.

### Как использовать

1. Копируем файл `scripts.py` в папку проекта (рядом с `manage.py`)
2. Подключаемся к базе данных школьного дневника в режиме `shell`:
```
python manage.py shell
```
3. Подключаем скрипты
```
import scripts
```
4. Выполняем требуемый скрипт
```
scripts.script_name(first_argument, second_argument, ...)
```
### Аргументы скриптов

1. `child_name` - ФИО ученика с заглавных букв в именительном падеже. Строковая переменная.
2. `subject_name` - название предмета как в расписании, первая буква - заглавная. Строковая переменная.

**Примеры:**
```
scripts.fix_marks('Пупкин Василий Иванович')
scripts.remove_chastisements('Пупкин Василий Иванович')
scripts.create_commendation('Пупкин Василий Иванович', 'Математика')
```
Возможно использование только фамилии и имени ученика вместо ФИО, однако, если в школе учатся два ученика с одинаковыми ФИ, используйте полное ФИО, иначе скрипт выведет ошибку:
```
scripts.fix_marks('Пупкин Василий')
...
datacenter.models.Schoolkid.MultipleObjectsReturned: get() returned more than one Schoolkid -- it returned 2!
```

При введении имени с ошибкой или несуществующего имени скрипт выведет ошибку:
```
scripts.remove_chastisements('Пупкин Васлий')
...
datacenter.models.Schoolkid.DoesNotExist: Schoolkid matching query does not exist.
```
Похожая ошибка отобразится при неправильном названии предмета.

### Цель проекта

Код написан в образовательных целях на онлайн-курсе для веб-разработчиков [dvmn.org](https://dvmn.org/).
