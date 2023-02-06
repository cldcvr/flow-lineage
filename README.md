
# Flow Lineage
A lineage chart is a graphical representation of a node's ancestors, showing the relationships among nodes. It is often used in analytics to show the relations and to trace their ancestry. Lineage charts can be in the form of a hierarchy data, showing the relationships between parents and children, or they can be more complex and show the relationships between more distant nodes.

<br>

# Demo
Head over to [Flow Lineage Storybook](https://flow.cldcvr.com/lineage/index.html?path=/story/components-f-lineage--playground) for a demo. 

or

Clone and install the [Flow Lineage demo](https://github.com/cldcvr/flow-lineage-starterkit-vue) (Vue 3).

<br>

# Getting started

Flow Lineage is been built on [Flow](https://flow.cldcvr.com/), an open source design framework. To run lineage, please make sure that you have [Flow core](https://github.com/cldcvr/flow-core) as part of your project.

While installation if you run into any issues, head over to our [known issues + solutions document](https://github.com/cldcvr/flow-lineage/blob/main/KNOWN_SOLUTIONS.md) to see if a solution already exists.

**Note:** If you already have Flow packages installed, please update to the latest versions

**Note:** If you do not have an existing front-end project, you can quickly create one from a [flow starter kit](https://github.com/cldcvr/flow-core#starter-kits). 

<br>

## Installation

### 1️⃣ Install flow lineage dependency
```
yarn add @cldcvr/flow-lineage
```
**Note:** after installation, re-start your application.

<br>

### 2️⃣ Import styles/CSS 
For **Vue JS:** 
Paste the below snippet after the closing `<template>` tag in your `App.vue` file
```html
<style>
 @import "@cldcvr/flow-lineage/dist/style.css";
</style> 
```
<details>
<summary>For React</summary>

**React:** Paste the below snippet in `src/index.tsx` or `index.jsx` file
```Javascript
import "@cldcvr/flow-lineage/dist/style.css";
```
</details>

<details><summary>For Angular</summary>

**Angular:** Add css file path in `angular.json` in `styles` property array.

```json
"styles": ["@cldcvr/flow-lineage/dist/style.css"],
```
</details>
<br>


### 3️⃣ Import flow-lineage into your project

Paste the below snippet in your project and add your application startup/runtime code to it. 

**Note:** This is required to register Flow elements error-free. We achieve this by importing all flow packages asynchronously and then starting up your application.

For **Vue JS:** 
Paste the below snippet in your project, for `src/main.ts` or `main.js`
```javascript
import("@cldcvr/flow-core").then(async () => {
	await import('@cldcvr/flow-lineage');
	//add your application startup/runtime code here **
});
```

<details>
<summary>For React</summary>

Paste the below snippet in your project, for `src/main.ts`

```javascript
import("@cldcvr/flow-core").then(async () => {
	await import("@cldcvr/flow-lineage");
	//add your application startup/runtime code here **
});
```
</details>

<details><summary>For Angular</summary>

Paste the below snippet in your project, for `src/index.tsx` or `index.jsx`

</details>



<br>

<details><summary>Example</summary>

**VueJS:** In the following example, I imported `@cldcvr/flow-core` and then imported the rest of the flow packages including `@cldcvr/flow-lineage` and after that startup code was added for VueJs `createApp(App).use(router).mount(“#app”);`.

```javascript
import("@cldcvr/flow-core").then(async () => {
  await import("@cldcvr/flow-system-icon");
  await import("@cldcvr/flow-product-icon");
  await import("@cldcvr/flow-lineage");
  createApp(App).use(router).mount("#app"); //runtime
});

```
</details>

<br>

### 4️⃣ For a typescript enabled project (optional)

**Note:** after adding, re-start your application.

**For Vue 3:**
Copy paste below import types in your `main.ts` file.
```Javascript
import "@cldcvr/flow-lineage/dist/types/vue3";
```
<details>
<summary>For Vue 2</summary>

Copy paste below import types in your `main.ts` file.

```Javascript
import "@cldcvr/flow-lineage/dist/types/vue2";
```
</details>

<details>
<summary>For React</summary>

**React**: Include react type in `tsconfig.json` file like below.
```json
"include": ["src", "./node_modules/@cldcvr/flow-lineage/dist/types/react.ts"]
```
</details>
<br>

<br>



# Sample code (Vue JS)
We have created a sample lineage component along with it's schema to get you going, simply copy paste the below language code block in your FE project.

## Template
```html
<template>
  <f-lineage
    direction="horizontal"
    :padding="28"
    :gap="100"
    :node-size.prop="{ width: 240, height: 53 }"
    :children-node-size.prop="{ width: 240, height: 32 }"
    :max-childrens="8"
    :links.prop="links" 
    :nodes.prop="nodes"
    :node-template="nodeTemplate"
    :children-node-template="childNodeTemplate"
  ></f-lineage>
</template>
```

## Script
```html
<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "FlowLineage",
  data() {
    return {
      nodes: {
        rdj: {
          templateData: {
            fullName: "Robert Downey Jr.",
            description: "Movies",
          },
        },
        judge: {
          templateData: {
            fullName: "The Judge",
            description: "Hank Palmer",
          },
        },
        ironman: {
          templateData: {
            fullName: "Iron Man",
            description: "Tony stark",
          },
          children: {
            irchild1: {
              templateData: {
                icon: "i-hashtag",
                title: "Iron man 1",
              },
            },
            irchild2: {
              templateData: {
                icon: "i-paragraph",
                title: "Iron man 2",
              },
            },
          },
          hideChildren: false,
        },
      },
      links: [
        {
          from: "rdj",
          to: "judge",
        },
        {
          from: "rdj",
          to: "ironman",
        },
      ],
      nodeTemplate: `
			<f-div width="100%" state="secondary" height="100%" padding="small" align="top-left" variant="curved" gap="small">
				<f-pictogram variant="circle" source="\${node.templateData.fullName}"></f-pictogram>
				<f-div direction="column">
					<f-text size="small" ellipsis>\${node.templateData.fullName}</f-text>
					<f-text size="x-small" ellipsis>\${node.templateData.description}</f-text>
				</f-div>
				\${node.childrenToggle}
			</f-div>
			`,
      childNodeTemplate: `
			<f-div state="secondary" width="100%" height="100%"padding="none medium" align="middle-left" gap="small" border="small solid default bottom" >
				<f-icon source="\${node.templateData.icon}" size="small"></f-icon>
				<f-text  size="small" ellipsis>\${node.templateData.title}</f-text>
		  </f-div>
			`,
    };
  },
});
</script>

```

</p>


Once it's running, you will see a lineage component like the image below.

![image (10)](https://user-images.githubusercontent.com/2121451/211773535-3fbc3b2b-b962-4cb3-9713-d50906b88243.png)


</details>


# Properties

Head over to [Flow Lineage Storybook](https://flow.cldcvr.com/lineage/index.html?path=/docs/components-f-lineage--playground) for all properties and playground.



<br>

# Lineage templates
Flow nodes are represented through templates, this allow you to  easily change, or write and use your own node template.


Head over to [Flow Lineage templates](https://flow.cldcvr.com/lineage/index.html?path=/story/introduction-about--page) to view whats available.  






