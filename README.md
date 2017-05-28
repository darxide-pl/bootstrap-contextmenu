bootstrap-contextmenu

Extra leightweight plugin (4kB) for building complex context menus in bootstrap3

Visit https://darxide-pl.github.io/bootstrap-contextmenu/ for examples and documentation

Quick start: 

1. Include bootstrap3 and jquery
```
<script src="https://code.jquery.com/jquery-2.2.4.min.js"
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
<link rel="stylesheet" type="text/css" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
```
2. Include plugin script and css:
```
<script src="bootstrap-contextmenu.js"></script>
<link rel="stylesheet" type="text/css" href="bootstrap-contextmenu.css">	
```

3. Create context menus.... Examples: 


# Simple example
```
<div class="list-group menu1">
	<div class="list-group-item">Right click on me</div>
	<div class="list-group-item">Right click on me</div>		
</div>

<script type="text/javascript">
const menu = Object.create(contextMenu)
menu.init('.menu1 .list-group-item' , [
		{
			type : 'header',
			text : 'header in context menu',
		}, 
		{
			type : 'item', 
			text : 'hello'
		}, 
		{
			type : 'item', 
			text : 'world'
		},
		{
			type : 'divider'
		}, 
		{
			type : 'item', 
			text : 'other item under divider'
		}
	])
</script>	
```

# Complex example with callbacks and some submenus 

```
<script type="text/javascript">
const menu2 = Object.create(contextMenu)
menu2.init('.menu2 .list-group-item' , [
		{
			type : 'item', 
			text : function(e) {
				let element = $(e.currentTarget)
				return 'This item has data-id="'+element.data('id')+'"'
			},
		}, 
		{
			type : 'item', 
			text : function(e) {
				let element = $(e.currentTarget) 
				if(element.data('id') == 1) {
					return 'I am active!'
				} 

				return 'I am not active'
			}, 
			href : 'http://www.google.pl',
			attr : {
				class : function(e) {
					let element = $(e.currentTarget) 
					if(element.data('id') == 1) {
						return 'active'
					}
				}
			}
		}, 
		{
			type : 'item',
			text : 'this item should be visible only if target element has data-id = 2',
			display : function(e) {
				let element = $(e.currentTarget)
				if(element.data('id') == 2) {
					return true
				}
				return false
			}
		}, 
		{
			type : 'submenu', 
			text : 'submenu example',
			items : [
				{
					type : 'item', 
					text : 'submenu item 1',
				}, 
				{
					type : 'item', 
					text : function() {
						return 'random number '+ Math.ceil(Math.random()*1000)
					}
				}, 
				{
					type : 'submenu', 
					text : 'next level submenu',
					items : [
						{
							type : 'item', 
							text : 'subsubmenu item 1',
						}, 
						{
							type : 'item', 
							text : function() {
								return 'random number '+ Math.ceil(Math.random()*1000)
							}
						}, 
					]
				}
			]
		}
	])
</script>
```
For live examples, explanations and docs visit gh-page: https://darxide-pl.github.io/bootstrap-contextmenu/
