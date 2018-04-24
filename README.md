# typescript-progression
Stratégie de progression du code de Javascript vers Typescript

```typescript
/**
* @description
* Javascript
*/

(function(){
	var MyService = function(pData) {
		var _data = pData;

		return {
			get: function() {
				return _data;
			},
			set: function(pData) {
				for(var p in pData) {
					if(_data[p] !== undefined && typeof _data[p] === typeof pData[p]) {
						_data[p] = pData[p];
					}
				}
			}
		};
	};
})();
```
