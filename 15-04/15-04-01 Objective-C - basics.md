
### Ref

[Obj-C for Java Developer](http://www.slideshare.net/bobmccune/ob-4933190)
[Learn Objective-C](http://cocoadevcentral.com/d/learn_objectivec/)
[Short Intro Obj-C for Java Developer](https://blog.codecentric.de/en/2011/04/short-introduction-to-ios-for-java-developers-objective-c/)

### Basics

- Foundation Framework: defines basic(built-in) Obj-C classes
- ARC: Autometic Reference Counting

Pointers, Memory Mgmt, Processaing & Linking, Namespace(e.g., NS, UI, CA, MK, etc)

Obj-C class definitions are seperated into an **interface** `.h` and an **implementation** `.m`

- `.h`: define the programming inteface, instance variable
- `.m`: define actual implementation code, one or more initializers for object instance

- `-`: instance method
- `+`: class(static) method  

### Class Hierarchy

[class hierarchy](https://cdn.tutsplus.com/mobile/uploads/legacy/45_Learn-Objective-C-3/2.png)

NSObject -> NSString, NSValue, NSArray

### id vs void*

[id vs void*](http://stackoverflow.com/questions/1304176/objective-c-difference-between-id-and-void)

- `id` means a reference to some random Obj-C object of unknown-class
- `void*` mens a reference to some random chunk memory with untyped/unknown contents

### Creating Objects

- `NSObject` defines class method called `alloc`
- `NSObject` defines instance method called `init`

```objective-c
BankAccount *account = [BankAccount alloc]
account = [account init]

// or
BankAccount *account = [[BankAccount alloc] init]
```


### Messages

- Methods are invoked by passing messages. Done indirectly. We never directly invoke methods.


### self and super

```objective-c

-(id)init {
  if (self = [super init]) {
    // do initialization
  }

  return self
}
```

[Why should i call self=\[super init\]](http://stackoverflow.com/questions/2956943/why-should-i-call-self-super-init)

- in initialization, failure is indicated by returning nil
- the super might return alloced object

### @ symbol

[Link](http://stackoverflow.com/questions/25749/what-does-the-symbol-represent-in-objective-c)

```objective-c
NSString *myString = @"MyString\n";
NSString *anotherString = [NSString stringWithFormat:@"%d %@", 1, @"String"];
```
