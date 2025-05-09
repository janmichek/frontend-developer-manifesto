# Frontend Developer Manifesto
The set of evergreen rules, best practices, commonly mistaken concepts and personal preferences in structured form

## Key Concepts
**Optimizing code for readability** - we spend much more time looking at the code. Better write more of encapsulated code than less lines of code on one place.

**Aha Programming** - use abstraction when its super-obvious. Till that moment its fine to duplicate. https://kentcdodds.com/blog/aha-programming/

**Components** - are reusable, isolated UI elements

**Clean Code** - evergreen universal programming hints, its mostly good to use them https://cleancoders.com/  -> accommodated for JS https://github.com/ryanmcdermott/clean-code-javascript/

**Desktop First** - Unless the requirements asks the opposite.

Things that cannot be automated are written here. If you go around some unaligned code, feel free to refactor little bit. It's always nice to do a bit of code cleanup


## Styles

We are using:
- Postcss https://postcss.org/
- Flexbox https://css-tricks.com/snippets/css/a-guide-to-flexbox/
- BEM https://en.bem.info/methodology/
- ITCSS https://frontend.garden/proc-je-itcss-nejpokrocilejsi-metodika-organizace-css/



### Every styled element needs to be classnamed

In BEM every styled element needs to be named. Also has the advantage when considering specificity.

**❌ Bad:**

```css
video {
   width: 100%
}

```

**✔️ Good:**

```css
.preview-file__video {
   width: 100%
}

```

### Use semantic naming

Classname should express what element is, not what it looks like.

**❌ Bad:**

```css
.element--yellow {
   color: yellow;
}

```

**✔️ Good:**

```css
.element--warning {
   color: yellow;
}

```



### No Dependant Selectors

This is actually BEM antipattern. Creating this dependency is the nastiest part of CSS causing unwanted results. Come up
with better BEM naming or componentize one level more. 



**❌ Bad:**

```css
.button .icon {
   color: red
}

```

**✔️ Good:**

```css
.button__icon {
   color: red
}

```

### Do not reflect structure nesting in naming

The `element` part of the naming should be as flat as possible. Avoid unnecessary dependent naming

**❌ Bad:**

```html
<ul :class="user__list">
    <li :class="user__list-item">
        <a class="user__list-item-link"/>
    </li>
</ul>
```

**✔️ Good:**

```html

<ul :class="user__list">
    <li :class="user__item">
        <a class="user__link"/>
    </li>
</ul>

```


### Use sizing naming

For sizing we use bootstrap style sizing https://getbootstrap.com/docs/4.1/layout/grid/

`[xs] [sm] [md] [lg] [xl]`

If sizing run out of scale of 5 levels - use just numbers `-1`, `-2`, ...

**❌ Bad:**

```html
<button class="button button--huge"/>
```

**✔️ Good:**

```html
<button class="button button--xl"/
```


### No names shortening

If there is no technical limitation - use full names to avoid mental mapping.
Exception could be widely domain-known shorthand(such as: tx)

**❌ Bad:**

```html
<button class="btn btn-dbu"/>
```

**✔️ Good:**

```html

<button class="button button--disabled"/>

```

### Naming scope

You can come up with naming from UI or product perspective for the same element. The preferred is UI perspective as long as it makes sense in context (of component)


**✔️ Good (preferred):**

```html
<input class="user-form__input"/>
```

**✔️ Good:**

```html

<input class="user-form__first-name"/>

```

### Prioritize properties order

Its time saving and more readable when every component holds the same convention. Put positioning related properties
like `flex`,  `display`, `position` at the top. Colors and whitespacings like `background`, `margin`, `padding` can be
at the bottom. Try to glue similar things like `font-size`, `line-height`, `font-weight` together for context.

No strict rules here, just make it nice to read and consistent over the app. You can always inspire from surrounding
components.
If you wanna play nice do some Enter paddings .]

**❌ Bad:**

```css
  .loading {
    background: var(--gray-300);
    font-size: 14px;
    line-height: 19px;
    flex-direction: column;
    display: flex;
    animation: scale 4.5s ease-in-out infinite;
    align-items: center;
    height: 240px;
    border-radius: 100%;
    margin-top: var(--space-4);
}

```

**✔️ Good:**

```css
.loading {
    display: flex;
    flex-direction: column;
    align-items: center;

    height: 240px;
    border-radius: 100%;

    font-size: 14px;
    line-height: 19px;

    margin-top: var(--space-4);
    background: var(--gray-300);

    animation: scale 4.5s ease-in-out infinite;
}

```

### Good naming suggestion

The intention of these suggestions is consistency and avoiding pitfalls.

Use `body` over `content`. Means the same, but `body` is extensible to accommodate with headers and footers.

**❌ Bad:**

```html
<div class="loading__content"/>
```

**✔️ Good:**

```html
<div class="loading__body"/>
```

For technical CSS limitations, sometimes is needed to wrap an element.
Let's call it `container`, not `wrap` nor `wrapper`

**❌ Bad:**

```html
<div class="loading__wrap"/>
```

**✔️ Good:**

```html
<div class="loading__container"/>
```

Container for buttons or action elements is called `controls`

**❌ Bad:**

```html
 <div class="dialogue-message-consumer__container">
     <button @click="parse"/>
     <button @reset-clicked="clear"/>
 </div>
```

**✔️ Good:**

```html
 <div class="dialogue-message-consumer__controls">
     <button @click="parse"/>
     <button @reset-clicked="clear"/>
 </div>
```

### Not recommended words for naming

Here are some common mistakes when naming variables or functions and some suggestions on how to fix them.
These examples may be confusing, too general, quickly goes into conflict, or express f subjective evaluation.
There may be cases where these would be valid of course

```
data -> details
```

```
info -> description
```

```
type -> variant
type -> [whatever else more specific]Type
```

```
item -> [whatever else more specific]
item -> [whatever else more specific]Item
```

```
value -> formattedValue
```

```
result -> response -> [whatever else more specific]
```

```
text -> heading
text -> paragraph
text -> description
text -> [whatever else more specific]Text
```

```
box -> container
box -> input
```

```
pretty -> formatted
```

## CRUD UI actions naming convention

`New Entity` -> (fill details) -> `Create Entity`

`Edit Entity` -> (change details) -> `Save Entity`

`Delete Entity` -> Are you sure? modal -> `Delete Entity Forever`


### Component has no whitespacing

For proper component isolation, component root element should be free of whitespacing. Spacing of component should be
done on parent level. This should be done on styles level. No need to parametrize styles through props.

**❌ Bad:**

```vue
<template>
  <user-item>
  <user-item>
  <user-item :no-bottom-padding="true">
</template>

```

**✔️ Good:**

```vue

<template>
  <user-item class="user-list__item">
  <user-item class="user-list__item">
  <user-item class="user-list__item">
</template>

<styles>
.user-list__item {
  margin: 16px;
  &:last-of-type {
   margin: 0;
  }
}

</styles>

```

## VUE
### Keep component length on reasonable length

As for the method length, components easily grow larger. In most cases, there is no such thing aso
over-componentization. The opposite true. Lets keep components on reasonable length. Personal preference 150 lines of
code.

### Write events in past tense

Event represents action and bound method represents reaction.
So the way that you read is: when something happened -> then do this.
This is a self-imposed rule, but its nothing against Vue styleguide.

**❌ Bad:**

```vue
<button @send-button-press="uploadImage()"/>
```

**✔️ Good:**

```vue
<button @send-button-pressed="uploadImage()"/>
```


### Less logic in the template

Keep the template part free from logic. A nice place to accommodate logic is in `computed` block. If the condition should be
a composite of 2 or more conditions, extract them to `computed`. The new name of the computed condition should reflect what UI is
doing.

**❌ Bad:**

```vue
<template>
  <button v-if="!isLoading || userCount > 1 && isTraining">
</template>

```

**✔️ Good:**

```vue

<template>
  <button v-if="isButtonHidden"/>
</template>

<script>
computed: {
  isButtonHidden () {
    return this.isLoading || this.userCount > 1 && this.isTraining
  }
}
</script>

```

## Components naming

Components are written inPascalCase, minimum 2 words.
Component name should consist of Domain of the feature and Element type (preferably imitating known UI patterns).
Component can also be named with the modifier state. Mostly when componentizing complex state
behaviour. `dialogue__message--delivered` -> `DialogueMessageDelivered.vue`

**❌ Bad:**

```
ComingSoon.vue
LayoutLogin.vue
```

**✔️ Good:**

```
LoginLayout.vue
ChatForm.vue
BotCard.vue
DialogueActionMenu.vue
TrainingButton.vue
```
