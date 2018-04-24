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

#### Utilisation des interfaces
```typescript
export interface IServiceData {
  id: number;
  name: string;
  description?: string;
}

export interface IService {
  get data(): IServiceData;
  set data(pData: IServiceData): void;
}

export class MyService implements IService {
  private _data: Object;

  constructor(pData: IServiceData) {
    this._data = pData;
  }
  
  get data(): IServiceData {
    return this._data;
  }

  set data(pData: IServiceData): void {
    this._merge(pData);
  }

  private _merge(pData: IServiceData): void {
    for (let p in pData) {
      if (this._data[p] !=== undefined && typeof this._data[p] === typeof pData[p]) {
        this._data[p] = pData[p];
      }
    }
  }
}

const serviceData: IServiceData = {
  id: 1,
  name: 'my name'
};

// Usage
const myServiceInstance = new MyService(serviceData);
console.log(myServiceInstance.data.name.length); //-> 7
```

#### Heritage
```typescript
import { MyService, IService, IServiceData } from './my-service.ts';

export interface IServiceDataOriginFrom {
  country: string;
  city: string;
  lang: string;
}

export interface IServiceAdditionalData {
  age?: number;
  address?: string;
  title?: string;
  from?: IServiceDataOriginFrom
}

export interface IServiceExtendedData extends IServiceData, IServiceAdditionalData {
  updatedAt: Date; 
}

export interface IServiceExtended extends IService {
  static extend(pData: IServiceData, toMerge: IServiceAdditionalData): IServiceExtendedData;
}

export class ServiceExtended extends MyService implements IServiceExtended {
  private _data: IServiceExtendedData;

  constructor(pData: IServiceData, toMerge: IServiceAdditionalData) {
    super(ServiceExtended.merge(pData, toMerge));
  }
  
  static merge(pData: IServiceData, toMerge: IServiceAdditionalData): IServiceExtendedData {
    return Object.assign({}, pData, toMerge, {
    	updateAt: new Date()
    });
  }
}

const data: IServiceData = {id: 34, name: 'my name'};
const additionalData: IServiceAdditionalData = {age: 24, title: 'frontend developper'};
const extendedData = new ServiceExtended(data, additionalData);
console.log(extendedData.age, extendedData.updateAt.toString()); //-> 24
```
