# vue-pagination
Vue.JS pagination component which mimics Wordpress pagination links

![foo](https://raw.githubusercontent.com/zenithtech/vue-pagination/master/menu.gif)


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
