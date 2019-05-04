# call-apply-bind
手动实现call, apply,bind


//手动实现 call

//call作用是改变this的指向

Function.prototype.newCall = function(obj, ...args){

    obj.new  = this; //在obj上随便定义个属性   this指调用newCall的函数对象
    obj.new(...args);
    delete obj.new;
}



let obj={

    name: 'bob'
}


let fun = {

    name: 'alla',
    say: function(){
        console.log(this.name)
        console.log(arguments)
    }
}


// fun.say()
// fun.say.call(obj,1,2,3)
// fun.say.newCall(obj,1,2,3)



//apply   与call大同小艺


Function.prototype.newApply = function(obj, args){

    obj.new = this;
    obj.new(...args);
    delete obj.new;
}

let obj1={

    name: 'bob'
}

let fun1 = {

    name: 'alla',
    say: function(){
        console.log(this.name);
        console.log(arguments)
    }
}

// fun1.say()
// fun1.say.apply(obj1,[1,2,3])
// fun1.say.newApply(obj1,[1,2,3,4])

//bind  
Function.prototype.newBind = function(obj,...args){

    var _this = this;
    return function(){
        _this.newCall(obj, ...args)
    }
}

let obj2={

    name: 'bob'
}

let fun2s = {

    name: 'alla',
    say: function(){
        console.log(this.name);
        console.log(arguments)
    }
}

let o = fun2s.say.bind(obj2)

o()

let o1 = fun2s.say.newBind(obj2, 1,2,3)

o1()
