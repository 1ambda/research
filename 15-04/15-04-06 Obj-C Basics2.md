### @property vs @synthesize

[SO Answer](http://stackoverflow.com/questions/9544370/objective-c-property-and-synthesize-logic)

- Unlike java/c++, in obj-c you can't access variable of class. You could only call It's methods
- `@synthesize` `topSpeed = _topSpeed` means You want an variable named `_topSpeed` and has Accessors named `topSpeed` and `setTopSpeed`.

### Pass multiple parameters

```objective-c
- (NSMutableArray*)getBusStops:(NSString*)busStop forTime:(NSSTimeInterval*)timeInterval;
```

### Alloc String

```objective-c
NSString *string1 = @"This is string 1.";
NSString *string2 = [[NSString alloc]initWithString:@"This is string 2."];
```

### Memory Mgmt

**Reference Counting**

- Objects start with reference count of 1
- Increased with `retain`
- Decreased with `release`, `autorelease`
- When count equals 0, runtime invokes `dealloc`

implicitly `retain` any object you create using methods starting with `alloc`, `new`, or contains `copy`

If you've retained it, you must `release` it

### Strong, Weak, Assign

[SO Answer](http://stackoverflow.com/questions/8927727/objective-c-arc-strong-vs-retain-and-weak-vs-assign)

- use `strong` to retain objects (synonym)

> Increases the retain count of an object by 1. Takes ownership of an object.

- use `weak` if you only want a pointer to the object without retaining it. useful for avoid retain cycles(ie. delegates). It will automatically nil out the pointer when the object is released
- use `assign` for primitives. exactly like weak except it doesn't nil out the object when released
- use `copy` for creating a shallow copy of the object. good practice to always set immutable properties to copy.

> copy –  Makes a copy of an object, and returns it with retain count of 1. If you copy an object, you own the copy. This applies to any method that contains the word copy where “copy” refers to the object being returned.

### Protocol

Java's Interface done Objective-C style

```objective-c
@protocol NSCoding

- (void)encodeWithCoder:(NSCoder *) aCoder;

@end


@interface Person : NSObject <NSCoding> {
  ....
}
```


### Category

Extending Class
