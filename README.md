# Typespring
TypeSpring is an Express.js and Typescript based application framework that allows you to develop annotation based restful APIs like in SpringBoot 

### **Define component for dependency injection**
In Typespring framework, you can easily define a component using @Component() decorator. This decorator creates an instance for dependency injection.
```javascript
@Component()
export default class ClassB{

}
```


### **Field Injection**
For now, Typespring only supports field injection using Autowired decorator. In the future, construction based injection will be supported.
```javascript
@Component()
export default class ClassA{
    
    public test():String{
        return "test"
    }

}
```

```javascript
@Component()
export default class ClassB{
    @Autowired()
    private classA:ClassA; // Instance of ClassA is injected.
}
```

### ** Initializing A Web Server**
Typespring framework allows you to create web api and handle web requests easily. 
The first step is creating a main file that has a main class as shown below.

```javascript
@TypespringApplication()
export class MainApplication{
    public main(){
        TypespringInitiliazer.run()
    }
}
```
After building and running main file, TypespringInitiliazer.run function will initialize a web server immeditely. 
But for invoking components, we need to import them in the main file. It doesnt matter where you are importing Components. The main purpose is invoking @Component decorators of classes.

```javascript
const Components = {
    ClassA,
    ClassB,
    ClassC
}
export {Components}
```

```javascript
@TypespringApplication()
export class MainApplication{
    public main(){
        TypespringInitiliazer.run(Components)
    }
}
```

### ** Web Request and Response Handling
```javascript
@Component()
export default class ClassC{

    @Autowired()
    private classA:ClassA

    @GetMapping("/api/test1")
    public test():any{
        return ResponseEntity.status(200).body("test")
    }

    @PostMapping("/api/test2")
    public test2(){
        let data = this.classA.test()
        return ResponseEntity.status(HttpStatus.OK).body(data)
    }
    
}
```





