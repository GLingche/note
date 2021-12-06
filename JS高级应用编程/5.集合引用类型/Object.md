## 这种模式非常适合函数有大量可选参数的情况
### 但参数过多就显得笨拙了，最好方式是对必选参数使用命名参数，再通过一个对象字面量来封装多个对象
```js
{
    function displayInfo(args){
        let output = "";
        if(typeof  args.name == "string"){
            output += "Name: " + args.name + "\n";
        }

        if(typeof args.age == "number"){
            output +="Age:" + args.age + "\n";
        }

        alert(output);
    }

    dispalyInfo({
      name:"xxx",
      age:"20"  
    });

    displayInfo({
        name:"yyyy"
    });

}
```

