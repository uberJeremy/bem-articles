# JavaScript for BEM: The Main Terms
# JavaScript по БЭМ: основные понятия


There is a block [i-bem](http://bem.github.com/bem-bl/sets/common-desktop/i-bem/i-bem.ru.html) which lives in the `bem-bl` library.  The `bem-bl` library is included in what we call the `BEM Stack`.

##################################

[Choose this one - closer to Russian Version]
Its JavaScript implementation strictly adheres to a `BEM Naming Convention`. Using the `i-bem` block allows you to take advantage of all the benefits when development according to BEM-principles, and program not only look of a components, but also their behavior.

[or this one - Slightly "edited" version]
It's JavaScript implementation strictly adheres to, and in some ways defines, the `BEM Coding Style` and `BEM Conventions`.  The use of this library allows one to manipulate the client-side JavaScript/DOM in *BEM-Style* according to *BEM-Principles*, not only in the design of visible components, but also their behaviour.

#######################

В стеке БЭМ-технологий есть [блок i-bem](http://bem.github.com/bem-bl/sets/common-desktop/i-bem/i-bem.ru.html)
библиотеки `bem-bl`. Его JavaScript-реализация использует предметную область БЭМ
и позволяет насладиться всеми преимуществами разработки по принципам БЭМ не
только программируя внешний вид компонент, но и их поведение.


## Why Do We Need One More Framework?

Principally, all existent JavaScript libraries can be divided into the following categories:

 * Polyfills<br/>
   For example jQuery and base2 (a long time ago, at the dawn of stack frameworks, it was very popular).
 * Ready-made Widget Sets
 * Complicated Libraries
   which for now we'll call "Rich UI Interfaces".
 * "Monsters"<br/>
   Robust libraries for writing complex web-applications

## Зачем нужен ещё один фреймворк?
В принципе, все существующие JavaSript-библиотеки можно условно разделить между
собой на несколько кiатегорий:

 * отвечающие за нормализацию API браузеров<br/>
   Например, jQuery или base2 (когда-то очень давно, еще на заре формирования
   стеков фреймворков, она была очень популярной)i;
 * предоставляющие какие-то готовые наборы виджетов;
 * сложные библиотеки, которые для так называемых Rich UI интерфейсов;
 * «монстры»<br/>
 Полноценные библиотеки для написания сложных веб-приложений.

This categorization is not absolute, and probably many libraries answer problems which exist across several categories.  The important thing here is that each of these libraries have been designed with one similar goal; to help us solve our problems.
Разделение достаточно условное, и скорее всего многие библиотеки можно
одновременно отнести к нескольким категориям. Но важно одно: у них у всех одна
цель — помогать нам решать наши задачи.

OldSchool designers still remember the good'ol days when nothing like jQuery existed and they had to program everything from scratch.
Each project had its own `common.js` which included a set of commonly used functions.
At the beginning of it was a section which would be copy-&-pasted from project to project.  Later these functions might be collected into a small JavaScript library.

That was the evolution of JavaScript frameworks.

Разработчики старой школы ещё помнят времена, когда не было даже jQuery и все
приходилось делать самостоятельно. У каждого на проекте был свой `common.js`,
§который включал в себя набор вспомогательных функций. Всё это сначала
копипастили из проекта в проект, а потом их выносили в свою маленькую JavaScript
библиотеку.<br/>
Так, эволюционно появлялись JavaScript-фреймворки.

The same thing happened to BEM.  Initially, we understood that we wanted to have these things called `blocks` which were `Interface Modules`, their smaller CSS-elements and modifiers existed only in CSS.  Later developers wanted to work using a similar structure, but this time in JavaScript.  During this time developers also wanted to include the key-concept of `levels` which allows one to build upon and improve the behavior of blocks from project to project.

То же самое прозошло и в БЭМ. Сначала понятие блоков (интерфейсных модулей), их
элементов и модификаторов существовало только для CSS. Затем разработчики
захотели работать с такой же структорой в JavaScript, и вдобавок использовать 4е
ключевое понятие — `уровни переопределения` — чтобы дополнять и расширять
поведение блоков от проекта к проекту.<br/>

This is how the JavaScript was written for the *helper block* [i-bem.js](https://github.com/bem/bem-bl/tree/master/blocks-common/i-bem) which lives over at GitHub.  This is the core framework for writing JavaScript in `BEM Terminology`.
Таким образом, появилась JavaScript реализация блока-хелпера
[i-bem.js](https://github.com/bem/bem-bl/tree/master/blocks-common/i-bem),
который хранится на GitHub. Это и есть фреймворк (или блок-ядро) для того, чтобы
писать JavaScript в БЭМ-терминах.

## Connection With HTML Code
As all JavaScript components, code for `i-bem.js` has to be coupled with some HTML, eventually intended to be the functional code behind some part of an interface.  In order to use i-bem all you have to do is add the CSS-Class `i-bem`, and define the `onclick` attribute to contain the parameters of the block.

## Ассоциация с HTML-кодом
Как и любой JavaScript-компонент, код, написанный под `i-bem.js` должен быть
проассоциирован с HTML-фрагментом, который он намерен превратить в
функционирующую часть интерфейса. Здесь для этого достаточно добавить блоку
CSS-класс `i-bem` и указать в атрибуте onclick параметры блока.

```js
<div
    class="myblock i-bem"
    onclick="return {
        myblock: { }}">

    <span class="myblock__item"></span>

</div>
```

If you are curious about why `onclick` attribute is used, see Sergey Berezhnoy's talk (Russian only) "[Different ways of creating components for the client-side](http://events.yandex-team.ru/events/yasubbotnik/msk-jul-2012/talks/302/)" - presented at [Ya.Subbotnik (Yandex Developer Day)](http://events.yandex-team.ru/events/yasubbotnik/) in July 2012.
О том, почему `onclick`, можно узнать из доклада Сергея Бережного «[Разные
способы создания клиентских
компонентов](http://events.yandex-team.ru/events/yasubbotnik/msk-jul-2012/talks/302/)»,
прозвучавшего на
[Я.Субботнике](http://events.yandex-team.ru/events/yasubbotnik/) в июле 2012.

Usually, the blocks initialization starts on `domReady` event.  Thanks to the ability to read the `onclick` attribute and receive a native javascript object we don't need access to any `id` components or to wait for the parsing of CSS classes.  All blocks that have the class attribute `i-bem` will be transformed according to their parameter's components.

Инициализация блоков на странице в общем случае запускается по `domReady`.
Благодаря возможности считать параметры из onclick и получить нативный
JavaScript-объект не нужны `id` компонент или парсинг CSS-классов: все блоки,
помеченные классом `i-bem` превратятся в соответствующие их параметрам
компоненты.

## Behavior Declaration
A block's behavior is described in a JavaScript file which has the same name as the block it's self (`myblock.js`).

From an OOP point of view, similar blocks form classes.  Furthermore, for every block on the page a instance of each corresponding "class" is generated.

The `decl` method is used for describing the block's behaviour, it receives 3 parameters:
 1. The `name` of the block we're talking about.
 2. This specific block's properties.
 3. The static properties of the class to which the block belongs.

```js
BEM.DOM.decl('myblock', {

    /\* Properties specific to this instance \*/

}, {

    /\* Static properties specific to the class to which this block belongs \*/

});
```

## Декларация поведения
В JavaScript-файле блока (`myblock.js`) описывается его поведение.

С точки зрения объектной модели все блоки одинаковые блоки образуют класс. При
этом каждое появление блока на странице рождает экземпляр этого класса.

Для описания поведения используется метод `decl`, принимающий 3 параметра:

 1. Блок, о котором пойдёт речь
 2. Собственные свойства экземпляра блока
 3. Статические свойства класса, к которому принадлежит блок

```js
BEM.DOM.decl('myblock', {

    /\* собственные свойства экземпляра \*/

}, {

    /\* статические свойства \*/

});
```

Inside JavaScript, the reference to the instance you can always get with help of keyword `this` and use its reserved fields `__self` and  `__base`. 

 * `this.__self`<br/>
 Refers to the class static methods (to which the instance belongs)
 * `this.__base`<br/>
  Perform a `super call`, which means to call the base method implementation.

Внутри JavaScript ссылку на экзепляр всегда можно получить по ключевому слову
`this` и использовать его зарезервированные поля `__self` и `__base`.

 * `this.__self`<br/>
 Ссылается на статические методы класса, к которому принадлежит экземляр
 * `this.__base`<br/>
Делает super call, то есть вызвает базовую реализацию метода.

The last one allows us to operate within different `levels`.
When extending functionality of an existing block, a developer always has access to the block's behaviour as defined on the previous level.
In other words, methods can be fully overwritten or they can be extended with additional behavior.  

Последнее позволяет использовать уровни переопределения. При расширении
функциональность уже существующего блока, разработчик всегда имеет доступ к
поведению, определённому предыдущим уровнем. То есть методы можно не только
полностью перезаписывать, но и «обрамлять» дополнительным поведением.

```js
BEM.DOM.decl('myblock', {

    method: function() {

        this.__base();
        this.doMore();

    }

});```

Other than inheritance by definition levels, a block has the possibility to inherit one from another block.  Because of the possibility of inheritance from one level to another, it's better to understand this of the merging of implementations.
Кроме наследования по уровням переопределения, есть ещё возможность явно
отнаследовать один блок от другого. Поэтому возможность "наследования" от уровня
к уровню лучше воспринимать как мёрдж реализаций.

## A Block's Selectors
To find other blocks it is possible to use of the `find*` methods, it depends on where the desirable block is located relative to the current block:

```js
// Search within the current block's context.
this.findBlockInside([elem], block)

// Search outside of the current block's context.
this.findBlockOutside([elem], block)

// Search DOM-node of the named block.
this.findBlockOn([elem], block)
```

## Селекторы блоков
Для поиска других блоков можно воспользоваться одним из `find*` методов, в
зависимости от того, где находится желаемый блок относительно текущего:

```js
// поиск внутри контекста
this.findBlockInside([elem], block)

// поиск снаружи контекста
this.findBlockOutside([elem], block)

// поиск на DOM-узле текущего блока
this.findBlockOn([elem], block)
```

Each of these methods return a JavaScript object, an instance of the block which was located by the search method.
Все эти методы возращают JavaScript-объект, экземпляр найденного блока.

In a similar way a collection of blocks can be found:

```js
// Search inside the current block's context.
this.findBlocksInside([elem], block)

// Search outside of the current block's context.
this.findBlocksOutside([elem], block)

// Search DOM-node of the named block
this.findBlocksOn([elem], block)
```

**Note: The only difference from the previously mentioned methods is the plural form of the word "block" in the methods' names **
Похожим образом можно найти и коллекции блоков:

```js
// поиск внутри контекста
this.findBlocksInside([elem], block)

// поиск снаружи контекста
this.findBlocksOutside([elem], block)

// поиск на BEM-узле текущего блока
this.findBlocksOn([elem], block)
```

## Elements
There are methods for accessing a block's `elements`: `elem` and `findElem`.
The difference between them is that the `elem` method cashes elements before it's initial call, therefore there is no need to store a result of `elem` method in a variable.  It's already implemented for this method.

```js
//cashing selector
this.elem(name,
    [modName], [modVal])

//non-cashing selector
this.findElem([ctx], name, 
    [modName], [modVal])
```
## Элементы
Аналогично, есть методы для доступа к элементам блока: `elem` и `findElem`.
Отличие в том, что метод `elem` кеширует свой результат при первом обращении. То
есть можно не сохранять вызов в переменную, чтобы сэкономить на поиске — всё уже
сделано в реализации этого метода.

```js
//кеширующий селектор
this.elem(name,
    [modName], [modVal])

//некеширующий
this.findElem([ctx], name, 
    [modName], [modVal])
```

## Modifiers
Modifiers in JavaScript exist for expressing the state of a block or element.

The methods for working with modifiers are the same for blocks and for elements.

The first parameter is optional, and may serve for illustration purposes.

```js
// Get the value of the block's modifier
this.getMod(modName)

// Get the value of the the element's modifier
this.getMod(elem, modName)

// Verify modifiers
this.hasMod([elem], modName, modVal)

// Set modifiers
this.setMod([elem], modName, modVal)

// Delete modifiers
this.delMod([elem], modName)

// Toggle a modifier's value
this.toggleMod([elem], modName, 
    modVal1, modVal2, [condition])
```

## Модификаторы
Модификаторы в JavaScript служат для выражения состояния блока или элемента.

Методы работы с модификаторами одинаковы и для блоков, и для элементов. Но
первый — опциональный — параметр показывает, о чём идёт речь.

```js
// значение модификато раблока
this.getMod(modName)

// значение модификатора элемента
this.getMod(elem, modName)

// проверка модификатора
this.hasMod([elem], modName, modVal)

// установка модификатора
this.setMod([elem], modName, modVal)

// удаление модификатора
this.delMod([elem], modName)

// переключение значений модификатора
this.toggleMod([elem], modName, 
    modVal1, modVal2, [condition])
```

Modifiers describe a block's state.  Every block has an event `onSetMod` which allows us to define the behaviour of a block's instance.  This event is fired when a modifier is being applied to the block.

```js
BEM.DOM.decl('myblock', {
    onSetMod : {
        'mod1' : {

            // Set the value of `mod1` to `val1`
            'val1' : function(mod, val, oldVal) {
            }

        },
			
        // Set the value of the modifier `mod2` to any value
        'mod2' : function(mod, val, oldVal) {
        }
    }
});
```

Сами модификаторы описываются как состояние блока. То есть, экземпляр блока
знает о том, как ему нужно среагировать на установку модификатора.<br/>
Для такого описания используется поле `onSetMod` из собственных свойств блока.

```js
BEM.DOM.decl('myblock', {
    onSetMod : {
        'mod1' : {

            // установка модификатора mod1 в val1
            'val1' : function(mod, val, oldVal) {
            }

        },
			
        // установка модификатора`mod2` в любое значение
        'mod2' : function(mod, val, oldVal) {
        }
    }
});
```

We declare modifiers for elements in a similar way:

```js
BEM.DOM.decl('myblock', {
    // …

    onElemSetMod : {

        // The same structure as the block
        'elem' : {
            'mod1' : {

                // the additional parameter `elem`
                'val1' : function(elem, mod, val, oldVal) {
                }

            }
        }
    }

});
```

Похожая декларация есть и для модификаторов элементов:

```js
BEM.DOM.decl('myblock', {
    // …

    onElemSetMod : {

        // структура, аналогичная блоку
        'elem' : {
            'mod1' : {

                // дополнительный параметр`elem` 
                'val1' : function(elem, mod, val, oldVal) {
                }

            }
        }
    }

});
```

## Events
Events play a key-role in JavaScript.  There are special methods which allow us to work with events on the DOM-level with existing blocks, and with events for BEM-objects (JavaScript objects that are the block's instances).

```js
// DOM-event
this
    .bindTo([elem], event, fn)
    .unbindFrom([elem], event)

// BEM-event
this
    .on(event, [data], fn, [ctx])
    .un(event, [data], fn, [ctx])
    .trigger(event, [data])
```

## События
События играют ключевую роль в JavaScript. Поэтому и при реализации блока
`i-bem` их не обошли вниманием. Специальные методы позволяют работать с
событиями как на DOM-узлах, соответствуюших блокам, так и на BEM-объектах
(JavaScript-объектах, представляющих экземляры блоков).

```js
// DOM-события
this
    .bindTo([elem], event, fn)
    .unbindFrom([elem], event)

// BEM-события
this
    .on(event, [data], fn, [ctx])
    .un(event, [data], fn, [ctx])
    .trigger(event, [data])
```

A DOM-event doesn't need any explanations, it the result of a user's action: click, key press, scroll, etc.

BEM-events are like "custom events", they exist for the possibility to create an API for blocks.

DOM-события не нуждаются в пояснении — это то, что происходит в результате
действий пользователя: клик мышкой, работа с клавиатурой, прокрутка и т.д.

BEM-события — это кастомные события, нужные для возможности организовать API
блоков.


## Initialization
The block starts to work after it is initialised.  The moment a block is initialised, it receives the `js_inited` modifier.

## Инициализация
Работа блока начинается с его инициализации. В этот момент у блока появляется
модификатор `js_inited`.

Similar to other methods, code can be assigned to the `inited` property which will be executed when this modifier is initialised.
In other words, it's possible to write a "constructor".


```js
onSetMod : {

    'js' : {

        'inited' : function(){

            // The block's "constructor"

        }
    }
}
```


Аналогично других модификаторам, на его установку можно реагировать исполнением
задекларированного кода. То есть, есть возможность написать "конструктор".

```js
onSetMod : {

    'js' : {

        'inited' : function(){

            // "конструктор" блока

        }
    }
}
```

Also `i-bem` makes possible a lazy initialization for the other blocks.
I allows us to create blocs without DOM-representation, use an idea of events delegation, etc. <br/>
More information can be found at [the `i-bem` block's page ](http://bem.github.io/bem-bl/sets/common-desktop/i-bem/i-bem.en.html).

Кроме описанного блок `i-bem` предоставляет для других блоков возможности
отложенной (ленивой) инициализации, позволяет писать блоки без
DOM-представления, использует идею делигирования событий и многое другое.<br/>
Об этом можно прочесть на [странице блока
i-bem](http://bem.github.com/bem-bl/sets/common-desktop/i-bem/i-bem.ru.html).

<!--(Begin) Article author block-->
<div class="article-author">
    <div class="article-author__photo">
        <img class="article-author__pictures" src="http://img-fotki.yandex.ru/get/5625/51437929.0/0_bf4ad_363d4605_S.png" alt="Varvara Stepanova">
    </div>
    <div class="article-author__info">
        <div class="article-author__row">
             <span class="article-author__name">Varvara Stepanova,
        </div>
        <div class="article-author__row">
            works in Yandex since 2008 as a leading interface developer, Team Leader of Yandex Frontend Development Group, which implemented following the BEM-methodology.

            In her free time she likes to travel. Her dream is to visit all countries in the world.
            Работает в Яндексе с 2008 года ведущим разработчиком интерфейсов. Руководит группой разработки frontend фреймворка Яндекса, реализованного по методологии БЭМ. Распространяет информацию о БЭМ как в России, так и за рубежом. В свободное от написания кода время любит путешествовать и мечтает побывать во всех странах мира.
        </div>
        <div class="article-author__row">
             <a class="article-author__social-icon b-link" target="_blank" href="http://twitter.com/toivonens">twitter.com/toivonens</a>
        </div>
        <div class="article-author__row">
             <a class="article-author__social-icon b-link" target="_blank" href="http://github.com/toivonen">github.com/toivonen</a>
        </div>
    </div>
</div>
<!--(End) Article author block-->

This article is based on [Vladimir Varankin's](https://github.com/narqo) talk "[BEM and JavaScript: Why Did We Created a JS-framework?]" that was presented at Ya.Subbotnik (Yandex Developer's Day) in Moscow September 8, 2012.

Статья подготовлена по материалам выступления [Владимира Варанкина](https://github.com/narqo) «[БЭМ и JavaScript: Зачем мы написали JS-фреймворк?](http://events.yandex.ru/events/yasubbotnik/msk-sep-2012/talks/323/)» на Я.Субботнике в Москве 8 сентября 2012.
