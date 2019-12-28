# Vue-Data-Driven-Pagination
This package provides a Data Driven Pagination Component For Vue.js applications. It abstracts away the pagination logic while providing you flexibility to display your list however you need to on the DOM.

## Installation

```
npm install --save data-driven-vue-paginator
```

## Usage

1. Once you've imported the component you can use it in your vue.js template by adding the following:
   - A ```list``` prop containing the array of items to paginate.
   - A ```perPage``` prop representing the number of items you need to display.
2. In your component you will need to define two templates:
   - The default template which takes the array of items to be displayed.
   - The pagination links template which contains pagination links predefined in the package. You can also define yours in the template.


### Sample Usage

``` html
  <v-paginate :list="books" perPage="2">
    <template v-slot="paginate">
      <ul>
        <li>{{ book.name }}</li>
      </ul>
    </template>
    <!-- table-responsive -->
    <template v-slot:paginationLinks></template>
  </v-paginate>
```

``` js
import vForm from "data-driven-vue-paginator";

export default {
  components: { vForm },
  data: () => ({ 
    books: [
      { name: 'harry potter', author: 'shakespare' },
      { name: 'things fall apart', author: 'chinua achebe' },
      { name: 'Half of a yellow sun', author: 'chinua achebe' }
    ] 
  }),
};
```
