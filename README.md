# The Reduce
Here is the implementation of almost (excluding the ones that returns iterable) every Array prototype methos with the reduce method. 
#### Note: This is just representation of the capabilities of the reduce method. In most cases built in methods are much optimized and performed. 
##### Note: In the representation sometimes built-in methods sometimes custom methods has been used. Since we are using function expressions not declarations. The functions won't be hoisted. So if we try to use it before expression. It will throw an error. If you change the order you may use the custom methods instead of the build-in ones. 
---
#### Array.prototype.at()
```javascript
Array.prototype.customAt  =  function (index) {
	if (index  <  0) index  =  this.length  +  index;
	if (index  >  this.length) return  undefined;
	return  this.reduce((acc, cur, ind) =>  {
		if (index  ===  ind) return  cur;
		return  acc;
	}, undefined);
};
```
---
#### Array.prototype.concat()
```javascript
Array.prototype.customConcat = function (...args) {
	return [...args].reduce((acc, cur) => {
		if (Array.isArray(cur)) {
			return [...acc, ...cur];
		}
		return [...acc,cur]
	}, this);
};
```
---
#### Array.prototype.copyWithin()
```javascript
Array.prototype.customCopyWithin  =  function (target, start, end  =  this.length) {
	let  count  =  0;
	target  =  target  <  0  ?  this.length  +  target  :  target;
	start  =  start  <  0  ?  this.length  +  start  :  start;
	end  =  end  <  0  ?  this.length  +  end  :  end;
	return  this.reduce((acc, cur, index) =>  {
		if (index  >=  target  &&  start  +  count  <  end) {
		acc.push(this[start  +  count]);
		count++;
		return  acc;
		}
		acc.push(cur);
		return  acc;
	}, []);
};
```
---
#### Array.prototype.every()
```javascript
Array.prototype.customEvery  =  function (callback) {
	return  this.reduce((acc, cur) =>  {
		if (!callback(cur)) return  false;
		return  acc;
	}, true);
};
```
---
#### Array.prototype.fill()
```javascript
Array.prototype.customFill  =  function (value, start, end  =  this.length) {
	start  =  start  <  0  ?  this.length  +  start  :  start;
	end  =  end  <  0  ?  this.length  +  end  :  end;
	return  this.reduce((acc, cur, index) =>  {
		if (index  >=  start  &&  index  <  end) {
		acc.push(value);
		return  acc;
	}
	acc.push(cur);
	return  acc;
}, []);
```
---
#### Array.prototype.filter()
```javascript
Array.prototype.customFilter  =  function (callback) {
	return  this.reduce((acc, cur) =>  {
		if (callback(cur)) {
		acc.push(cur);
	}
	return  acc;
	}, []);
};
```
---
#### Array.prototype.find()
```javascript
Array.prototype.customFind  =  function (callback) {
	return  this.reduce((acc, cur) =>  {
		if (acc  ===  undefined  &&  callback(cur)) {
			return  cur;
		}
	return  acc;
	}, undefined);
};
```
---
#### Array.prototype.findIndex()
```javascript
Array.prototype.customFindIndex  =  function (callback) {
	return  this.reduce((acc, cur, index) =>  {
		if (acc  ===  -1  &&  callback(cur)) return  index;
			return  acc;
	}, -1);
};
```
---
#### Array.prototype.findLast()
```javascript
Array.prototype.customFindLast  =  function (callback) {
	return  this.reduce((acc, cur) =>  {
		if (callback(cur)) {
			return  cur;
		}
	return  acc;
	}, -1);
};
```
---
#### Array.prototype.flat()
```javascript
Array.prototype.customFlat  =  function (depth) {
	return  this.reduce((acc, cur, index) =>  {
		if (Array.isArray(cur) &&  depth  >  0) {
			const  result  =  cur.customFlat(depth  -  1);
			const  concatenated  =  acc.customConcat(result);
			return  concatenated;
		}
	acc.push(cur);
	return  acc;
	}, []);
};
```
---
#### Array.prototype.flat()
```javascript
Array.prototype.customFlat  =  function (depth) {
	return  this.reduce((acc, cur, index) =>  {
		if (Array.isArray(cur) &&  depth  >  0) {
			const  result  =  cur.customFlat(depth  -  1);
			const  concatenated  =  acc.customConcat(result);
			return  concatenated;
		}
	acc.push(cur);
	return  acc;
	}, []);
};
```
---
#### Array.prototype.customFlatMap()
```javascript
Array.prototype.customFlatMap  =  function (callback) {
return  this.reduce((acc, cur, index) =>  {
	if (Array.isArray(cur)) {
		let  result  =  callback(cur);
		if (typeof  result[Symbol.iterator] ===  "function") {
			acc.push(...result);
		} else {
			acc.push(result);
		}
		return  acc;
		}
	acc.push(callback(cur));
	return  acc;
	}, []);
};
```
---
#### Array.prototype.customForEach()
```javascript
Array.prototype.customForEach  =  function (callback) {
	return  this.reduce((acc, cur) =>  {
		callback(cur);
	}, undefined);
};
```
---
#### Array.prototype.customIncludes()
```javascript
Array.prototype.customIncludes = function (search) {
	return this.reduce((acc, cur) => {
		if (cur === search) {
			return true;
		}
		return acc;
	}, false);
};
```
---
#### Array.prototype.customIndexOf()
```javascript
Array.prototype.customIndexOf = function (search) {
	return this.reduce((acc, cur, index) => {
		if (acc === -1 && cur === search) {
			return index;
		}
		return acc;
	}, -1);
};
```
---
#### Array.prototype.customJoin()
```javascript
Array.prototype.customJoin = function (seperator) {
	return this.reduce((acc, cur) => {
		return acc + seperator + cur;
	}, "");
};
```
---
#### Array.prototype.customLastIndexOf()
```javascript
Array.prototype.customLastIndexOf = function (search) {
	return this.reduce((acc, cur, index) => {
		if (cur === search) {
			return index;
		}
		return acc;
	}, -1);
};
```
---
#### Array.prototype.customMap()
```javascript
Array.prototype.customMap = function (callback) {
	return this.reduce((acc, cur, index) => {
		const result = callback(cur, index);
		acc.push(result);
		return acc;
	}, []);
};
```
---
#### Array.prototype.customPush()
```javascript
Array.prototype.customPush = function (...values) {
	const arrLength = this.length;
	values.reduce((acc, cur, index) => {
		acc[index + arrLength] = cur;
		return acc;
	}, this);
	return arrLength + values.length;
};
```
---
#### Array.prototype.customReverse()
```javascript
Array.prototype.customReverse = function () {
	if (this.length === 1) return [...this];
	return this.reduce((acc, cur) => {
		acc.unshift(cur);
		return acc;
	}, []);
};
```
---
#### Array.prototype.customShift()
```javascript
Array.prototype.customShift = function () {
	const newArray = [...this];
	const deleted = newArray[0];
	newArray.reduce((acc, cur, index) => {
		if (index === 0) {
			delete acc[index];
			if(newArray[index + 1]){
				acc[index] = newArray[index + 1];
				return acc;
			}
			acc.length = 0;
			return acc;
		} else if (index === newArray.length - 1) {
			acc.length = newArray.length - 1;
			return acc;
		}
		acc[index] = newArray[index + 1];
		return acc;
	}, this);
	return deleted;
};
```
---
#### Array.prototype.customSlice()
```javascript
Array.prototype.customSlice = function (start, end = this.lenth) {
	return reduce((acc, cur, index) => {
		if (index >= start && index < end) {
			acc.push(cur);
		}
		return acc;
	}, []);
};
```
---
#### Array.prototype.customSome()
```javascript
Array.prototype.customSome = function (callback) {
	this.reduce((acc, cur) => {
		if (callback(cur)) {
			return true;
		}
		return acc;
	}, false);
};
```
---
#### Array.prototype.customSort()
```javascript
Array.prototype.customSort = function (callback) {
	return this.reduce((acc, cur) => {
		if (acc.length === 0) return [cur];
		let allow = true;
		let addLater = null;
		const result = acc.reduce((a, c) => {
			if (callback(cur, c) >= 0 && allow) {
				if (addLater) {
					a.push(addLater, c);
					allow = false;
				} else {
					a.push(cur, c);
					allow = false;
				}
				return a;
			} else if (allow) {
				addLater = cur;
			}
			a.push(c);
			return a;
		}, []);
		if (allow && addLater !== null) {
			result.push(addLater);
		}
		return result;
	}, []);
};
```
---
#### Array.prototype.customSplice()
```javascript
Array.prototype.customSplice = function (start, deleteCount, ...replacers) {
	const copyArr = [...this];
	const deleted = [];
	const copyDeleteCount = deleteCount;
	const offsetElements = [];
	let offset = 0;
	copyArr.reduce((acc, cur, index) => {
		if (index >= start) {
			if (deleteCount > 0) {
				if (replacers[index - start]) {
					acc[index] = replacers[index - start];
					deleteCount--;
					return acc;
				}
				deleted.customPush(acc[index]);
				delete acc[index];
				offset++;
				deleteCount--;
				return acc;
			} else if (replacers[index - start]) {
				offsetElements.customPush(acc[index]);
				offset--;
				acc[index] = replacers[index - start];
				return acc;
			}
		}
		if (offset) {
			if (offsetElements.length > 0) {
				offsetElements.customPush(acc[index]);
				acc[index] = offsetElements[0];
				offsetElements.customShift();
				if (index === copyArr.length - 1) {
					acc.customPush(...offsetElements);
				}
				return acc;
			}
			acc[index - offset] = acc[index];
			if (index === copyArr.length - 1) acc.length = copyArr.length - copyDeleteCount + replacers.length;
			return acc;
		}
		acc[index] = cur;
		return acc;
	}, this);
	return deleted;
};
```
---
#### Array.prototype.customToString()
```javascript
Array.prototype.customToString = function () {
	if(this.length === 0) return "";
	return this.reduce((acc, cur, index) => {
		return acc.toString() + "," + cur.toString();
	});
};
```
---
#### Array.prototype.customUnshift()
```javascript
Array.prototype.customUnshift = function (...elements) {
	const offsetElements = [];
	this.reduce((acc, cur, index) => {
		offsetElements.customPush(cur);
		if(elements[index]){
			acc[index] = elements[index];
		}else{
			acc[index] = offsetElements[0];
			offsetElements.customShift();
		}
		return acc;
	},this);

	this.customPush(...offsetElements);
	return this.length;
};
```






