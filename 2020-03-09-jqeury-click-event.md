### single-click + double-click + ctrl-click in same element with jquery

```
function bindClickDbClickCtrlClick($element, clickAction, doubleClickAction) {
		var timer = 0, delay = 200, prevent = false;
		$element
			.on("click", function(e) {
				if ( !e.metaKey && e.ctrlKey ) {
					e.metaKey = e.ctrlKey;  // for non-mac
				}
				if(e.metaKey) {  // for ctrl-click
					clickAction(e);
					return;
				}
				timer = setTimeout(function() {
					if (prevent == false) {
						clickAction(e);  // for single-click without ctrl
					}
					prevent = false;
				}, delay);
			})
			.on("dblclick", function(e) {
				clearTimeout(timer);
				prevent = true;
				doubleClickAction(e);  // for double-click
			});
	}
```
