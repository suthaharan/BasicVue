### Resources
* CDN Library Source: https://cdnjs.com/libraries/vue/2.7.14
* Unpackage: https://unpkg.com/ ( https://unpkg.com/vue@2.7.14/dist/vue.js )

### Lessons Learnt

* 01 - Getting Started with Vue
  * Basic HTML template with Vue js file from CDN
  * Create new Vue instance
  * Target the ID in HTML
  * Add a data property to config object and set a header property that you can use in the HTML template using double moustache syntax
  * Reactivity system in Vue usind v-model directive. With Vue, data is bound both ways
  ```
    In the console set the variable header and see the text change in the browser

    myshoppingList.$data.header = "Hello! from Vue Beginner"
  ```

* 02 - Template and Syntax Expression
  * Within double moustache expression only one expression can be evaluated at a time
  ```
  {{ header.toLocaleUpperCase() }}
  ```
  * Also, we can't declare variables or do a if logic statements in double moustache expression. If needed, you can use ternary statement or shorthand if expression 

* 03 - List Rendering
  * We will add an array of items and use a directive called v-for to loop through the items
  * The directive v-for is reactive as well. You can add or remove items from the list and it will get dynamically reflected in the browser. In the browser console, perform the following actions 
  ```
    myshoppingList.$data.items.push('5 coffees')
    myshoppingList.$data.items.pop()
  ```

* 04 - User Input and Dev Tools
  * Let's add back user input field and establish two way data binding. Then, declare the variable in the data object
  * Add in the following code in the browser console
    ```
    myshoppingList.$data.newItem = "3 Ice Coffee"
    ```
  * Now, let's install Vue dev tool and enable the file protocol for vue.js code debugging. To do that, go to browser More Tools > Extensions > Details > Allow access to file URLs and ensure it is checked. This will make Vue extension appear in the browser inspector window.
  * You may get a message "Devtools inspection is not available because it's in production mode or explicitly disabled by the author." if you use minified version of vue.js. 
  * Select the Vue tab from the Inspector window (you may need to restart the browser) and set the newItem variable with the new value
  
* 05 - User Events
  * Using vue dev tools we can rapidly test different ways to implement features for our Vue application. Vue Devtools injects our Vue instances into the console for us so we can test and manipulate them without relying on setting up the values via variables.
  * In the console, we can type $vm0 to interact with the Vue instance. You can interact with the Vue instance by typing
  ```
    $vm0.items
    $vm0.newItem = "10 Cheese sticks"
    $vm0.items.push($vm0.newItem)
  ```
  * Event listeners: v-on:keyup.enter(@keyup.enter), v-on:click (@click). Inside the template, Vue is smart enough to know the Vue instance that is being used in the application. 

* 06 - Methods
  * Inside Vue instance we can define methods object where we can add method to encapsulate specific functionality for our Vue instance. We will have to use "this" keyword to get a reference to the Vue instance data. We can write cleaner javascript and cleaner methods to maintain our template. 
  ```
                  saveItem: function(){
                    this.items.push(this.newItem);
                    this.newItem = '';
                }
  ```
  * We are in charge of maintaining the state of the variable in Vue
  * We can also test the functionality via Vue dev tools. Now type some value in the input box and then type the below in the console.
  ```
  $vm0.saveItem();
  ```

* 07 - Conditional Rendering
  * Directives: v-if and v-else to conditionally render elements
  * Adding methods to change the state of the presentation layer

* 08 - Attribute Bindings
  * We use Vue's double mustache syntax to render data to the DOM
  * To make any HTML attribute such as href dynamic, we use v-bind directive 
  ```
  <a v-bind:href="newItem" target="_blank">Dynamic link</a>
  ```
  * In our current exercise, we can disable the Save button when nothing is entered in the textbox
  ```
  <button class="btn btn-primary" @click="saveItem" v-bind:disabled="newItem.length === 0">Save</button>
  OR
  <button class="btn btn-primary" @click="saveItem" :disabled="newItem.length === 0">Save</button>
  ```
  * We can use v-bind or shorten it to a colon 

* 09 - Dynamic Classes
  * When applying dynamic bindings to attributes, using classes is a special as we can pass in additional data to determine when to apply certain classes and when not to.
  * Toggle between classes between objects and arrays syntax
  ```
    <li v-for="item in items" @click="toggleState()" :class="{strikethrough: item.purchased}">{{ item.label }}</li>
    OR
    <li v-for="item in items" @click="toggleState()" :class="[ item.purchased ? 'strikethrough' : '' ]">{{ item.label }}</li>
  ```
  * If you want to add additional class attributes, you can do so by two ways
  ```
    <li v-for="item in items" @click="toggleState()" :class="[ item.purchased ? 'strikethrough' : 'highlight' ]">{{ item.label }}</li>
    OR
    <li v-for="item in items" @click="toggleState()" class="highlight" :class="{strikethrough: item.purchased}">{{ item.label }}</li>
    OR
    <li v-for="item in items" @click="toggleState()" :class="[ item.purchased ? 'strikethrough' : '', item.label==='coffee' ? 'highlight' : '']">{{ item.label }}</li>
  ```

* 10 - Computed Properties
  * For transformation and calculation, we go with computed properties
  * Computed properties are extremely powerful tools for encapsulating data transformations and manipulations that stay synched with data that they reference
  * Computed property should return a value for Vue to know it
  * Remember: Computed property is for transforming data for our presentation layer. They should not alter or change the existing data.
  * When you need to change data, you will use METHODS
  * When you need to change the presentation of existing data, you will use COMPUTED properties


