---
id: exploring-shadcn-vue
aliases:
  - 🛥️ Exploring Shadcn-Vue
tags: []
title: 🛥️ Exploring Shadcn-Vue
---

[Shadcn](https://www.shadcn-vue.com/) seems to be a wrapper around [radix-vue](https://www.radix-vue.com/). It is not a component library, but a framework for allowing you to easily create your own component libraries. This is nice for using nicely designed components without being forced to have a noticeable forced style in your application, like you would have when you used bootstrap or material design.

## Installing Components

One of the down falls of component libraries that are implemented as a Vue plugin is that you need to import the whole library even if you just use a single part of it. With [shadcn-vue](https://www.shadcn-vue.com/) you only import the components that you use, and you do not install an NPM package for each component, instead you run a script that imports the code for a component into your project. Allowing you to easily update the sub-components to suit your needs. Specifically in terms of re-styling.

E.g. installing the card component can be done by entering:

```tsx
npx shadcn-vue@latest add card
```

## Component Design

All components are insanely small, separating function from styling. For instance for the [card](https://www.shadcn-vue.com/docs/components/card.html) component, there is no single parent card element that takes in multiple props to define how it should be rendered. There are just a collection of small components that make up visual elements that are specifically designed for use with the parent card component.

For instance, I created the following:

```html
<template>
  <Card class="w-[250px]">
    <CardHeader>
      <CardTitle>{{ props.box.name }}</CardTitle>
      <CardDescription>Location: {{ props.box.location }}</CardDescription>
    </CardHeader>
    <CardFooter class="flex justify-end px-6 pb-6">
      <button
        @click="() => {
      router.push({ name: 'boxContents', params: { id: box.id }})
    }"
      >
        Open
      </button>
    </CardFooter>
  </Card>
</template>
```

Which ends up looking like this:

![](Pasted%20image%2020240914144931.png)

The entire card title is just a few lines of code:

```html
<script setup lang="ts">
  import type { HTMLAttributes } from "vue"
  import { cn } from "@/lib/utils"

  const props = defineProps<{
    class?: HTMLAttributes["class"]
  }>()
</script>

<template>
  <h3
    :class="
      cn('text-2xl font-semibold leading-none tracking-tight', props.class)
    "
  >
    <slot />
  </h3>
</template>
```

This component is used to create the default title, but if you wanted to use the card with a different title, you could just style your own, and if you add CSS classes to the component itself, how the classes get added to the `title` is clearly defined (classes might not be added to the root element).

### Imports

One of the things I liked the most was how components are organized and then imported. The components directory gets a `ui` sub folder that contains folders for all the [shadcn-vue](https://www.shadcn-vue.com/) components that have been installed.

```html
. ├── boxEntry.vue ├── createBox.vue └── ui ├── button │ ├── Button.vue │ └── index.ts ├── card │
├── Card.vue │ ├── CardContent.vue │ ├── CardDescription.vue │ ├── CardFooter.vue │ ├──
CardHeader.vue │ ├── CardTitle.vue │ └── index.ts ├── input │ ├── Input.vue │ └── index.ts └── label
├── Label.vue └── index.ts
```

The components are defined just like you would normally define a single file component using either the options or composable API. Then the `index.ts` file is used to make all nested components modular:

```tsx
// Contents of card/index.ts
export { default as Card } from "./Card.vue"
export { default as CardHeader } from "./CardHeader.vue"
export { default as CardTitle } from "./CardTitle.vue"
export { default as CardDescription } from "./CardDescription.vue"
export { default as CardContent } from "./CardContent.vue"
export { default as CardFooter } from "./CardFooter.vue"
```

This makes it so that you can import these components using destructuring:

```tsx
import { Card, CardDescription, CardFooter, CardHeader, CardTitle } from "@/components/ui/card"
```

## Passing CSS classes as properties

[Shadcn](https://www.shadcn-vue.com/) uses this to pass css classes to specific elements within a component. For example here is the props for the [`label` component](https://www.shadcn-vue.com/docs/components/label.html):

```jsx
const props = defineProps<LabelProps & { class?: HTMLAttributes['class'] }>()
```

Interestingly it does not define any defaults, ore required flags, it just creates a generic type using this `LabelProps` interface and a literal. This is something that comes from: https://www.radix-vue.com/. I thought it is a really cool way of defining prop interfaces.

## Downsides

Both [Shadcn](https://www.shadcn-vue.com/) and [radix-vue](https://www.radix-vue.com/) make heavy use of [tailwindcss](https://tailwindcss.com/). Which has the immediate downside of large compiled CSS files in your application. A variation of this application that does not make use of [tailwind](https://tailwindcss.com/) has been asked for on [GitHub](https://github.com/shadcn-ui/ui/discussions/2832).

## Conclusion

I will continue using this library on some personal projects and use it as a way of learning more about creating web component libraries in the future.
