# vue-pagination
Vue.JS pagination component, mimics WordPress pagination links, uses Bootstrap formatting.

Uses [FontAwesome](https://fontawesome.com) and [Bootstrap](https://getbootstrap.com/).

![foo](https://raw.githubusercontent.com/zenithtech/vue-pagination/master/menu.gif)


Add the `pagination_data` and `pagination_goto` properties to the app:
```
const main = new Vue({
    el: '#main',
    data() {
        return {
		pagination_data: [],
		pagination_goto: 1
        };
    }
});
```


Initialize your component within your app:
```
Vue.component(
	'pagination',
	require('./components/Pagination.vue').default
);
```

Then include the compomenet in your HTML as such, where `other-component` is where Ajax calls are made:

```
<other-component :pagination_data.sync="pagination_data" :pagination_goto.sync="pagination_goto"></other-component>

<pagination :pagination_data.sync="pagination_data" :pagination_goto.sync="pagination_goto"></pagination>
```

Within `other-component` we watch for when `pagination_goto` changes upon clicking a link in `pagination`, and call the ajax function passing it the page number.

Within `pagination` we watch for when `pagination_data` is received and update the current page number.
