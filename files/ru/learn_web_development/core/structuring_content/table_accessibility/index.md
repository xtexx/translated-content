---
title: HTML таблицы продвинутые возможности и доступность
slug: Learn_web_development/Core/Structuring_content/Table_accessibility
---

{{LearnSidebar}}{{PreviousMenuNext("Learn/HTML/Tables/Basics", "Learn/HTML/Tables/Structuring_planet_data", "Learn/HTML/Tables")}}

Во второй статье этого модуля мы рассматриваем ещё несколько продвинутых возможностей в HTML таблицах — такие как заголовок/описание и группировка строк внутри head, body и footer секциях таблицы, а также доступность таблиц для пользователей с ограниченными возможностями.

| Необходимые знания: | Базовый HTML ([Введение в HTML](/ru/docs/conflicting/Learn_web_development/Core/Structuring_content)). |
| ------------------- | ------------------------------------------------------------------------------------------------------ |
| Цель:               | Изучить более продвинутые возможности HTML таблиц и их доступность.                                    |

## Добавление заголовка к таблице с помощью \<caption>

Вы можете добавить заголовок для таблицы установив его в элементе {{htmlelement("caption")}} и этот элемент необходимо поместить внутрь элемента {{htmlelement("table")}}. Причём вам нужно поместить его сразу после открытия тега `<table>`.

```html
<table>
  <caption>
    Dinosaurs in the Jurassic period
  </caption>

  ...
</table>
```

Как можно понять из короткого примера выше, заголовок отражает в себе описание контента таблицы. Это полезно для всех читателей просматривающих страницу и желающих получить краткое представление от том полезна ли для них таблица, что особенно важно для слепых пользователей. Вместо того чтобы читать содержимое множества ячеек чтобы понять о чем таблица, он или она могут полагаться на заголовок и принимать решение читать ли таблицу более подробно.

Заголовок помещают сразу после тега `<table>`.

> [!NOTE]
> Атрибут [`summary`](/ru/docs/Web/HTML/Element/table#summary) также может быть использован в элементе `<table>` для добавления описания, которое также будет распознано программами для чтения с экрана. Однако мы рекомендуем вместо этого использовать элемент `<caption>`, так как `summary` является устаревшим и не может быть прочитан зрячими пользователями (он не отображается на странице).

### Упражнение: Добавление заголовка

Давайте попробуем это, вернёмся к примеру который мы ранее встретили в прошлой статье.

1. Откройте расписание занятий школьного учителя по языку в конце статьи [HTML таблицы основы](/ru/docs/Learn_web_development/Core/Structuring_content/HTML_table_basics#active_learning_colgroup_and_col) или сделайте копию нашего [timetable-fixed.html](https://github.com/mdn/learning-area/blob/master/html/tables/basic/timetable-fixed.html) файла.
2. Добавьте подходящий заголовок к таблице.
3. Сохраните свой код и откройте его в браузере, чтобы посмотреть как это выглядит.

> [!NOTE]
> Этот пример можно найти на GitHub по ссылке [timetable-caption.html](https://github.com/mdn/learning-area/blob/master/html/tables/advanced/timetable-caption.html) ([живой пример](https://mdn.github.io/learning-area/html/tables/advanced/timetable-caption.html)).

## Добавление структуры с помощью \<thead>, \<tfoot> и \<tbody>

Когда таблицы становятся более сложными по структуре полезно дать им более структурированное определение. Отличный способ сделать это используя {{htmlelement("thead")}}, {{htmlelement("tfoot")}} и {{htmlelement("tbody")}}, которые позволяют вам разметить header, footer и body секции таблицы.

Эти элементы не создают дополнительной доступности для пользователей со скринридерами и не приводят к какому-то визуальному улучшению при их использовании. Зато они очень полезны при стилизации и разметке, как точки для добавления CSS к вашей таблице. Вот несколько интересных примеров, в случае длинной таблицы вы можете сделать header и footer таблицы повторяемый на каждой печатной странице, или вы можете сделать body таблицы отображаемое на одной странице и иметь доступ ко всему содержимому контенту прокручивая вверх и вниз.

Использование:

- Элементом `<thead>` нужно обернуть часть таблицы которая относится к заголовку — обычно это первая строка содержащая заголовки колонок, но это не обязательно всегда такой случай. Если вы используете {{htmlelement("col")}}/{{htmlelement("colgroup")}} элемент, тогда заголовок должен находиться ниже его.
- Элементом `<tfoot>` нужно обернуть ту часть, которая относится к footer таблицы — например, это может быть последняя строка в которой отражаются суммы по столбцам таблицы. Вы можете включить сюда footer таблицы, как и следовало ожидать, или чуть ниже заголовка таблицы (браузер всё равно отобразит его внизу таблицы).
- Элементом `<tbody>` необходимо обернуть остальную часть содержимого таблицы которая не находится в header или footer таблицы. Этот блок располагают ниже заголовка таблицы или иногда footer таблицы, зависит от того какую структуру вы решите использовать (читать выше по тексту).

> **Примечание:** `<tbody>` всегда есть в каждой таблице, даже если он не указывается коде явно. Вы можете убедиться в этом, открыв один из предыдущих примеров в котором не используется `<tbody>` и посмотрев HTML код в [Developer Tools браузера](/ru/docs/Learn_web_development/Howto/Tools_and_setup/What_are_browser_developer_tools) — вы увидите, что браузер добавил этот тег самостоятельно. Вы могли бы задаться вопросом почему мы должны волноваться о его включении, но вы должны, потому что это даёт больше контроля над структурой таблицы и стилем.

### Упражнение: Добавление структуры таблицы

Давайте используем эти новые элементы.

1. В первую очередь, сделайте копию [spending-record.html](https://github.com/mdn/learning-area/blob/master/html/tables/advanced/spending-record.html) и [minimal-table.css](https://github.com/mdn/learning-area/blob/master/html/tables/advanced/minimal-table.css) в новой папке.
2. Попробуйте открыть это в браузере — вы увидите, что все выглядит классно, но могло бы быть лучше. Строка "SUM" которая содержит потраченные суммы кажется находится не в том месте и некоторые детали отсутствуют в коде.
3. Поместите очевидную строку заголовка внутрь `<thead>` элемента, строку "SUM" внутрь `<tfoot>` элемента и оставшийся контент внутрь `<tbody>` элемента.
4. Сохраните, перезагрузите и вы увидите, что добавление элемента `<tfoot>` привело к тому, что строка "SUM" опустилась к нижней части таблицы.
5. Далее, добавьте атрибут [`colspan`](/ru/docs/Web/HTML/Reference/Elements/td#colspan), чтобы ячейка "SUM" занимала первые четыре столбца, таким образом числовое значение "Cost" появится в последнем столбце.
6. Давайте добавим несколько простых дополнительных стилей к таблице, чтобы дать вам представление насколько эти элементы полезны при использовании CSS. Внутри в `<head>` вашего HTML документа вы увидите пустой элемент {{htmlelement("style")}}. Внутри этого элемента добавьте следующие строки CSS кода:

   ```css
   tbody {
     font-size: 90%;
     font-style: italic;
   }

   tfoot {
     font-weight: bold;
   }
   ```

7. Сохраните, обновите и вы увидите результат. Если `<tbody>` и `<tfoot>` элементы не были установлены, то вам придётся писать много сложных селекторов/правил для применения одного и того же стиля.

> [!NOTE]
> Мы не ожидаем что сейчас вы полностью поймёте CSS. Вы узнаете больше когда пройдёте наши CSS курсы (например, [Введение в CSS](/ru/docs/conflicting/Learn_web_development/Core/Styling_basics) это хорошее место для начала; у нас также есть статья конкретно о [стилизации таблиц](/ru/docs/Learn_web_development/Core/Styling_basics/Tables)).

Ваша готовая таблица должна выглядеть примерно так:

```html hidden
<!doctype html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>My spending record</title>
    <style>
      html {
        font-family: sans-serif;
      }

      table {
        border-collapse: collapse;
        border: 2px solid rgb(200, 200, 200);
        letter-spacing: 1px;
        font-size: 0.8rem;
      }

      td,
      th {
        border: 1px solid rgb(190, 190, 190);
        padding: 10px 20px;
      }

      th {
        background-color: rgb(235, 235, 235);
      }

      td {
        text-align: center;
      }

      tr:nth-child(even) td {
        background-color: rgb(250, 250, 250);
      }

      tr:nth-child(odd) td {
        background-color: rgb(245, 245, 245);
      }

      caption {
        padding: 10px;
      }

      tbody {
        font-size: 90%;
        font-style: italic;
      }

      tfoot {
        font-weight: bold;
      }
    </style>
  </head>
  <body>
    <table>
      <caption>
        How I chose to spend my money
      </caption>
      <thead>
        <tr>
          <th>Purchase</th>
          <th>Location</th>
          <th>Date</th>
          <th>Evaluation</th>
          <th>Cost (€)</th>
        </tr>
      </thead>
      <tfoot>
        <tr>
          <td colspan="4">SUM</td>
          <td>118</td>
        </tr>
      </tfoot>
      <tbody>
        <tr>
          <td>Haircut</td>
          <td>Hairdresser</td>
          <td>12/09</td>
          <td>Great idea</td>
          <td>30</td>
        </tr>
        <tr>
          <td>Lasagna</td>
          <td>Restaurant</td>
          <td>12/09</td>
          <td>Regrets</td>
          <td>18</td>
        </tr>
        <tr>
          <td>Shoes</td>
          <td>Shoeshop</td>
          <td>13/09</td>
          <td>Big regrets</td>
          <td>65</td>
        </tr>
        <tr>
          <td>Toothpaste</td>
          <td>Supermarket</td>
          <td>13/09</td>
          <td>Good</td>
          <td>5</td>
        </tr>
      </tbody>
    </table>
  </body>
</html>
```

{{ EmbedLiveSample('Hidden_example', '100%', 300) }}

> [!NOTE]
> Этот пример можно также найти на GitHub по ссылке [spending-record-finished.html](https://github.com/mdn/learning-area/blob/master/html/tables/advanced/spending-record-finished.html) ([живой пример](https://mdn.github.io/learning-area/html/tables/advanced/spending-record-finished.html)).

## Вложенные таблицы

В одну таблицу вкладывать другую таблицу возможно, если вы используете полную структуру включая элемент `<table>`. Это как правило не рекомендуется, так как делает разметку более запутанной и менее доступной для пользователей скринридеров, так в большинстве случаев вы можете просто вставить дополнительные ячейки/строки/столбцы в существующую таблицу. Однако, иногда это необходимо, например, если вы хотите легко импортировать контент из других источников.

Разметка простой вложенной таблицы:

```html
<table id="table1">
  <tr>
    <th>title1</th>
    <th>title2</th>
    <th>title3</th>
  </tr>
  <tr>
    <td id="nested">
      <table id="table2">
        <tr>
          <td>cell1</td>
          <td>cell2</td>
          <td>cell3</td>
        </tr>
      </table>
    </td>
    <td>cell2</td>
    <td>cell3</td>
  </tr>
  <tr>
    <td>cell4</td>
    <td>cell5</td>
    <td>cell6</td>
  </tr>
</table>
```

## Таблицы для пользователей с ограниченными возможностями

Давайте кратко опишем как мы используем данные таблицы. Таблицы могут быть удобным инструментом, который даёт нам быстрый доступ к данным и позволяет искать разные значения. Например, быстрого взгляда на таблицу ниже достаточно, чтобы найти сколько колец было продано в Амстердаме в августе 2016. Чтобы понять эту информацию, мы проводим визуальные ассоциации между данными в этой таблице и её заголовками колонок и/или строк.

<table>
  <caption>
    Items Sold August 2016
  </caption>
  <tbody>
    <tr>
      <td></td>
      <td></td>
      <th colspan="3" scope="colgroup">Clothes</th>
      <th colspan="2" scope="colgroup">Accessories</th>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <th scope="col">Trousers</th>
      <th scope="col">Skirts</th>
      <th scope="col">Dresses</th>
      <th scope="col">Bracelets</th>
      <th scope="col">Rings</th>
    </tr>
    <tr>
      <th rowspan="3" scope="rowgroup">Belgium</th>
      <th scope="row">Antwerp</th>
      <td>56</td>
      <td>22</td>
      <td>43</td>
      <td>72</td>
      <td>23</td>
    </tr>
    <tr>
      <th scope="row">Gent</th>
      <td>46</td>
      <td>18</td>
      <td>50</td>
      <td>61</td>
      <td>15</td>
    </tr>
    <tr>
      <th scope="row">Brussels</th>
      <td>51</td>
      <td>27</td>
      <td>38</td>
      <td>69</td>
      <td>28</td>
    </tr>
    <tr>
      <th rowspan="2" scope="rowgroup">The Netherlands</th>
      <th scope="row">Amsterdam</th>
      <td>89</td>
      <td>34</td>
      <td>69</td>
      <td>85</td>
      <td>38</td>
    </tr>
    <tr>
      <th scope="row">Utrecht</th>
      <td>80</td>
      <td>12</td>
      <td>43</td>
      <td>36</td>
      <td>19</td>
    </tr>
  </tbody>
</table>

Но что если вы не можете провести эти визуальные ассоциации? Как тогда вы сможете прочитать таблицу выше? Люди с ослабленным зрением часто используют скринридер, который читает им информацию с веб-страницы. Это не проблема когда вы читаете простой текст, но интерпретация таблицы может быть сложной проблемой для слепых людей. Тем не менее, вместе с правильной разметкой мы можем заменить визуальные ассоциации программными.

В этой части статьи приводятся дополнительные способы которые делают таблицы более доступными.

### Использование заголовков столбцов и строк

Скринридеры будут определять все заголовки и использовать их создавая программные ассоциации между этими заголовками и ячейками к которым они относятся. Сочетание заголовков столбцов и строк будет определять и интерпретировать данные в каждой ячейке так, что пользователи скринридеров могут интерпретировать таблицу также как это делают зрячие пользователи.

Мы уже разобрали заголовки в предыдущей статье, смотри по ссылке [Добавление заголовков с помощью элемента \<th>](/ru/docs/Learn_web_development/Core/Structuring_content/HTML_table_basics#Adding_headers_with_%3Cth%3E_elements).

### Атрибут scope

Новая тема в этой статье это атрибут [`scope`](/ru/docs/Web/HTML/Element/th#scope), который может быть добавлен к элементу `<th>` он сообщает скринридеру какие ячейки точно являются заголовками — например, заголовок строки в которой он находится или столбца. Возвращаясь назад к нашему примеру с записями расходов, вы могли однозначно определить заголовки столбцов как здесь:

```html
<thead>
  <tr>
    <th scope="col">Purchase</th>
    <th scope="col">Location</th>
    <th scope="col">Date</th>
    <th scope="col">Evaluation</th>
    <th scope="col">Cost (€)</th>
  </tr>
</thead>
```

И у каждой строки может быть определён заголовок, как здесь (если мы добавили заголовки строк и заголовки столбцов):

```html
<tr>
  <th scope="row">Haircut</th>
  <td>Hairdresser</td>
  <td>12/09</td>
  <td>Great idea</td>
  <td>30</td>
</tr>
```

Скринридер распознает разметку структурированную таким образом, что позволяют пользователям прочитать весь столбец или строку целиком.

Атрибут `scope` имеет ещё два возможных значения — `colgroup` и `rowgroup`. Они используются для заголовков, которые располагаются вверху ваших столбцов или строк. Если вы посмотрите на таблицу "Items sold..." в начале этого раздела статьи, вы увидите что ячейка с "Clothes" находится над ячейками "Trousers", "Skirts" и "Dresses". Все эти ячейки должны быть помечены как заголовки (`<th>`), но "Clothes" заголовок который находится сверху и определяет остальные три подзаголовка. Поэтому "Clothes" должна получить атрибут `scope="colgroup"`, тогда как другие получат атрибут `scope="col"`.

### Атрибуты id и headers

Альтернатива атрибута `scope` это использование атрибутов [`id`](/ru/docs/Web/HTML/Reference/Global_attributes#id) и [`headers`](/ru/docs/Web/HTML/Reference/Elements/td#headers) задавая ассоциации между заголовками и ячейками. Этот способ выглядит следующим образом:

1. Вы устанавливаете уникальный `id` для каждого `<th>` элемента.
2. Вы устанавливаете атрибут `headers` для каждого `<td>` элемента. Каждый `headers` атрибут должен содержать список всех `id`, разделённый пробелами, ко всем `<th>` элементам которые действуют как заголовок для этой ячейки.

Это обеспечивает явное определение позиции для каждой ячейки вашей HTML таблицы, определяет заголовки столбцов и строк таблицы. Для того чтобы это работало реально хорошо таблице нужно определить и заголовки столбцов, и заголовки строк.

Вернёмся к нашему примеру с расчётом затрат, его можно переписать следующим образом:

```html
<thead>
  <tr>
    <th id="purchase">Purchase</th>
    <th id="location">Location</th>
    <th id="date">Date</th>
    <th id="evaluation">Evaluation</th>
    <th id="cost">Cost (€)</th>
  </tr>
</thead>
<tbody>
  <tr>
    <th id="haircut">Haircut</th>
    <td headers="location haircut">Hairdresser</td>
    <td headers="date haircut">12/09</td>
    <td headers="evaluation haircut">Great idea</td>
    <td headers="cost haircut">30</td>
  </tr>

  ...
</tbody>
```

> [!NOTE]
> Этот метод создания очень точного определения ассоциаций между заголовками и данными в ячейках, но использует **гораздо** больше разметки и оставляет обширное пространство для ошибок. Атрибута `scope` обычно достаточно для большинства таблиц.

### Упражнение: играем со scope и headers

1. Для заключительного упражнения мы, вначале создадим копию [items-sold.html](https://github.com/mdn/learning-area/blob/master/html/tables/advanced/items-sold.html) и [minimal-table.css](https://github.com/mdn/learning-area/blob/master/html/tables/advanced/minimal-table.css) в новой папке.
2. Теперь попробуем добавить соответствующий атрибут `scope`, который наиболее соответствует этой таблице.
3. И наконец попробуем сделать другую копию изначальных файлов, на этот раз делая таблицу более доступной используя атрибуты `id` и `headers`.

> [!NOTE]
> Вы можете проверить как работает последние примеры здесь [items-sold-scope.html](https://github.com/mdn/learning-area/blob/master/html/tables/advanced/items-sold-scope.html) ([живой пример](https://mdn.github.io/learning-area/html/tables/advanced/items-sold-scope.html)) и [items-sold-headers.html](https://github.com/mdn/learning-area/blob/master/html/tables/advanced/items-sold-headers.html) ([живой пример](https://mdn.github.io/learning-area/html/tables/advanced/items-sold-headers.html)).

## Заключение

Есть ещё некоторые вещи которые можно узнать о HTML таблицах, но мы действительно дали всё что нужно на настоящий момент. Дальше вы возможно захотите больше узнать о стилизации HTML таблиц, посмотрите статью ["Стилизация таблиц"](/ru/docs/Learn_web_development/Core/Styling_basics/Tables).

{{PreviousMenuNext("Learn/HTML/Tables/Basics", "Learn/HTML/Tables/Structuring_planet_data", "Learn/HTML/Tables")}}
