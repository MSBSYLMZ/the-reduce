# The Reduce
Here is the implementation of almost (excluding the ones returns iterable) every Array prototype methos with the reduce method. 
#### Note: This is just representation of the capabilities of the reduce method. In most cases built in methods are much optimized and performed. 
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
Array.prototype.customConcat  =  function (...args) {
	return [...args].reduce((acc, cur) =>  {
		if (Array.isArray(cur)) {
		return [...acc, ...cur];
		}
		acc.push(cur);
		return  acc;
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






