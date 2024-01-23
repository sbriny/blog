title:《重新认识 Vue Router》

|- router-link
|- router-view

***view ,component and template***

Use a custom component `router-link` to create link, this allow Vue Router to change the URL without reloading the page, handle URL generation as well as its encoding.（在不重新加载页面的情况下更改和生成URL。）
component `router-view` will display the component that corresponds to the url. You can put it anywhere to adapt it to your layout.（展示与路径相符的组建，并可调整在代码中位置以适用布局。）
To access the router or the route inside the setup function, call the useRouter or useRoute functions. （调用useRouter或useRoute函数以使用router或内置函数。）
Throughout the docs, we will often use the `router` instance. Keep in mind that `this.$router` is exactly the same as directly using the router instance created through `createRouter`. The reason we use `this.$router` is because we don't want to import thte router in every single component that nedds to manipulate routing.（router实例贯穿整个文档，使用$router简化在每个需要操作路由的组件中的引入）