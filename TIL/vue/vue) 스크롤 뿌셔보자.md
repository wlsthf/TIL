# vue) 스크롤 뿌셔보자



```vue
<ul ref="scrollContainer" @scroll="handleScroll">
	<li v-for="item in obj.items">
		<p>{{item.seq}}</p>                  
	</li>     
</ul>

<a href="#" class="btn_top" v-show="showScroll" @click.prevent="moveTop()">top</a>
```



```javascript
module.exports = {
    name: '콤포논토이름',
    data: function() {
        return {
            showScroll: false,
        }    
    },
    methods: {
    	moveTop: function() {
            let elem = this.$refs.scrollContainer;
            elem.scrollTop = 0;
        },
        handleScroll: function(event) {
            let elem = this.$refs.scrollContainer;
            if(elem.scrollTop > 0) {
                this.showScroll = true;
            } else {
                this.showScroll = false;
            }
        },
    },
    mixins: [믹스인!],
}
```

