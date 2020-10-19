# Function

특정 상황에 사용하려고 별도의 메모리 주소를 할당해서 필요한 코드들을 담아 놓은 것

 ```js
 const foo = function() {
   var name = 'eulsoo'
   var bar = function() {
     var v = 'aaa'
     console.log(v)
   } 
   return bar
 }
 //  foo에서 bar를 리턴하니까 bar()를 실행한 것과 같다.
 foo()()

 ```