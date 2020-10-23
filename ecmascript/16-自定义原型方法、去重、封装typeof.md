# 自定义原型方法、去重、封装typeof

## 封装typeof

```js
function myTypeof(val) {
            var type = typeof(val);
            var toStr = Object.prototype.toString();
            var res = {
                '[object Object]': object,
                '[object Array]': array,
                '[object String]': string,
                '[object Number]': number,
                '[object Boolean]': boolean
            }
            if (val === null) {
                return 'null'
            } else if (type === 'object') {
                var ret = toStr.call(val);
                return res[ret]
            } else {
                return type;
            }
        }
```

## 数组去重

```js
var arr = [0, 0, 1, 2, 2, 1, 4, 2, 4, 'a', 'b', 'a']

        Array.prototype.unique = function() {
            var obj = {};
            var newArr = []
            for (let i = 0; i < this.length; i++) {
                if (!obj.hasOwnProperty(this[i])) {
                    obj[this[i]] = this[i];
                    newArr.push(this[i])
                };

            }
            return newArr
        }
```

## 字符串去重

```js
var str = 'fnrnfrnfhkjddmdee';
        String.prototype.unique = function() {
            var obj = {},
                newStr = '';
            for (let i = 0; i < this.length; i++) {
                if (!obj.hasOwnProperty(this[i])) {
                    obj[this[i]] = this[i];
                    newStr += this[i]
                }
            }
            return newStr
        }
        console.log(str.unique());
```

## 获取字符串中第一位只有一个的字符

```js
var str = 'hruhfrauhfuhbfrufcuhgrhf';

        function test(str) {
            var obj = {};
            for (let i = 0; i < str.length; i++) {
                if (obj[str[i]]) {
                    obj[str[i]]++;
                } else {
                    obj[str[i]] = 1;
                }
            }
            for (var key in obj) {
                if (obj[key] == 1) {
                    return key;
                }
            }
        }

        console.log(test(str));
```

