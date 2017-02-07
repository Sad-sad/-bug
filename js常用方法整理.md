**1.原生编写一个方法，通过className获取元素**
``` js
        例：<div class="list"></div>
            var $={
            		byId:function(id){
                      return typeof id==='string'document.getElementsById(id):id;
                    },
                    byClass:function(cls,parent){
                      parent=parent?this.byId(parent):document;
                      var eles=document.getElementsByTagName("*");
                      var arr=[];
                      for(var i=0,len=eles.length;i<len;i++){
                       if(eles[i].className.match(new RegExp('(^| )'+cls+'( |$)'))){  //匹配空格list  list  list空格
                       arr.push(eles[i])                 当正则表达式中包含变量时，必须使用new   RegExp  不能用//定界符 
                      }
                 }
                 return arr;
            }
       }
       console.log($.byClass("list"))
```
**2.对一个数组进行去除重复项**
``` javascript
    例：var arr=[1,2,4,5,6,3,46,3,2,88];
           function isInarray(val,arr){    //检测值是否存在于数组中
                for(var i in arr){
                    if(arr[i]==val){
                      return true
                     }
            }
            return false
       }
           function removeItem(arr){
                var newArr=[];
                for(var i in arr){
                     if(!isInarray(arr[i],newArr)){
                      newArr.push(arr[i])     //push（）向数组追加一个元素 放在最后
                 }
            }
            return newArr
       }
           console.log(removeItem(arr))
```
**3.执行顺序**
``` js
    function global（）{
            var  a=b=55;    //从右往左执行
    }
    global()  
    console.log(a)    //报错  a is not define
    console.log(b)   //55
    例：var glo="aa";
    function fun(){
        console.log(glo);     //在函数内，先找出所有的变量，这时的glo变量被声明但并未赋值，所以为undefined
        var glo="bb";
        console.log(glo)
    }
    fun()
        执行结果：第一个：undefined   第二个  bb   所有的变量声明当被悬置到函数的顶部了
        原因：代码执行两个阶段：1.变量，函数声明，参数创建。先解析再执行
                                            2.代码执行，函数表达式和不合格的标识符被创建
                                            
```
                                      
**4.求一个数组中重复的值放在一个新的数组中**
``` js
       var arr=[1,2,,5,4,2,5,4,7,9,10];
       function isInarray(val,arr){
            var num=0;
            for(var j=0;j<arr.length;j++){
            if(arr[j]==val){
                  num+=1;
             }
            }
            return num
           }
           function getItem(arr){
                var newArr=[];
            for(var i=0;i<arr.length;i++){
                 if(isInarray(arr[i],arr)>1 && isInarray(arr[i],newArr)===0){
                  newArr.push(arr[i])
             }
            }
            return newArr
           }
               console.log(getItem(arr))
``` 
**5.将字符串“border-top-color”转换成“BorderTopColor”**
``` js
        方法一：function fn(str){
                        var arr=str.split("-"),newStr="";
                        console.log(arr)
                        for(var i=0;i<arr.length;i++){
                             newStr+=arr[i].charAt(0).toUpperCase()+arr[i].substr(1);
                        }
                        console.log(newStr)
                       }
                       fn(str)
    方法二：var str="border-bottom-color"        //正则表达式匹配
                   function strFn(str){
                        str=str.replace(/\b\w+\b/g,function(s){
                             return s.charAt(0).toUpperCase()+s.substr(1);
                        }).replace(/-/g,"")
                        console.log(str)
                           }
                       strFn(str)
```
**6、给数字加千分符**
``` js
          例      var num="1234567890.23";
               var reg=/(\d{1,3})(?=(\d{3})+($|\.))/g;
               num=num.replace(reg,"$1,")
               console.log(num)
```
**7、查找字符串中出现最多的字符和个数**    
``` js
    例：function getMaxChar(str){
                var strs=str.split(""),
                 obj={},
                 maxStr="",
                 count=0;
                for(var i=0;i<strs.length;i++){
                     var item=strs[i],c=0;                              c=(obj[item]||0)+1
                     if(obj[item]){                                          c>count&&　（maxstr=item,c=count）
                          c=obj[item]+1;                                  obj[item]=c
                     }else{
                      c=1;
                     }
                     if(c>count){
                          maxStr=item;
                          count=c;
                         }
                         obj[item]=c;
                        }     
                        var num=[];
                        for(var m in obj){
                             num.push(obj[item])
                        }
                        var maxNum=Math.max.apply(null,num);
                        for(var n in obj){
                             if(obj[n]==maxNum){
                                      maxStr=n
                                }
                            }
                                return obj
                                //return ("出现最多的是"+maxStr+",出现了"+c+"次")
                       }
   console.log(getMaxChar(str))
```
**8.实现b数组拷贝a数组，实现每个元素的拷贝**
``` js
    var a=[1,"aa",3];
    方法一：  var  b=new Array();  for(var i=0;i<3;i++){b.push(a[i])}
    方法二：  var b=[].concat(a)
    方法三：  var b=a.slice(0,a.length)
``` 
**9.函数实现参数后的后缀名 如abc.jpg 返回 .jpg**
``` js
        function getSuf(name){
             var dotLast=name.lastIndexOf(".");
         if(dotLast==-1){
              return "文件名格式不正确"
         }else{
              return name.substr(dotLast)
         }
        }
        console.log(getSuf("a.jpg"))
```        
**10.求平均数**
``` js
        function fun（）{
            var sum=0；
            for（var i=0；i<arguments.length;i++）{
                sum+=arguments[i]
        }
        return  sum/arguments.length
    }
```  
**11.js实现循环1-100的奇数**
``` js
        function  getNumber(){
            for(var i=0;i<100;i++){
                if(i%2==1){console.log(i)}      //i%2==0   偶数
            }
    }
```
**12.实现字符串反转**
``` js
    方法一：function(str){
            var newStr=""
            for(var i=str.length;i>0;i--){
                newStr+=str.substring(i-1,i)            //substring（）截取字符串，下标如果是n，则截取n-1位
            }
            return newStr;
    }
    方法二：function(str){
               var newstr="";
                for(var i=str.length-1;i>=0;i--){
                       newstr+=str.charAt(i)
                }
                return  newstr;
            }
    方法三：var arr=str.split("");
                   var newStr=arr.reverse().join().replace(/,/g,"")
```
**13.实现数组反转**

```	 js
	        var arr=[1,2,3,5]
	              function setArray(arr){
	                     var newArr=[];
	                     /*for(var i=arr.length-1;i>=0;i--){     //方法一
	                          newArr.push(arr[i])
	                     }*/
	                     for(var i=0;i<arr.length;i++){       //方法二
	                          newArr.unshift(arr[i])
	                     }
	                     return newArr
	                }
	                console.log(setArray(arr))    
	                
```
**14.求素数**

``` js
        function getItem(begin,end){
             var arr=[];
             for(var i = begin; i < end ;i++){
                  if(isPrimeNum(i)){
                       arr.push(i)
                    }
               }
                 return arr
            }
        function isPrimeNum(num){
                 for(var i=2;i<num;i++){
                          if(num%i==0){
                       return false
                      }
                 }
                 return true
            }
            console.log(getItem(1,100))
                       
```
**15.为元素绑定多个事件（同时支持IE和火狐）**

``` js
        var  addHandler=function(element,type,handler){
                if(element.addEventListener){
                       element.addEventLister(type,handler,false);       //removeEventLister(type,handler,false)  删除事件
                }else if(element.attachEvent){
                        element.attachEvent("on"+type,handler);        //detachEvent("on"+type,handler)  删除事件
                }else{
                        element["on"+tyoe]=handler
                }
        }
       
```
**16.求二维数组所有数的和**
``` js
        function sum(arr){
            var total=0;
            for(var i=0;i<arr.length;i++){
                for(var j=0;j<arr[i].length;j++){
                    total+=arr[i][j]
                }
            }
            return  total
        }
```
**17.js实现随机选取10--100之间的10个数字，存入一个数组**

``` js
        function  select(start,end){
            var o=end-start+1;
            return  Math.floor(Math.randow()*o+start)
        }
        var arr=[];
        for(var i=0;i<10;i++){
            arr.push(select(10,100))
        }
```
**18.位数组扩展indexof、remove、removeat方法**

``` js
        var oldArrayIndexof=Array.indexof;
        Array.prototype.indexof=function(obj){
            if(!oldArrayIndexof){
                for(var i=0,len=this.length;i<len;i++){
                    if(this[i]==obj){return i}
                }
                 return  -1
            }else{
                 return oldArrayIndexof(obj)
            }
        }
        Array.prototype.remove=function(idx){
            if(isNaN(idx) || idx>this.length){
                return  false
            }
            for(var i=idx;i<this.length;i--){
                this[i]=this[i+1]
            }
            this.length-=1;
        }
        Array.prototype.removeAt=function(index){
            this.splice(index,1)             //splice(m,n) 用于删除数组中索引从m开始的n个字符
        }                                                     // 返回值：仍然是一个数组，存放了被数组删除的值
```
        
**19.实现兼容的getElementByClassName()方法        **
    
``` js
var $ = {
        getEleByClass: function( cls, parent, tag ){
            var parent = parent || document;
            var tag = tag || "*";
            if( parent.getElementsByClassName ){
                return parent.getElementsByClassName( cls );
            } else {
        var aClass = [];
        var reg = new RegExp( "(^| )" + cls + "( |$)" );
        var aEle = this.getEleByTag( tag, parent );
            for( var i = 0, len = aEle.length; i < len; i++ ){
                reg.test( aEle[i].className ) && aClass.push( aEle[i] );
            }
        return aClass;
        }
    },
        getEleByTag: function( ele, obj ){
            return ( obj || document ).getElementsByTagName( ele );
        },
        hasClass: function( ele, cls ){
            return ele.className.match( new RegExp( "(^|\\s)" + cls + "(\\s|$)" ));
        },
        addClass: function( ele, cls ){
            if( !$.hasClass( ele, cls ) ){
            ele.className += " " + cls;
            }
        },
        removeClass: function( ele, cls ){
            if( $.hasClass( ele, cls ) ){
                var reg = new RegExp( "(^|\\s)" + cls + "(\\s|$)" );
                ele.className = ele.className.replace( reg, " " );
            }
        }
    };
```
**20,实现isArray  inArray功能**
      
``` js
  function isArray(obj){
            return  Object.prototype.toString.call(obj)=='[object Array]'
        }
        function inArray(val,arr){
            arr=isArray(arr)?arr:arr.split("|");
            if(type val=='string' || type val=='number'){
                for(var i in arr){
                    if(arr[i])==val{
                        return true
                    }
                }
            }
                return false
        }
```
**21.实现点击li打印对应的索引值   **

``` js
方法一：for(var i=0, len = lis.length; i<len; i++){
            lis[i].index = i;
            lis[i].onclick = function(){
                alert( this.index );
            }
        }
方法二：
for(var i=0, len = lis.length; i<len; i++){
            (function(i){
                lis[i].onclick = function(){
                 alert( lis[i] );
            }
            })(i);
        }
方法三：
for(var i=0, len = lis.length; i<len; i++){
            lis[i].setAttribute("data-num",i);
        }
        for(var i=0, len = lis.length; i<len; i++){
            lis[i].onclick = function(){
                alert( this.getAttribute("data-num") );
            }
        }
```
**21.给定一个数组实现反转，要求原地实现    **
``` js
 function reversal( arr ){
        for (var i = 0; i < arr.length / 2; i++) {
            var temp = arr[i];
            arr[i] = arr[arr.length - i - 1];
            arr[arr.length - i - 1] = temp;
        }
    }
    var array = [1,"abc",3,4,5];
    reversal(array);
    alert(array);
```
**22.数组冒泡排序**

``` js
    function sortArr(arr){
        for(var j=0;j<arr.length;j++){
            for(var i=arr.length-1;i>j;i--){
                if(arr[i]<arr[i-1]){
                    var temp=arr[i];
                    arr[i]=arr[i-1];
                    arr[i-1]=temp;
                }
            }
        }
        return arr;
    }
```
**23.实现兼容的getElementsByClassName（）方法**
   
```js
 var $={
        getEleByClass:function(cls,parent,tag){
            var parent=parent||document;
            var tag=tag||"*";
            if(parent.getElementsByClassName){
                return parent.getElementsByClassName(cls)
            }else{
                var aClass=[];
                var reg=new RegExp("(^| )"+cls+"( |$)");
                var aEle=this.getEleByTag(tag,parent);
                for(var i=0,len=aEle.length;i<len;i++){
                    reg.test(aEle[i].className)&& aClass.push(aEle[i])
                }
                return aClass
            }
        },
        getEleByTag:function(ele,obj){
            return (obj||document).getElementsByTagName(ele);
        },
        hasClass:function(ele,cls){
            return ele.className.match(new RegExp("(^|\\s)"+cls+"(\\s|$)"))
        },
        addClass:function(ele,cls){
            if(!$.hasClass(ele,cls)){
                ele.className+=""+cls;
            }
        },
        removeClass:function(ele,cls){
            if($.hasClass(ele,cls)){
                var reg=new RegExp("(^|\\s)"+cls+"(\\s|$)");
                ele.className=ele.className.replace(reg,"")
            }
        }
    }    
```


