# Общие CSS замечания, советы и рекомендации

## CSS файлы

В начале каждого CSS файла создаётся и поддерживается список содержимого в, указывающий на разделы файла стилей. Название разделов имеет префикс из `$`, что означает поиск `$[раздел]` выдаст только блок относящийся к секции.

### Синтакс и форматирование

Мы используем многострочную запись для улучшения последующей работы с системой контроля версий (выявление различий в сделанных в одной строке это тихий ужас) и мы упорядочиваем логические войства и селекторы по логическим группам, а **не** по алфавиту.

Мы пишем их селекторы в нижнем регистре и разделяем слова дефисом: `.thisIsBad{}`, `.this_is_also_bad{}` but `.this-is-correct{}`.

Всегда пишите последнюю точку с запятой в последнем правиле для селектора, чтобы избежать возможных конфликтов и синтаксических ошибок во время всего использования документа.

Для примера предпочитаемого форматирования и структуры CSS файла просто посмотрите файл [github.com/csswizardry/vanilla/&hellip;/style.css](http://github.com/csswizardry/vanilla/blob/master/css/style.css)

**К прочтению:**

* [coding.smashingmagazine.com/&hellip;/writing-css-for-others](http://coding.smashingmagazine.com/2011/08/26/writing-css-for-others)
* [jasoncale.com/&hellip;/5-dont-format-your-css-onto-one-line](http://jasoncale.com/articles/5-dont-format-your-css-onto-one-line)


## Комментарии

Комментируйте так много и так часто, насколько вы вообще можете это делать. Если это может понадобиться, то включите в комментарий блок кода разметки, помогающий понять в каком контексте находятся стили.

Будьте многословны, не стесняйтесь: CSS будет уменьшен при выкладывании на рабочий сервер.


## Отступы

Для каждого уровня вложенности разметки, пытайтесь делать соотвественные отступы в стилях. Например: 

    .nav{}
        .nav li{}
            .nav a{}
            
    .promo{}
        .promo p{}

Также же пишите вендорные префиксы, так чтобы значения были в одном столбике, то есть:

    -webkit-border-radius: 4px;
       -moz-border-radius: 4px;
            border-radius: 4px;

Это позволяет нам сразу увидеть, что все свойства установлены в 4px, но что более важно — так это то, что если наш редактор поддерживает режим редактирования столбцов, то мы можем менять значение сразу во всей колонке значений в один момент.

## Создание компонента

При создании нового компонента пишите разметку **до того**, как напишите хоть одну строчку CSS. Это позволяет увидеть какие свойства наследовались и избежать повторного применения избыточных стилей.

## OOCSS

При создании компонента старайтесь не повторять себя также не упускайте из виду принципы OOCSS.

Вместо того, чтобы плодить множество уникальных компонентов, попытайтесь распознать повторяющиеся шаблоны дизайна и создать из них абстракции; Сверстайте эти абстракции, а затем используйте уточняющие классы для расширения их внешнего оформления.

Если вы вынуждены создать новый компонент, то разделите его на структура и декоративное оформление; сверстайте структуру используя общие классы, тем самым давая возможность использования структуры компонента в других местах вашего проекта и затем используя более специфичные классы оформите компонент в соответствии с требованиями дизайна.

**К прочтению:**

* [csswizardry.com/&hellip;/the-nav-abstraction](http://csswizardry.com/2011/09/the-nav-abstraction)
* [stubbornella.org/&hellip;/the-media-object-saves-hundreds-of-lines-of-code](http://stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code)


## Раскладка

Все компоненты должны быть полностью независимы от ширины; ваши компоненты должны оставаться резиновыми(fluid) и их ширина должна контролироваться сеточной системой (grid system)

Высота **никогда** не должна назначаться элементам. Высота применяется только на сущности, имевшие размеры *до того*, как попали на сайт (например, картинки и спрайты). Никогда не устанавливайте высоту на `p`, `ul`, `div`, что угодно. Вы можете добить желаемого эффекта с помощью гораздо более гибкого `line-height`.

(Grid systems should be thought of as shelves.) Они содержат контент, но не являются им самим. (You put up your shelves then fill them with your stuff.)

Вы никогда не должны применять никаких стилей на ячейку сетки, так как они служат только целям разметки. (Never, under any circumstances, apply box-model properties to a grid item.)

## Sizing

We use a combination of methods for sizing UIs. Percentages, pixels, ems, rems and nothing at all.

**Read:**

* [csswizardry.com/&hellip;/measuring-and-sizing-uis-2011-style](http://csswizardry.com/2011/12/measuring-and-sizing-uis-2011-style)


## Font sizing

We use rems (with a pixel fallback for older browsers only). We do not want to define any font sizes in pixels as standard. We define line heights unitlessly everywhere **unless** we are trying to align text to known heights.

We want to avoid defining font sizes over and over; to achieve this we have a predefined scale of font sizes tethered to classes. We can recycle these rather than having to declare styles over and over.

Before writing another font-size declaration, see if a class for it already exists.

**Read:**

* [csswizardry.com/&hellip;/pragmatic-practical-font-sizing-in-css](http://csswizardry.com/2012/02/pragmatic-practical-font-sizing-in-css)


## Shorthand

It might be tempting to use declarations like `background:red;` but in doing so what we are actually saying is ‘I want no image to scroll, aligned top left and repeating X and Y and a background colour of red’. Nine times out of ten this won’t cause any issues but that one time it does is annoying enough to warrant not using such shorthand. Instead use `background-color:red;`.

Similarly, declarations like `margin:0;` are nice and short, but **be explicit**. If you’re actually only really wanting to affect the margin on the bottom of an element then it is more appropriate to use `margin-bottom:0;`.

Be explicit in which properties you set and take care to not inadvertently unset others with shorthand. E.g. if you only want to remove the bottom margin on an element then there is no sense in blitzing all margins with `margin:0;`.

Shorthand is good, but easily misused.


## Selectors

Keep selectors efficient and portable.

Heavily location-based selectors are bad for a number of reasons. For example, take `.sidebar h3 span{}`. This selector is too location-based and thus we cannot move that `span` outside of a `h3` outside of `.sidebar` and maintain styling.

Selectors which are too long also introduce performance issues; the more checks in a selector (e.g. `.sidebar h3 span` has three checks, `.content ul p a` has four), the more work the browser has to do.

Make sure styles aren’t dependent on location where possible, and make sure selectors are nice and short.

**Remember:** classes are neither semantic or insemantic; they are sensible or insensible! Stop stressing about ‘semantic’ class names and pick something sensible and futureproof.

**Read:**

* [speakerdeck.com/&hellip;/breaking-good-habits](http://speakerdeck.com/u/csswizardry/p/breaking-good-habits)
* [csswizardry.com/&hellip;/writing-efficient-css-selectors](http://csswizardry.com/2011/09/writing-efficient-css-selectors)

### Over-qualified selectors

An over-qualified selector is one like `div.promo`. We could probably get the same effect from just using `.promo`. Of course sometimes we will _want_ to qualify a class with an element (e.g. if you have a generic `.error` class that needs to look different when applied to different elements (e.g. `.error{ color:red; }` `div.error{ padding:14px; }`)), but generally avoid it where possible.

Another example of an over-qualified selector might be `ul.nav li a{}`. As above, we can instantly drop the `ul` and because we know `.nav` is a list, we therefore know that any `a` _must_ be in an `li`, so we can get `ul.nav li a{}` down to just `.nav a{}`.

### Performance

Whilst it is true that browsers will only ever keep getting faster at rendering CSS, efficiency is something we could do to keep an eye on. Short selectors, not using the universal (`*{}`) selector and avoiding more complex CSS3 selectors should help circumvent these problems.

**Read:**

* [csswizardry.com/…/writing-efficient-css-selectors](http://csswizardry.com/2011/09/writing-efficient-css-selectors)


## Be explicit, don’t make assumptions

Instead of using selectors to drill down the DOM to an element, it is often best to put a class on the element you explicitly want to style. Let’s take a specific example.

Imagine you have a promotional banner with a class of `.promo` and in there there is some text and call-to-action link. If there is just one `a` in the whole of `.promo` then it may be tempting to style that call-to-action via `.promo a{}`.

The problem here should be obvious in that as soon as you add a simple text link (or any other link for that matter) to the `.promo` container it will inherit the call-to-action styling, whether you want it to or not. In this case you would be best to explicitly add a class (e.g. `.cta`) to the link you want to affect.

Be explicit; target the element you want to affect, not its parent. Never assume that markup won’t change.

### Key selectors should (typically) never be a type selector or an object/abstraction class

You should never find yourself writing selectors whose key selector is a type selector (e.g. `.header ul{}`) or a base object (e.g. `.header .nav{}`). This is because you can never guarantee that there will only ever be one `ul` or `.nav` in that `.header`, the key selector is too loose—too broad.

It would be more appropriate to give the element in question an explicit class targeting that one and that one only, so `.header .nav{}` would be replaced with `.site-nav`, for example.

The only time where a type selector may be appropriate is if you have a situation like this:

    a{
        color:red;
    }
    .promo{
        background-color:red; 
        color:white;
    }
        .promo a{
            color:white;
        }

In this case you _know_ that every `a` in `.promo` needs a blanket rule because it would be unreadable without.

**Write selectors that target what you want, not what happens to be there already.**


## IDs and classes

Do not use IDs in CSS **at all**. They can be used in your markup for JS and fragment-identifiers but use only classes for styling. We don’t want to see a single ID in this (or any other) stylesheet.

Classes come with the benefit of being reusable (even if we don’t want to, we can) and they have a nice, low specificity.

**Read:**

* [csswizardry.com/&hellip;/when-using-ids-can-be-a-pain-in-the-class](http://csswizardry.com/2011/09/when-using-ids-can-be-a-pain-in-the-class)


## `!important`

It is okay to use `!important` on helper classes only. To add `!important` preemptively is fine, e.g. `.error{ color:red!important }`, as you know you will **always** want this rule to take precedence.

Using `!important` reactively, e.g. to get yourself out of nasty specificity situations, is not advised. Rework your CSS and try to combat these issues by refactoring your selectors. Keeping your selectors short and avoiding IDs will help out here massively.


## Magic numbers and absolutes

A magic number is a number which is used because ‘it just works’. These are bad because they rarely work for any real reason and are not usually very futureproof or flexible/forgiving. They tend to fix symptoms and not problems.

For example, using `.dropdown-nav li:hover ul{ top:37px; }` to move a dropdown to the bottom of the nav on hover is bad, as 37px is a magic number. 37px only works here because in this particular scenario the `.dropdown-nav` happens to be 37px tall.

Instead we should use `.dropdown-nav li:hover ul{ top:100%; }` which means no matter how tall the `.dropdown-nav` gets, the dropdown will always sit 100% from the top.

Every time you hard code a number think twice; if you can avoid it by using keywords or ‘aliases’ (i.e. `top:100%` to mean ‘all the way from the top’) or&mdash;even better&mdash;no measurements at all then you probably should.

Every hard-coded measurement you set is a commitment you might not necessarily want to keep.


## Conditional stylesheets

IE stylesheets can, by and large, be totally avoided. The only time an IE stylesheet may be required is to circumvent blatant lack of support (e.g. PNG fixes).

As a general rule, all layout and box-model rules can and _will_ work without an IE stylesheet if you refactor and rework your CSS. This means we never want to see `<!--[if IE 7]> element{ margin-left:-9px; } < ![endif]-->` or other such CSS that is clearly using arbitrary styling to just ‘make stuff work’.


## Debugging

If you run into a CSS problem **take code away before you start adding more** in a bid to fix it. The problem exists in CSS that is already written, more CSS isn’t the right answer!

Delete chunks of markup and CSS until your problem goes away, then you can determine which part of the code the problem lies in.

It can be tempting to put an `overflow:hidden;` on something to hide the effects of a layout quirk, but overflow was probably never the problem; **fix the problem, not its symptoms.**


## Preprocessors

By following the above advice you should typically find the need for a preprocessor decreases dramatically. If you still wish to use a preprocessor then by all means do so, but only as en extension of the above, not an alternative.

For example, preprocessors’ nesting abilities often lead to overly specific and location dependent selectors. Let’s use our `. nav a{}` example again:

    .nav{
        li{
            a{}
        }
    }

Will compile to:


    .nav {}
    .nav li {}
    .nav li a {}

Whilst this is a very timid example, it does help illustrate how a lot of preprocessors’ built in ‘helpful’ aspects actually go against our ideals; `.nav li a{}` could (and should) just be `.nav a{}`.

Also, with mixins and the like, preprocessors teach you how to recognise abstractions&mdash;which is great&mdash;but not necessarily how to use them properly; there’s no point writing an abstracted mixin when you proceed to repeat it a dozen times in a stylesheet.

Be sure to know the ins-and-outs of excellent vanilla CSS and where a preprocessor can _aid_ that, not hinder or undo it. Learn the downsides of preprocessors inside-out and then fuse the best aspects of the two with the bad bits of neither.