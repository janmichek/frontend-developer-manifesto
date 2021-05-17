# Frontend Developer Manifesto
The set of evergreen rules, best practices, commonly mistaken concepts and personal preferences in structured form

## Key Concepts
**Optimizing code for readability** - we spend much more time looking at the code. Better write more of encapsulated code than less lines of code on one place.

**Aha Programming** - use abstraction when its super-obvious. Till that moment its fine to duplicate. https://kentcdodds.com/blog/aha-programming/

**Components** - are reusable, isolated UI elements

**Clean Code** - evergreen universal programming hints https://cleancoders.com/  -> accommodated for JS https://github.com/ryanmcdermott/clean-code-javascript/

**Desktop First** - Only optimizing for 1024px width, IE 10+

Things that cannot be automated written here. If you go around some unaligned code, feel free tor refactor little bit.


## Styles

We are using:
- Postcss https://postcss.org/
- Flexbox https://css-tricks.com/snippets/css/a-guide-to-flexbox/
- BEM https://en.bem.info/methodology/
- ITCSS https://frontend.garden/proc-je-itcss-nejpokrocilejsi-metodika-organizace-css/


### Every styled element needs to be classnamed

In BEM every styled element needs to be named.

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



### Use negative classnaming

When creating component with binary state (eg: `hidden` / `visible`), use negative classname or attribute for hiding. Then the default state, without any name, will be the visible state.

As from HTML standards some of the elements has `hidden` od `disabled` attribute. Developer expects that when they declare HTML element or component in its simplest form, it will be present on screen. No need to declare anything extra to make it working.


**❌ Bad:**


```html
<div :class="tabs-details-item tabs-details-item--disabled"/>
```


**✔️ Good:**

```html
<div :class="tabs-details-item tabs-details-item--enabled"/>

```



### No Dependant Selectors

This is actually BEM antipattern. Dependant selectors are responsible for many mistakes when stylesheet grows. Come up with better BEM naming or componentize one level more.

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


###  Come up with valid BEM naming

If you struggle to come up with naming – it’s mostly a symptom of poor componentization. Good opportunity to make new component.

**❌ Bad:**

```html
<!-- In context of Tabs component --!>
<div :class="tabs__content__icon--disabled"/>
```


**✔️ Good:**

```html
<!-- New component TabsIcon inside Tabs --!>
<div :class="tabs-icon--disabled"/>

```

### Use sizing naming

For sizing we use bootstrap style sizing https://getbootstrap.com/docs/4.1/layout/grid/

`[xs] [sm] [md] [lg] [xl]`


**❌ Bad:**

```html
<button class="button button--huge"/>
```


**✔️ Good:**

```html
<button class="button button--xl"/
```

### Use plenty of classnames
No need to save on amount of classnames. On this place we can be wasteful with names. One classname should do less things possible.


**❌ Bad:**

```html
<button class="dialogue-element__delete-action--draggable"/>

<styles>
    .dialogue-element__delete-action--draggable {}
</style>
```

**✔️ Good:**

```vue
<div class="dialogue-element__action dialogue-element__action--delete dialogue-element__action--draggable">

<styles>
.dialogue-element__action {}
.dialogue-element__action--delete{}
.dialogue-element__action--draggable {}
</style>
```


### No names shortening
If there is no technical limitation, use full names to avoid mental mapping.

**❌ Bad:**

```html
<button class="btn btn-dbu"/>
```


**✔️ Good:**

```html

<button class="button button--disabled"/>

```


### Prioritize properties order
Its time saving and more readable when every component holds the same convention. Put positioning related properties like `flex`,  `display`, `position` at the top. Colors and whitespacings like `background`, `margin`, `padding` can be at the bottom. Try to glue similar things like `font-size`, `line-height`, `font-weight` together for context.

No strict rules here, just make it nice to read and consistent over the app. You can always inspire from surrounding components.
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

The intention of these suggestions are consistency and avoiding pitfalls.

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


## JS


### Functions naming

Functions names should consist of verb.  If function returns Boolean should be prefixed `is / has`.


**❌ Bad:**

```javascript

newline () {
  this.messageText = `${this.messageText} \n`
}

loading() {
  return !this.events
}
```

**✔️ Good:**

```javascript

printNewline () {
  this.messageText = `${this.messageText} \n`
}

isLoading() {
  return !this.events
}
```


### Use meaningful and pronounceable variable names

**❌ Bad:**

```javascript
const yyyymmdstr = moment().format("YYYY/MM/DD");
```

**✔️ Good:**

```javascript
const currentDate = moment().format("YYYY/MM/DD");
```


### Functions should do one thing
No example for this. Just keep things simple. Functions tend to suffer from complexity in most of the cases. If you passing 5 arguments you probably doing something nasty inside. If function is long, its also a symptom you are doing a lot of things on one place.


### Methods should be small, smaller than small
Evergreen programming hint similar to hint above. There is no hard limit. When functions are short and nicely named, It will be joy to read. I personally prefer max 4 lines.


### Don't add unneeded context for functions
This is context dependant. The closer to occurrence you are the less specific you should be.

**❌ Bad:**

```vue
<--! in context of UploadImageForm !-->
<button submit="uploadImage()"/>
```

**✔️ Good:**

```vue
<--! in context of UploadImageForm !-->
<button submit="upload()"/>
```


### Don't add unneeded context for variables

If your class/object name tells you something, don't repeat that in your
variable name.

**❌ Bad:**

```javascript
const Car = {
  carMake: "Honda",
  carModel: "Accord",
  carColor: "Blue"
};

function paintCar(car) {
  car.carColor = "Red";
}
```

**✔️ Good:**

```javascript
const Car = {
  make: "Honda",
  model: "Accord",
  color: "Blue"
};

function paintCar(car) {
  car.color = "Red";
}
```


### Avoid Mental Mapping

Explicit is better than implicit.

**❌ Bad:**

```javascript
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach(l => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  // Wait, what is `l` for again?
  dispatch(l);
});
```

**✔️Good:**

```javascript
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach(location => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  dispatch(location);
});
```



### Avoid Side Effects

A function produces a side effect if it does anything other than take a value in
and return another value or values. A side effect could be writing to a file,
modifying some global variable, or accidentally wiring all your money to a
stranger.

Now, you do need to have side effects in a program on occasion. Like the previous
example, you might need to write to a file. What you want to do is to
centralize where you are doing this. Don't have several functions and classes
that write to a particular file. Have one service that does it. One and only one.

The main point is to avoid common pitfalls like sharing state between objects
without any structure, using mutable data types that can be written to by anything,
and not centralizing where your side effects occur. If you can do this, you will
be happier than the vast majority of other programmers.


**❌ Bad:**

```javascript
// Global variable referenced by following function.
// If we had another function that used this name, now it'd be an array and it could break it.
let name = "Ryan McDermott";

function splitIntoFirstAndLastName() {
  name = name.split(" ");
}

splitIntoFirstAndLastName();

console.log(name); // ['Ryan', 'McDermott'];
```

**✔️ Good:**

```javascript
function splitIntoFirstAndLastName(name) {
  return name.split(" ");
}

const name = "Ryan McDermott";
const newName = splitIntoFirstAndLastName(name);

console.log(name); // 'Ryan McDermott';
console.log(newName); // ['Ryan', 'McDermott'];
```


## Vue


### Pass less data to component
Choosing accurate property name gives you more sense about what is going on inside component. Passing exact value (instead of object) saves boilerplate code on component side. Passing exact value makes it isolated from context and reusable. It is also possible to check prop type and values. There are also security reasons for not to expose the whole tree of data.


**❌ Bad:**

```vue
<template>
  <div
    :class="`conversation-avatar--${event.side}`">
    <app-initials
      :conversation-id="event.conversation_id"
      :name="event.customer_name"/>
  </div>
</template>

<script>
  export default {
    props: {
      event: {
        type: Object,
        required: true,
      },
    },
  }
</script>

```

**✔️ Good:**

```vue
<template>
  <div
    :class="`conversation-avatar--${side}`">
    <app-initials
      :conversation-id="conversationId"
      :name="customerName"/>
  </div>
</template>

<script>
  export default {
    props: {
      side: {
        type: String,
        required: true,
        validator: val => ['consumer', 'bot'].includes(val),
      },
      conversationId: {
        type: Number,
        required: true,
      },
      customerName: {
        type: String,
        required: true,
      },
    },
  }
</script>

```



### Keep component length on reasonable length
As for the method length, components easily grow larger. In most cases, there is no such thing aso over-componentization. The opposite true. Lets keep components on reasonable length. Personal preference 150 lines of code.



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


## Wrap components from UI library

UI components from library are building blocks for App. App is an composition of interconnected components. Wrapping components for exact purpose is a sweetspot to keep things organized and named. If there would be UI components used right on the 'page', the page component would grow very large. This approach encapsulates source code both in fact and mentally.


**✔️ Good:**

```vue
 // assuming <app-button>, <app-icon> and <indicator-dot> are from UI library
<template>
  <app-button
    class="training-button"
    :disabled="isTraining"
    @click.native="train">
    <template #icon>
      <app-icon
        v-if="!isTraining"
        name="model_training"
        :size="19"/>
      <training-loader
        v-else
        class="training-button__loader"/>
    </template>
    <template #indicator>
      <indicator-dot
        v-if="!isIndicatorHidden"
        status="warning"/>
    </template>
    {{ label }}
  </app-button>
</template>

<script>
  export default {
    name: 'TrainingButton',
    props: {
      isTraining: {
        type: Boolean,
        required: true,
      },
      isChanged: {
        type: Boolean,
        required: true,
      },
    },
    computed: {
      label () {
        return !this.isTraining ? 'Train The Bot' : 'In Training'
      },
      isIndicatorHidden () {
        return !this.isChanged || this.isTraining
      },
    },
    methods: {
      async train () {
        this.$emit('clicked')
      },
    },
  }
</script>

<style scoped>
  .training-button {
    width: 185px;

    &:disabled {
      border-color: transparent;
      background: transparent;
    }

    &__loader {
      margin: 2px;
    }
  }
</style>

```



### Less logic in template
Keep template part free from logic. Nice place to accommodate logic is in `computed` block. If the condition should be composite of 2 or more conditions, extract them to `computed`. New name of computed condition should reflect what UI is doing.

**❌ Bad:**
```vue
<template>
  <button v-if="!isLoading || !isChanged || isTraining">
  </div>
</template>

```

**✔️ Good:**

```vue

<template>
  <button v-if="!isButtonHidden"/>
</template>

<script>
computed: {
  isButtonHidden () {
    return  this.isLoading && this.isChanged && !this.isTraining
  }
}
</script>

```


### Component has no whitespacing
For proper component isolation, component root element should be free of whitespacing. Spacing of component should be done on parent level. This should be done on styles level. No need to parametrize styles through props.


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


### Duplicated names for data and props
For lifecycle reasons there may be `props` and `data` needed. Data holds inner state while props may change value from outer source. They both express the same user feature, but differs in technical aspect. That can be messy with naming.
When extending component for these reasons, the prop name should be more explicit.


**❌ Bad:**

```vue
// DialogueNameInput.vue
<template>
  <input
    v-model="internalValue"
    type="text"
    @keyup.enter="confirm">
</template>

<script>
  export default {
    props: {
      name: {
        type: String,
        default: null,
      },
    },
    data () {
      return {
        internalValue: this.name,
      }
    },
    watch: {
      value (newVal) {
        this.internalValue = newVal
      },
    },
    methods: {
      confirm (event) {
        this.$emit('confirmed', this.internalValue)
      },
    },
  }
</script>


```

**✔️ Good:**

```vue
// DialogueNameInput.vue
<template>
  <input
    v-model="name"
    type="text"
    @keyup.enter="confirm">
</template>

<script>
  export default {
    props: {
      dialogueName: {
        type: String,
        default: null,
      },
    },

    data () {
      return {
        name: this.dialogueName,
      }
    },

    watch: {
      dialogueName (newName) {
        this.name = newName
      },
    },

    methods: {
      confirm (event) {
        this.$emit('confirmed', this.name)
      },
    },
  }
</script>


```


### Names for passed v-model to props
Declaring `v-model` creates reactive input and output. Sometimes we want to manipulate properties within document.
Declared `v-model` appears as `value` property on component side. Then rename value to something meaningful as soon as possible.

**❌ Bad:**
```vue
// declared v-model on parent component UserSelect
    props: {
      value: {
        type: Array,
        required: true,
      },
    },
    data () {
      return {
        internalValue: this.value,
      }
    },
```


**✔️ Good:**

```vue
// declared v-model on parent component UserSelect
    props: {
      value: {
        type: Array,
        required: true,
      },
    },
    data () {
      return {
        selectedUser: this.value,
      }
    },
```


### Abstracting for styles is not recommended
Component isolation sometime means styles duplication in nature of this concept. Lets use abstraction for styling, only if it saves huge amount of styles. Making abstraction only to save few lines of css properties is not a good reason to come up with parent component.

There are some other ways around which needs to be discussed carefully and tried per case (mixin/include, global stylesheet, not scoped styles, utility class)


##  Components naming
Components are written inPascalCase, minimum 2 words.
Component name should consist of Domain of the feature and Element type (preferably imitating known UI patterns).
Component can also be named with the modifier state. Mostly when componentizing complex state behaviour. `dialogue__message--consumer` -> `DialogueMessageConsumer.vue`


**❌ Bad:**

```
ComingSoon.vue
LayoutStatic.vue
```

**✔️ Good:**

```
ChatForm.vue
BotCard.vue
DialogueActionMenu.vue
TrainingButton.vue
DialogueMessageConsumer.vue
```



## Vuex
 We use Vuex for state management https://vuex.vuejs.org/

Here are some best practices how to manage state:
https://gist.github.com/DawidMyslak/2b046cca5959427e8fb5c1da45ef7748

### Functions to store
UI should be just a simple value presenter and user events listener with as less logic as possible. We don't want tightly coupled UI and data functions on component level.
In app size of Bot Builder its good idea to assume that different components will be interacting with themselves despite DOM tree. This could be clearly achieved by store solution.
For future documentation to UI library we cannot hold data manipulating function within components.

###  Store Flow
This may be not the shortest flow, but its universal for every case

1. Submit UI for change
```vue
 <intent-input @submit="createIntent"/>
```

2. Method in component is triggered
```javascript
  async createIntent (newIntentName) {
       await this.addIntent(newIntentName)
         ...
  },
```

3. Store action is triggered
```javascript
    async addIntent ({ commit }, intentName) {
     ...
    },
```

4. APICall will manipulate the data source
```javascript
    try {
      await this._vm.$api.createIntent(intentName)
    } 
```

5. After successful creating, reload data from data source to store
```javascript
    async createIntent (newIntentName) {
        await this.addIntent(newIntentName)
        await this.loadIntents()
      },
```

6. Fetched response is committed to store state
```javascript
        commit('setIntents', intents.data)
```

7. State is updated and sends reactive update about change 
```javascript
    setIntents (state, value) {
      state.intents = value
    },
```

8.  Component with registered mapGetter will be reactively notified and updates component data
```javascript
    ...mapGetters({
        intents: 'nlu/getIntents',
      }),
```


### Data functions naming
To avoid conflicting names within flow loop, follow this classic CRUD naming
Component -> Store -> API

    createItem -> addItem -> createItem
    loadItem -> fetchItem -> getItem
    editItem -> changeItem -> updateItem
    deleteItem -> removeItem -> deleteItem




## Others

If there is technical limitation, code obvious and  well named solution, so its clear we are hacking something. Do not use any of bad examples to go around possible technical limitation.

### Comments in code

Intention of code should be clear.
Master should be free from commented code.
Master should be free from `// todo comments`
Better use github Issue instead of code comments.
Comments are allowed when hackish or exotic solution is used.



### Removal/edit guide

When removing / editing feature, you may also remove part of code which serves as an abstraction for accommodate feature itself. This is hard to discover. Leaving unused code makes unnecessary complexity without new reason. It bloats the code in longer term.

When developer edits or removes the feature, there should be mental hook for deeper investigation.

Hints how to make clear changes:
- Try to `revert` the functionality, not `erase` currently working code
- Find the initial Issue and Pull Requests from the moment when the initial feature was implemented and changed. You can see how much effort around was put to accommodate feature itself.
- Use `Find Usages` tool in your IDE
- Doublecheck parent component, children components and siblings. That gives you more clues.
- The surrounding code may now not be dependant. Especially with html / css we often add containers to wrap components. Maybe after delete/edit this container is not needed. Maybe the absolute positioning is not needed anymore.



### Not recommended words for naming
Here are some common mistakes when naming variables or functions and some suggestions how to fix them.
These examples may be confusing, too general, quickly goes to conflict or express f subjective evaluation.
There may be cases where these would be valid of course

```
data -> details
```

```
info -> description
```

```
type -> variation
```

```
item -> [whatever else more specific]Item
```

```
value -> formattedValue
value -> propValue
```

```
result -> response
```

```
text -> heading
text -> paragraph
text -> messageText
```

```
box -> container
box -> input
```

```
pretty -> formatted
```




## UI actions naming convention
`New Entity` -> (fill details) -> `Create Entity`

`Edit Entity` -> (change details) -> `Save Entity`

`Delete Entity` -> Are you sure? modal -> `Delete Entity Forever`





