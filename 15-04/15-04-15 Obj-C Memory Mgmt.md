## Objective-C Memory Mgmt 2

[SO: Strong, Retrain, Weak, Assign ](http://stackoverflow.com/questions/8927727/objective-c-arc-strong-vs-retain-and-weak-vs-assign)

### strong, weak, assign

- 오브젝트를 *retain* 하려면 `strong` 사용
- *retain* 하지 않고, 오브젝트를 가리킬때만 `weak` 사용
- *primitives* 프로퍼티를 위해서는 `assign` 사용. `weak` 와 동일하나, `nil` 이 되지 않음.

### copy

오브젝트를 *shallow copy* 하기 위해 사용할 것.

*immutable* 프로퍼티에 `copy` 를 지정하는건 좋은 습관인데, 왜냐하면

- *mutable* 오브젝트가 *immutable* 프로퍼티에 넘어오면 `copy`
- *immutable* 이면 `retain` 하기 때문

```objective-c
// e.g
@property (nonatomic, copy) NSString *apiToken
```

### Factory Method with ARC

```objective-c
+ (instancetype)rakeWithApiToken: (NSString *)apiToken {
    return [[self alloc] initWithApiToken:apiToken];
}
```

*ARC* 면 자동으로 리턴 코드에서 *autorelease* 

### instanceType vs id

[SO: instantceType vs id](http://stackoverflow.com/questions/8972221/would-it-be-beneficial-to-begin-using-instancetype-instead-of-id)

> There definitely is a benefit. When you use 'id', you get essentially no type checking at all. With instancetype, the compiler and IDE know what type of thing is being returned, and can check your code better and autocomplete better.
