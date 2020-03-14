# lazy_function
惰性函数  
1、现有一个函数，用来获取某时刻的时间，以后调用该函数，都返回第一次调用时的时间  
```var timeStamp=null;
        function getTimeStamp(){
            if(timeStamp){
                return timeStamp;
            }
            timeStamp=new Date().getTime();
            return timeStamp;
        }```
这种写法的缺点：  
1）在函数内引用了外部的timeStamp变量，污染外部的变量  
2）每次执行getTimeStamp，都有进行一次判断  
2、使用惰性函数  
```
var getTimeStamp3=function(){
            var timeStamp=new Date().getTime();
            getTimeStamp3=function(){
                return timeStamp;
            }
            return timeStamp;
        }
```   
内部函数改变自身的机制  
在函数内部改变自身  
例如：  
```
var fn=function(){
    if(...){
        fn=...
    }else if(...){
        fn=...
    }else{
        fn=...
    }
    return ...
}
```
第一次执行的时候不仅返回值，而且在函数内部改变了自身，下次执行的时候就执行这个被改变的新函数了（虽然它的函数名并没有改变）  