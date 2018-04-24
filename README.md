# typescript-progression
Stratégie de progression du code de Javascript vers Typescript

#### Exemple javascript service avec propriété "privée"
```typescript
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

#### Renforcement du Javascript par typage des variables, propriétés, arguments/retours des methodes
```typescript
(function(){
  var MyService = function(pData: Object): Object {
    var _data: Object = pData;
    
    return {
      get: function(): Object {
        return _data;
      },
      set: function(pData: Object): void {
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

#### Utilisation de classe au lieu de fonction à prototype
```typescript
class MyService {
  private _data: Object;

  constructor(pData: Object) {
    this._data = pData;
  }
  
  get data(): Object {
    return this._data;
  }

  set data(pData: Object): void {
    this._merge(pData);
  }

  private _merge(pData: Object): void {
    for (let p in pData) {
      if (this._data[p] !=== undefined && typeof this._data[p] === typeof pData[p]) {
        this._data[p] = pData[p];
      }
    }
  }
}
```
