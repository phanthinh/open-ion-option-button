## Requirements

 - AngularJS v1.2.4+
## Used 
open ion-option-button in the ionicframework

Directive example:
## Example
```js
.directive("openIonicOptionButton",function openIonicOptionButton() {
	return {
    restrict: 'EA',
		link: function (scope, element, attrs) {
			
			element.on("click",function(e){
				
				var ITEM_CONTENT_CLASS = 'item-content';
				var ITEM_SLIDING_CLASS = 'item-sliding';
				var ITEM_OPTIONS_CLASS = 'item-options';
				var ITEM_CLASS = attrs.classItem || 'item';
				console.log(ITEM_CLASS);
				// chopo: ojo que lo ideal es poner esto en una directiva porque tiene acceso directo al dom
				console.log('click');
				console.log(e);

				var content, buttons, offsetX, buttonsWidth;

				if (e.target.classList.contains(ITEM_CONTENT_CLASS)) {
					content = e.target;
				} else if (e.target.classList.contains(ITEM_CLASS)) {
					content = e.target.querySelector('.' + ITEM_CONTENT_CLASS);
				} else {
					content = ionic.DomUtil.getParentWithClass(e.target, ITEM_CONTENT_CLASS);
				}

				// If we don't have a content area as one of our children (or ourselves), skip
				if (!content) {
					return;
				}

				// Make sure we aren't animating as we slide
				content.classList.remove(ITEM_SLIDING_CLASS);
				console.log(content);

				offsetX = parseFloat(content.style[ionic.CSS.TRANSFORM].replace('translate3d(', '').split(',')[0]) || 0;

				console.log("offset: " + offsetX);

				// Grab the buttons
				buttons = content.parentNode.querySelector('.' + ITEM_OPTIONS_CLASS);
				if (!buttons) {
					return;
				}
				
				buttons.classList.remove('invisible');
				buttonsWidth = buttons.offsetWidth;
				
				// El item está cerrado
				if(offsetX === 0) {
					content.style[ionic.CSS.TRANSFORM] = "translate3d(-" + buttonsWidth + "px, 0px, 0px)";
				}
				
				// El item está cerrado
				else {
					content.style[ionic.CSS.TRANSFORM] = "translate3d(0px, 0px, 0px)";
				}
				
				console.log("buttonsWidth: " + buttonsWidth);
				
			})
		}
	}
})
