# Техники центрирования на CSS

## 1. Центрирование текстового содержимого

### 1.1. Горизонтальное центрирование текста

- родитель должен иметь конкретную ширину

**Стили**
```css
.parent {
   text-align: center;
}
```

### [Демо: text-align.html](./src/text-align.html)

### 1.2. Центрирование внутренними отступами

- родитель не может иметь конкретную ширину и высоту, они высчитываются в зависимости от контента
- может иметь максимальную ширину, контент будет переноситься по строкам
- родитель должен быть строчным

**Стили**
```css
.parent {
   display: inline-block;
   max-width: 200px; /*optional*/
   padding: 10px 30px;
   text-align: center;
}
```

### [Демо: padding.html](./src/padding.html)

### 1.3. Вертикальное центрирование высотой строки

- ограничение на перенос строк, может быть только одна строка
- всегда нужно дублировать величину высоты элемента для высоты строки
- может комбинироваться с вариантами 1.1 и 1.2 для горизонтального центрирования

**Стили**
```css
.parent {
   height: 50px;
   line-height: 50px;
}
```

### [Демо: line-height.html](./src/line-height.html)

### 1.4. Вертикальное центрирование ячейкой таблицы

- нет ограничений по высоте и ширине; они могут быть как заданы, так и нет
- может комбинироваться с вариантами 1.1 и 1.2 для горизонтального центрирования
- вертикальный центр высчитывается автоматически
- ограничение: содержимое может быть только строчным
- если используется `box-sizing: border-box`, то присутствие `border` может повлиять на расчёт величины высоты строки

**Стили**
```css
.parent {
   display: table-cell;
   vertical-align: middle;
   height: 50px;
}
```

### [Демо: table-cell.html](./src/table-cell.html)

## 2. Горизонтальное центрирование колонки

- только горизонтальное центрирование
- только для блочных элементов с указанной шириной

**Стили**
```css
.centered {
   display: block;
   width: 800px;
   margin: auto;
}
```

### [Демо: block-margin-auto.html](./src/block-margin-auto.html)

## 2. Центрирование в строке

### 2.1. Горизонтальное центрирование в строке

- можно использовать на нескольких элементах расположенных рядом
- `text-align` наследуется дочерними элементами, поэтому надо его перекрывать

**Стили**
```css
.parent {
   text-align: center;
}
.centered {
   display: inline-block;
   text-align: center; /*custom internal centering*/
}
```

### [Демо: inline-center.html](./src/inline-center.html)

### 2.2. Вертикальное центрирование в строке c псевдо-элементом

- работает с одним и более элементами
- ограничение: не может быть переноса строк

**Стили**
```css
.parent {
   height: 100%; /*any*/
}
.parent::after {
   content: '';
   display: inline-block;
   vertical-align: middle;
   width: 1px;
   height: 100%;
}
.centered {
   display: inline-block;
   vertical-align: middle;
}
```

### [Демо: inline-pseudo.html](./src/inline-pseudo.html)

## 3. Абсолютное позиционирование и отрицательный `margin`

- заданы ширина и высота
- нужно высчитывать значения `margin` в зависимости от размеров
- работает как `position: absolute`, так и с `position: relative`

**Стили**
```css
.centered {
   position: absolute;
   width: 600px;
   height: 400px;
   top: 50%;
   left: 50%;
   margin-left: -300px; /*50% of width*/
   margin-top: -200px; /*50% of height*/
}
```

### [Демо: absolute-margin.html](./src/absolute-margin.html)

## 4. Абсолютное позиционирование и сдвиг с помощью `transofrm`

- не обязательно задавать ширину и высоту
- может размываться текст
- работает как `position: absolute`, так и с `position: relative`

**Стили**
```css
.centered {
   position: absolute;
   width: 600px;
   height: auto; /*optional*/
   top: 50%;
   left: 50%;
   transform: translate(-50%, -50%);
}
```

### [Демо: absolute-transform.html](./src/absolute-transform.html)

## 5. Абсолютное позиционирование по 4 сторонам

- заданы ширина и высота

**Стили**
```css
.centered {
   position: absolute;
   width: 600px;
   height: 300px;
   top: 0;
   bottom: 0;
   left: 0;
   right: 0;
   margin: auto;
}
```

### [Демо: absolute-4-sides.html](./src/absolute-4-sides.html)

## 6. Центрирование с помощью табличных стилей

- не обязательно задавать ширину и высоту
- нужно использовать дополнительную обёртку
- `text-align` наследуется дочерними элементами, поэтому надо его перекрывать

**Стили**
```css
.extra-parent {
  position: fixed;
  display: table;
  width: 100%;
  height: 100%;
}
.parent {
  display: table-cell;
  vertical-align: middle;
  text-align: center;
}
.centered {
  display: inline-block;
  text-align: left;  /*redefine*/
  width: 600px; /*optional*/
  height: auto; /*optional*/
}
```

### [Демо: table-layout.html](./src/table-layout.html)

## 7. Flexbox 

- не обязательно задавать ширину и высоту
- можно центрировать несколько элементов рядом
- элементы могут располагаться даже на нескольких строках и колонках
- трудно запоминаемый и не интуитивно понятный синтаксис (субъективно)
- работает только в новых браузерах (https://caniuse.com/#search=flex)

**Стили**
```css
.parent {
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: center;
  flex-direction: row;
  flex-wrap: wrap;
}
.centered {
   /*any*/
}
```

### [Демо: flexbox.html](./src/flexbox.html)

## 7. Grid 

- не обязательно задавать ширину и высоту
- можно центрировать несколько элементов рядом, но надо выбирать в каком направлении: по вертикали или горизонтали
- работает только в браузерах выпущенных позже середины 2017 года (https://caniuse.com/#search=grid)

**Стили**
```css
.parent {
  display: grid;
  justify-content: center;
  align-content: center;
  grid-auto-flow: column; /* 'column' - horizontal, 'row' - vertical*/
}
.centered {
   /*any*/
}
```

### [Демо: grid-layout.html](./src/grid-layout.html)

# Ссылки

- [http://howtocenterincss.com/](http://howtocenterincss.com/)
- [Вертикальное и горизонтальное выравнивание на CSS. Полное руководство.](https://www.youtube.com/watch?v=-q575iqz9r4)
- [Центрирование в CSS: полное руководство](http://vavik96.com/centrirovanie-v-css-polnoe-rukovodstvo/)