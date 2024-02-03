---
title: 'what are props ?'
description: 'Props are custom attributes that you can register on a component. They allow you to pass data from a parent component to a child component. This communication between components enables building modular and reusable code.'
slug: 'what-are-props'
featureImg: 'https://miro.medium.com/v2/resize:fit:1024/1*4jQEMGWtdEINepQ20STJPA.png'
# draft: true
---

# Understanding Vue.js Props

Vue.js projects consists of components that are reusable pieces of code (javascript) + markup (html).
now more often that not, you will come across a scenario where you will have to modify the component UI or the behaviour in different contexts.

Thats where props come in...

## What are Props?

Props are custom attributes that you can register on a component. They allow you to pass data from a parent component to a child component. This communication between components enables building modular and reusable code while allowing you to modify the component UI or behaviour in different contexts.

## Props were there from the start !

Now, talking about props take a look at the following block of code.

```html
<!-- 
  this is simple input html element which
 renders a simple text input on the screen 
 -->

<input />

<!-- 
  now what if i want a different type of input element,
 lets say a date time input, i would simply provide the 
 `type` prop
 -->

<input type="date" />

<!-- 
  and now i see the input is a date time input, 
  which i can select dates with

  following are the possible types you can use 
  as your `type` prop value
-->

<!-- renders a text input -->
<input type="text" />

<!-- renders a button -->
<input type="button" />

<!-- renders a search input -->
<input type="search" />

<!-- renders a text input which only allows numbers -->
<input type="number" />

<!-- renders a color picker -->
<input type="color" />
```

## Declaring Props in Vue.js

In Vue.js, props are declared in the child component's `script` block using the `defineProps` macro. Here's a simple example:

```vue
<!-- File: Text.vue -->

<script setup>

defineProps<{
  message: string
}>()
</script>

<template>
  <p>{{ message }}</p>
</template>
```

## Using the Component with Props

lets use the `Text.vue` component in our `Parent.vue` component:

```vue
<!-- File: Parent.vue -->

<script setup>
import Text from './Text.vue'
</script>

<template>
  <div class="parent-wrapper">
    <Text message="this is nice !" />
  </div>
</template>
```

if you want to bind the message prop to some ref in the parent component

```vue
<!-- File: Parent.vue -->

<script setup>
import Text from './Text.vue'

const name = ref('Arslan')
</script>

<template>
  <div class="parent-wrapper">
    <Text :message="name" />
  </div>
</template>
```

with that your `message` prop is now bound to the `name` ref, whenever the `name` ref updates, your `message` prop will update and hence the `<Text/>` component would re-render.
