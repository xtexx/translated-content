---
title: border-inline-end-width
slug: Web/CSS/border-inline-end-width
---

[CSS](/zh-CN/docs/Web/CSS) 属性 **`border-inline-end-width`** 定义了元素的逻辑行末的边框宽度，并根据元素的书写模式、行内方向和文本朝向对应至实体边框宽度。根据 {{CSSXref("writing-mode")}}、{{CSSXref("direction")}} 和 {{CSSXref("text-orientation")}} 所定义的值，此属性对应于 {{CSSXref("border-top-width")}}、{{CSSXref("border-right-width")}}、{{CSSXref("border-bottom-width")}} 或 {{CSSXref("border-left-width")}} 属性。

{{InteractiveExample("CSS Demo: border-inline-end-width")}}

```css interactive-example-choice
border-inline-end-width: thick;
writing-mode: horizontal-tb;
```

```css interactive-example-choice
border-inline-end-width: thick;
writing-mode: vertical-rl;
```

```css interactive-example-choice
border-inline-end-width: 4px;
writing-mode: horizontal-tb;
direction: rtl;
```

```html interactive-example
<section class="default-example" id="default-example">
  <div class="transition-all" id="example-element">
    This is a box with a border around it.
  </div>
</section>
```

```css interactive-example
#example-element {
  background-color: palegreen;
  color: #000;
  border: 0 solid crimson;
  padding: 0.75em;
  width: 80%;
  height: 100px;
  unicode-bidi: bidi-override;
}
```

## 语法

```css
/* 边框宽度值 */
border-inline-end-width: 2px;
border-inline-end-width: thick;

/* 全局值 */
border-inline-end-width: inherit;
border-inline-end-width: initial;
border-inline-end-width: revert;
border-inline-end-width: revert-layer;
border-inline-end-width: unset;
```

与此相关的属性有 {{CSSXref("border-block-start-width")}}、{{CSSXref("border-block-end-width")}} 和 {{CSSXref("border-inline-start-width")}}，这些属性定义了元素其他边框的宽度。

### 取值

- `<'border-width'>`
  - : 边框宽度。见 {{CSSXref("border-width")}}。

## 形式定义

{{CSSInfo}}

## 形式语法

{{CSSSyntax}}

## 示例

### 为竖排文本应用边框

#### HTML

```html
<div>
  <p class="exampleText">示例文本</p>
</div>
```

#### CSS

```css
div {
  background-color: yellow;
  width: 120px;
  height: 120px;
}

.exampleText {
  writing-mode: vertical-lr;
  border: 1px solid blue;
  border-inline-end-width: 5px;
}
```

#### 结果

{{EmbedLiveSample("为竖排文本应用边框", 140, 140)}}

## 规范

{{Specifications}}

## 浏览器兼容性

{{Compat}}

## 参见

- [CSS 逻辑属性与逻辑值](/zh-CN/docs/Web/CSS/CSS_logical_properties_and_values)
- 此属性对应的实体边框属性：{{CSSXref("border-top-width")}}、{{CSSXref("border-right-width")}}、{{CSSXref("border-bottom-width")}} 和 {{CSSXref("border-left-width")}}
- {{CSSXref("writing-mode")}}、{{CSSXref("direction")}}、{{CSSXref("text-orientation")}}
