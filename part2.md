1. 实现一个flatten函数，将一个嵌套多层的数组 array（数组） (嵌套可以是任何层数)转换为只有一层的数组，数组中元素仅基本类型的元素或数组，不存在循环引用的情况。 Ex:flatten([1,[2],[3,[[4]]]])=>[1,2,3,4]


```
var arr = [3, [2, -4, [5, 7]], -3, ['aa', [['bb']]]]
var arr2 = flatten2(arr)
console.log(arr2)

/*方法1*/
function flatten(arr){
  var newArr = []
  function _flat(arr){
    arr.forEach(val=>{
      if(Array.isArray(val)){
        _flat(val)
      }else{
        newArr.push(val)
      }
    })    
  }
  _flat(arr)
  return newArr
}

/*方法2*/

function flatten2(arr){
  return arr.reduce(function(initArr, currentArr){
    return initArr.concat(Array.isArray(currentArr)?flatten2(currentArr):currentArr)
  }, [])
}
```
2. 实现一个reduce函数，作用和原生的reduce类似。

reduce(list, iteratee, [memo])，memo是reduce函数的初始值，会被每一次成功调用iteratee函数的返回值所取代 。这个迭代传递4个参数：memo,value 和 迭代的index和最后一个引用的整个 list。如果没有memo传递给reduce的初始调用，iteratee不会被列表中的第一个元素调用。第一个元素将取代memo参数传递给列表中下一个元素调用的iteratee函数。

Ex：var sum = reduce([1,2,3],function(memo,num){return memo+num;},0)

```
  function iterator(list, iteratee, memo, index, length) {
      for (; index >= 0 && index < length; index++) {
        memo = iteratee(memo, list[index], index, list);
      }
      return memo;
  }
  
  function reduce(list,iteratee,memo){
    
    var index=0,length=list.length;
    
    if(arguments.length<3){
      memo=list[index];
      index=1;
    }
    return iterator(list, iteratee, memo, index, length);
  }

  var sum = reduce([1, 2, 3], function(memo, num){ return memo + num; }, 0);

```
3. 纯CSS实现，点击按钮显示一个modal，再点击关闭按钮，关闭modal。

```
//html
<body>
  <div>
    <label for="checkbox">
        展示
    </label>
    <input id="checkbox" type="checkbox"></input>
  <div class="modal">
    <label class="close" for="checkbox">关闭</label>
  </div>
  </div>
</body>
//css
input[type="checkbox"]{
  display:none;
}
label{
  line-height:20px;
  padding:2px 5px;
  background:#aaa;
  font-size:14px;
  color:white;
  box-shadow: 0 0 2px #888888;
}
label:active{
   box-shadow:none;
}
.modal{
  display:none;
  position:fixed;
  top:0;
  bottom:0;
  left:0;
  right:0;
  background:rgba(0,0,0,.3);
}
#checkbox:checked~.modal{
  display:flex;
}
.close{
  margin:auto;
}

```
4. 用纯CSS实现以下效果：一组li标签鼠标悬停于哪一个标签其前的标签及本身都显示背景色

```
//html
<body>
  <ul>
     <li></li>
     <li></li>
     <li></li>
     <li></li>
     <li></li>
  </ul>
</body>
//css 方法1
*{
  padding:0;
  margin:0;
}

li{
  list-style:none;
  height:20px;
  width:20px;
  border-radius:50%;
  margin:10px;
  border:1px currentColor solid;
  /* float: right; */
}
li:hover,li:hover~li{
  background:gray;
}
ul{
  display:flex;
  direction:rtl;
  width:fit-content;
} 
/* ul{
  float: left;
} */
//css 方法2
*{
  padding:0;
  margin:0;
}

li{
  list-style:none;
  height:20px;
  width:20px;
  border-radius:50%;
  margin:10px;
  border:1px currentColor solid;
  float: right;
}
li:hover,li:hover~li{
  background:gray;
}
ul{
  float: left;
}


```
5. 实现一个map函数，模拟原生的map函数，map(list, iteratee)。

通过对list里的每个元素调用转换函数(iteratee迭代器)生成一个与之相对应的数组。iteratee传递三个参数：value，然后是迭代 index。

ex：map([1,2,3],function(num){return num*3;})=>[3,6,9]

```
function map(list,iteratee) {
    var results=[];
    for(vsr index=0;index<list.length;index++){
        results[index] = iteratee(obj[index],index,list);
    }
    return results;
};
```
