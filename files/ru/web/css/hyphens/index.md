---
title: hyphens
slug: Web/CSS/hyphens
---

{{CSSRef}}

[CSS](/ru/docs/Web/CSS) свойство **`hyphens`** указывает, как следует переносить слова через дефис, когда текст переносится на несколько строк. Оно может полностью запретить перенос, делать перенос в местах, заданных вручную или позволять браузеру автоматически расставлять переносы, где это необходимо.

{{InteractiveExample("CSS Demo: hyphens")}}

```css interactive-example-choice
hyphens: none;
```

```css interactive-example-choice
hyphens: manual;
```

```css interactive-example-choice
hyphens: auto;
```

```html interactive-example
<section id="default-example">
  <p id="example-element">An extra­ordinarily long English word!</p>
</section>
```

```css interactive-example
#example-element {
  border: 2px dashed #999;
  font-size: 1.5rem;
  text-align: left;
  width: 7rem;
}
```

Правила расстановки переносов зависят от языка. В HTML язык определяется атрибутом [`lang`](/ru/docs/Web/HTML/Reference/Global_attributes/lang), и браузеры применяют правила переноса только при присутствии данного атрибута и доступности соответствующего словаря для расстановки переносов. В XML необходимо использовать атрибут [`xml:lang`](/ru/docs/Web/SVG/Attribute/xml:lang).

> [!NOTE]
> Правила, определяющие, как выполняется расстановка переносов, явно не определены в спецификации, поэтому точная расстановка переносов может варьироваться от браузера к браузеру.

## Синтаксис

```css
/* Keyword values */
hyphens: none;
hyphens: manual;
hyphens: auto;

/* Global values */
hyphens: inherit;
hyphens: initial;
hyphens: unset;
```

Свойство `hyphens` задаётся как одно из ключевых значений, выбранного из списка ниже.

### Значения

- `none`
  - : Слова не разрываются при переносе строки, даже если внутри слов указаны точки разрыва. Строки будут переноситься только по пробелам.
- `manual`
  - : Слова разрываются при переносе строки только там, где символы внутри слов указывают точки разрыва. Подробнее смотреть ниже [Предлагаемые возможности разрыва строки](#предлагаемые_возможности_разрыва_строки).
- `auto`
  - : Браузер может автоматически разбивать слова в соответствующих точках переноса, следуя любым правилам, которые он выбирает. Однако предлагаемые возможности разрыва строки (смотреть [Предлагаемые возможности разрыва строки](#предлагаемые_возможности_разрыва_строки) ниже) переопределят автоматический выбор точки разрыва, если таковые имеются.

> [!NOTE]
> Поведение параметра `auto` зависит от того, на каком языке применяются правила переноса. Вы должны указать язык с помощью HTML атрибута `lang`, чтобы гарантировать, что на этом языке применяется автоматическая расстановка переносов.

## Предлагаемые возможности разрыва строки

Для указания потенциальных точек разрыва строки в тексте вручную используются два символа Unicode:

- U+2010 (HYPHEN)
  - : «Жёсткий» дефис указывает на возможность видимого разрыва строки. Даже если строка в этом месте не переносится, дефис всё равно отображается.
- U+00AD (SHY)
  - : Невидимый «мягкий» перенос. Этот символ не отображается визуально, вместо этого он отмечает место, где браузер должен разорвать слово, если расстановка переносов необходима. В HTML, используйте `&shy;` для вставки мягкого дефиса.

> [!NOTE]
> Когда HTML-элемент [`<wbr>`](/ru/docs/Web/HTML/Reference/Elements/wbr) приводит к разрыву строки, дефис не добавляется.

## Формальное определение

{{cssinfo}}

## Формальный синтаксис

{{csssyntax}}

## Примеры

### Указание переносов текста

В этом примере используются три класса, по одному для каждой возможной конфигурации свойства `hyphens`.

#### HTML

```html
<dl>
  <dt><code>none</code>: no hyphen; overflow if needed</dt>
  <dd lang="en" class="none">An extreme&shy;ly long English word</dd>
  <dt>
    <code>manual</code>: hyphen only at &amp;hyphen; or &amp;shy; (if needed)
  </dt>
  <dd lang="en" class="manual">An extreme&shy;ly long English word</dd>
  <dt><code>auto</code>: hyphens where the algorithm decides (if needed)</dt>
  <dd lang="en" class="auto">An extreme&shy;ly long English word</dd>
</dl>
```

#### CSS

```css
dd {
  width: 55px;
  border: 1px solid black;
}
dd.none {
  -webkit-hyphens: none;
  -ms-hyphens: none;
  hyphens: none;
}
dd.manual {
  -webkit-hyphens: manual;
  -ms-hyphens: manual;
  hyphens: manual;
}
dd.auto {
  -webkit-hyphens: auto;
  -ms-hyphens: auto;
  hyphens: auto;
}
```

#### Результат

{{EmbedLiveSample("Указание_переносов_текста", "100%", 490)}}

## Характеристики

{{Specifications}}

## Совместимость с браузерами

{{Compat}}

## Смотрите также

- {{Cssxref("content")}}
- {{cssxref("overflow-wrap")}} (formerly `word-wrap`)
- {{cssxref("word-break")}}
