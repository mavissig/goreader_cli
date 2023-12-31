# goreader

Implementation of a utility for reading and comparing json and xml files

Author : [Egor Kondratov(mavissig)](https://github.com/mavissig)

## Contents

---

0. [Preamble](#preamble)
1. [Introduction](#introduction)
2. [Information](#information)
3. [About the program](#about-the-program) \
   3.1. [GoReader](#goreader-1) \
   3.2. [Settings](#settings)


## Preamble

---


В рамках Учебного проекта я написал программу, позволяющую выводить в stdout и сравнивать файлы.

Во главе угла я ставил задачу разобраться как в golang работают преобразования файлов типа json и xml.

Приятного просмотра и чистого кода.

## Introduction

---

В данном проекте я реализовал на языке программирования Go программу, которой можно на вход подать файл xml 
и она конвертирует его в xml или наоборот

Второй функцией программы является сравнение двух файлов, неважно будут они переданы в формате json или xml

## Information

---

### JSON файлы

JSON (JavaScript Object Notation) - это легкий текстовый формат обмена данными, предназначенный для удобного чтения данных. JSON легко читать и писать.

#### Синтаксис JSON

JSON-данные записываются в виде пар "имя/значение" (также известных как пары "ключ/значение"). Пара "имя/значение" состоит из имени поля (в двойных кавычках), за которым следует двоеточие, за которым следует значение. Имена JSON требуют двойных кавычек. Формат JSON почти идентичен объектам JavaScript. В JSON ключами могут быть строки, записанные в двойных кавычках.

В JSON значениями могут быть следующие типы данных:
- строка
- число
- объект
- массив
- булево значение
- null

#### файлы

Строка JSON может быть сохранена в своем собственном файле, который в основном является просто текстовым файлом с расширением .json и MIME-типом application/json.

#### Ссылки JSON

Ссылка JSON - это отображение с уникальным ключом $ref, значение которого является указателем JSON. Значение <ссылка> - это ссылка JSON, состоящая из двух частей <относительный путь к файлу или URL><указатель JSON>. Возможные значения:
- пусто (для ссылки на текущий документ)
- путь (относительно текущего файла)
- URL (включая протокол)

Указатель. Возможные значения:
- пусто (для ссылки на весь файл - это то же самое, что и #).
- с путем к объекту (ссылается на корень документа).
- Каждый сегмент пути должен иметь предшествующий его / (например, #/foo).

#### Общие ошибки

- Нет соседей. Спецификация OpenAPI говорит: Этот объект не может быть расширен дополнительными свойствами, и любые добавленные свойства ДОЛЖНЫ быть проигнорированы.
- Неправильный путь к $ref. Путь оценивается от самого файла. Использование путей относительно корневого файла является распространенной ошибкой.
- Использование ссылок на запрещенные свойства. Чтобы строго соответствовать OpenAPI 3.x, ссылка JSON может быть использована только там, где это явно отмечено в спецификации OpenAPI. Например, она может быть использована для путей, параметров, объектов схемы и многого другого. В противном случае, всякий раз, когда может быть использован объект схемы, вместо него может быть использован объект ссылки..

Пример JSON файла:
```json
{
  "cake": [
    {
      "name": "Red Velvet Strawberry Cake",
      "time": "45 min",
      "ingredients": [
        {
          "ingredient_name": "Flour",
          "ingredient_count": "2",
          "ingredient_unit": "mugs"
        },
        {
          "ingredient_name": "Strawberries",
          "ingredient_count": "8"
        },
        {
          "ingredient_name": "Coffee Beans",
          "ingredient_count": "2.5",
          "ingredient_unit": "tablespoons"
        },
        {
          "ingredient_name": "Cinnamon",
          "ingredient_count": "1"
        }
      ]
    },
    {
      "name": "Moonshine Muffin",
      "time": "30 min",
      "ingredients": [
        {
          "ingredient_name": "Brown sugar",
          "ingredient_count": "1",
          "ingredient_unit": "mug"
        },
        {
          "ingredient_name": "Blueberries",
          "ingredient_count": "1",
          "ingredient_unit": "mug"
        }
      ]
    }
  ]
}
```

### XML файлы

XML (eXtensible Markup Language) - это язык разметки, похожий на HTML, но без предопределенных тегов для использования. Вместо этого вы определяете свои собственные теги, специально разработанные для ваших потребностей. Это мощный способ хранения данных в формате, который может быть сохранен, проиндексирован и поделен.

#### Синтаксис XML

XML-документы могут иметь ссылку на DTD или на XML Schema. XML-документы записываются в виде пар "имя/значение". Пара "имя/значение" состоит из имени поля, за которым следует двоеточие, за которым следует значение.

В XML значениями могут быть следующие типы данных:
- строка
- число
- объект
- массив
- булево значение
- null

#### файлы

Строка XML может быть сохранена в своем собственном файле, который в основном является просто текстовым файлом с расширением .xml.

#### Ссылки XML

Ссылка XML - это отображение с уникальным ключом $ref, значение которого является указателем XML. Значение <ссылка> - это ссылка XML, состоящая из двух частей <относительный путь к файлу или URL><указатель XML>. Возможные значения:
- пусто (для ссылки на текущий документ)
- путь (относительно текущего файла)
- URL (включая протокол)

Указатель. Возможные значения:
- пусто (для ссылки на весь файл - это то же самое, что и #).
- с путем к объекту (ссылается на корень документа).
- Каждый сегмент пути должен иметь предшествующий его / (например, #/foo).

#### Общие ошибки

- Нет соседей. Спецификация OpenAPI говорит: Этот объект не может быть расширен дополнительными свойствами, и любые добавленные свойства ДОЛЖНЫ быть проигнорированы.
- Неправильный путь к $ref. Путь оценивается от самого файла. Использование путей относительно корневого файла является распространенной ошибкой.
- Использование ссылок на запрещенные свойства. Чтобы строго соответствовать OpenAPI 3.x, ссылка XML может быть использована только там, где это явно отмечено в спецификации OpenAPI. Например, она может быть использована для путей, параметров, объектов схемы и многого другого. В противном случае, всякий раз, когда может быть использован объект схемы, вместо него может быть использован объект ссылки..

Пример XML файла:
```xml
<recipes>
    <cake>
        <name>Red Velvet Strawberry Cake</name>
        <stovetime>40 min</stovetime>
        <ingredients>
            <item>
                <itemname>Flour</itemname>
                <itemcount>3</itemcount>
                <itemunit>cups</itemunit>
            </item>
            <item>
                <itemname>Vanilla extract</itemname>
                <itemcount>1.5</itemcount>
                <itemunit>tablespoons</itemunit>
            </item>
            <item>
                <itemname>Strawberries</itemname>
                <itemcount>7</itemcount>
                <itemunit></itemunit> <!-- itemunit may be empty  -->
            </item>
            <item>
                <itemname>Cinnamon</itemname>
                <itemcount>1</itemcount>
                <itemunit>pieces</itemunit>
            </item>
            <!-- Here can be more ingredients  -->
        </ingredients>
    </cake>
    <cake>
        <name>Blueberry Muffin Cake</name>
        <stovetime>30 min</stovetime>
        <ingredients>
            <item>
                <itemname>Baking powder</itemname>
                <itemcount>3</itemcount>
                <itemunit>teaspoons</itemunit>
            </item>
            <item>
                <itemname>Brown sugar</itemname>
                <itemcount>0.5</itemcount>
                <itemunit>cup</itemunit>
            </item>
            <item>
                <itemname>Blueberries</itemname>
                <itemcount>1</itemcount>
                <itemunit>cup</itemunit>
            </item>
            <!-- Here can be more ingredients  -->
        </ingredients>
    </cake>
    <!-- Here can be more cakes  -->
</recipes>
```

## About the program

---

## GoReader

Разработана программа для выводаи сравнения json и xml файлов:

- Программа разработана на языке Golang.
- Программа разработана в соответствии с принципами "Чистой архитектуры"
- При написании кода придерживался SOLID
- Программа предоставляет возможность:
    - Загружать json или xml файлы при включенном флаге -f
    - Загружать json и/или xml файлы с флагами --old --new для сравнения
- В данной версии программа корректно обрабатывает json и xml файлы составленные по примеру приведенному выше

## Settings

- Запуск с флагом -f переводит программу в режим ConvertAndString, это режим при котором формат конвертируется в противоположный и выводится в stdout