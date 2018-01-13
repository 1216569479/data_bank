# call、apply和bind

## this
this 指向对象，其中包括全局对象、当前对象或者任意对象！
JS 中函数的调用方式有以下几种：
* 作为普通函数（全局对象）
* 作为对象的方法调用（当前对象）
* 作为构造函数调用（任意对象）
* Function.prototype.apply或Function.prototype.call（任意对象）
### 注意： ###
在JavaScript中，call、apply和bind 是Function对象自带的三个方法，这三个方法的主要作用是改变函数中的this指向

### 1.call
call(thisarg,arg1,arg2),其中thisarg表示函数运行时指定的this，返回值是你调用方法的返回值，如果该方法没有返回值，则返回undefined


         function class1() {
            this.name = function () {
                console.log("我是class1内的方法");
            }
        }
        function class2() {
            class1.call(this); //此行代码执行后，
            当前的this指向了class1（也可以说class2继承了class1）   
        }
        var f = new class2();
        f.name();   //调用的是class1内的方法，将class1的name方法交给class2使用 
### 2.apply
apply(thisarg,[arg1,arg2])，应用某一对象的方法，用另一个对象替换当前对象

        function a(arg1, arg2) {
            this.name = function () {
                console.log(arg1, arg2)
            }
        }
        function b() {
            var x = 1, y = 2;
            a.apply(this, [x, y])
        }
        var c = new b();
        c.name()
### 3.bind
 bind()方法会创建一个新函数，称为绑定函数，当调用这个绑定函数时，绑定函数会以创建它时传入 bind()方法的第一个参数作为this,传入bind() 方法的第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。

        var bar = function () {
            console.log(this.x);
        }
        var foo = {
            x: 3
        }
        bar();
        bar.bind(foo)();
        /*或*/
        /*此时bind中的第一个参数为foo对象，最终作为this*/
        var func = bar.bind(foo);
        func();
### 总结
 当你的参数是明确知道数量时用 call ； 而不确定的时候用 apply


