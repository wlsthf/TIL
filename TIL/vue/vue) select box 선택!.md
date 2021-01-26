# vue) select box 선택!





```vue
<select title="골라골라 셀렉트" v-on:change="fn($event)">
	<option value="">Kibon</option>
    <option v-for="(val, key) in obj" 
		v-if="val != 0" 
		:value="key">
		{{key}}
	</option>
</select>
```





```javascript
methods: {
    fn: function(event) {
		console.log(event.target.value)
	},
}

```

