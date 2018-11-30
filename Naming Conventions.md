# Laravel


* Class names MUST be declared in StudlyCaps.
* Method names MUST be declared in camelCase().
* Class constants MUST be declared in all upper case with underscore 

````
<?php
namespace Vendor\Model;

class StudlyCaps
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
    
    function camelCase() {
        // function body
    }
}


namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleMethod($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
````

# Vue

Most of this is taken from https://vuejs.org/v2/style-guide/

## Components

File names are
* PascalCase
* Multi Word except for root App components. This prevents conflicts with existing and future HTML elements, since all HTML elements are a single word.

````
MyComponent.vue
````

From [HTML case sensitivity workaround #2308](https://github.com/vuejs/vue/issues/2308) 

So as we all know, HTML is case insensitive. myProp="123" gets parsed as myprop="123" and this has led to the caveat in Vue.js where you have to use my-prop="123" to refer to a prop declared in JavaScript as myProp. This bites beginners quite often.

In addition, we also need to apply the same mapping to custom components - e.g. when you define a component:

````
import MyComponent from './MyComponent'

export default {
  components: {
    MyComponent // es2015 shorhand
  }
}
````
You must use <my-component> in the template instead of <MyComponent>.

Ohter Notes:

* https://vuejs.org/v2/guide/components-props.html
* https://vuejs.org/v2/style-guide/

### Single File Component Layout

````
<template>
    
</template>

<script>
    import SsGridColumnHeader from "./SsGridColumnHeader";
    import SsGridPagination from "./SsGridPagination";
    import SsGridPaginationLocation from "./SsPaginationLocation";
    
    export default {
        name: "test",
        components: {SsGridColumnHeader, SsGridPaginationLocation, SsGridPagination},
        model: {
            prop: 'value',
            event: 'input'
        },
        props: {
            checked: Boolean
        },
        mounted: function () {

        },
        updated: function () {          // Not used much
            this.$nextTick(function () {
                // Code that will run only after the
                // entire view has been re-rendered
             )
        },
        data () {
            return {
                foo: 'bar'
            }
        },
        watch: {
            current_page: function () {
                this.resetPageNumbers();
            },
        },
        computed: {
            next_page_number() {
                return this.current_page < this.last_page ? this.current_page + 1 : null;
            },
        },
        methods: {
            goToNew: function () {
                window.location.href = '/organization/create';
            },
        }
    }
</script>

<style scoped>  // bad

</style>
````

### Data

Component data must be a function.

````
// In a .vue file
export default {
  data () {
    return {
      foo: 'bar'
    }
  }
}
````

### How to handle static properties
NOT TESTED - I di not know if this works with what I have created.

From https://itnext.io/how-not-to-vue-18f16fe620b5

There are no reason to pass static properties to data and especially in computed. When you do it, Vue makes these properties reactive but it’s unnecessary.

````
export default {
    phone: 799999999999,
    city: 'kcmo'
}

componet.$options.phone,
component.$options.city
````


### Prop definitions

Prop names should always use camelCase during declaration, but kebab-case in templates and JSX.

````
props: {
  greetingText: String
}


<WelcomeMessage greeting-text="hi"/>
````


Should be as detailed as possible

````
props: {
  status: String
}
// Even better!
props: {
  status: {
    type: String,
    required: true,
    validator: function (value) {
      return [
        'syncing',
        'synced',
        'version-conflict',
        'error'
      ].indexOf(value) !== -1
    }
  }
}
````

Validation, see https://monterail.github.io/vuelidate/


Elements with multiple attributes should span multiple lines, with one attribute per line.

````
<img
  src="https://vuejs.org/images/logo.png"
  alt="Vue Logo"
>
<MyComponent
  foo="a"
  bar="b"
  baz="c"
/>
````

### Computed Properties

Complex computed properties should be split into as many simpler properties as possible.

````
computed: {
  basePrice: function () {
    return this.manufactureCost / (1 - this.profitMargin)
  },
  discount: function () {
    return this.basePrice * (this.discountPercent || 0)
  },
  finalPrice: function () {
    return this.basePrice - this.discount
  }
}
````


### Implicit parent-child communication USE WITH CAUTION
Props and events should be preferred for parent-child component communication, instead of this.$parent or mutating props.

````
Vue.component('TodoItem', {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  template: `
    <input
      :value="todo.text"
      @input="$emit('input', $event.target.value)"
    >
  `
})
Vue.component('TodoItem', {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  template: `
    <span>
      {{ todo.text }}
      <button @click="$emit('delete')">
        X
      </button>
    </span>
  `
})
````

### Style

Element selectors should be avoided with scoped.

## Template

### Keyed v-for
Always use key with v-for.

````
<ul>
  <li
    v-for="todo in todos"
    :key="todo.id"
  >
    {{ todo.text }}
  </li>
</ul>
````

### v-if/v-else-if/v-else without key USE WITH CAUTION
It’s usually best to use key with v-if + v-else, if they are the same element type (e.g. both <div> elements).

By default, Vue updates the DOM as efficiently as possible. That means when switching between elements of the same type, it simply patches the existing element, rather than removing it and adding a new one in its place. This can have unintended side effects if these elements should not actually be considered the same.

````
<div
  v-if="error"
  key="search-status"
>
  Error: {{ error }}
</div>
<div
  v-else
  key="search-results"
>
  {{ results }}
</div>
````

Different DOM types

````
<p v-if="error">
  Error: {{ error }}
</p>
<div v-else>
  {{ results }}
</div>
````


### Non-empty HTML attribute
Values should always be inside quotes (single or double, whichever is not used in JS).

````
<input type="text">
<AppSidebar :style="{ width: sidebarWidth + 'px' }">
````

### Directive shorthands 
(: for v-bind: and @ for v-on:) should be used always or never.

````
<input
  v-bind:value="newTodoText"
  v-bind:placeholder="newTodoInstructions"
>

<input
  v-on:input="onInput"
  v-on:focus="onFocus"
>
````


# [How can we teach good naming practice for students learning Java?](https://cseducators.stackexchange.com/questions/4594/how-can-we-teach-good-naming-practice-for-students-learning-java)
From Stack Exchange:

The following is from the above:

### What works
I have found that the following question is a useful overriding guide for most of my students:

"If you were not someone who had just spent the last 15 hours looking over this code in detail, what are the odds that you could figure out what it was doing at a quick glance?"

### Naming norms
This is the best tool that I use, and these work for all of my students. There are a few direct practices that I ask for in all submitted code:

* With regard to booleans, what do we know if this variable is true? Create a name based on the true condition. (e.g. if this variable will be true whenever the foo is inside the bar, we would name the variable fooInBar)
* With regards to accessor methods, what information is being returning? Simply name this information. (totalTrials(), unusedElements(), nextItem(), etc.)
* With regards to mutators, what command (verb) is being issued? Use this verb, possibly with an attached noun. (increment(), consume(Item i), fixVertex(), etc.)
* Single letter variable names should be used only for throwaway counters and such. (e.g. for(int k = 0; k < items.length(); k++))
* For other variables, we enter into broader territory, and things can get trickier. Which brings us to...

### Miscellaneous variables
Unintuitively, I have had mixed luck with the question,

"what does this variable actually represent?"

This is the question that I ask myself while I code, and it works for many students, but for students who really struggle to come up with good names, the question does not seem to grant much insight.

This doesn't mean that I don't use the question, but it has become a last resort. Students who present poorly named variables often seem unable to cleanly articulate what a particular variable is accomplishing.

If I'm honest, the fact that this question rarely helps strugglers makes little sense to me (and is rather disheartening), but I have come to accept it as a fact. Going back to my intuition that strong writers create clean code, there could be some language difficulty going on here, but that is only a hunch.

For such strugglers, I might help them by having them describe the variable in broad terms, and writing what they say. I will then sit and progressively distill what they have written with them until we arrive at a good name together. Unfortunately, this practice is time intensive and does not scale well, but it works, and I haven't found any better solutions for my strugglers.
