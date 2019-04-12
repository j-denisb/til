Based on my experience with C++ I am used to think that casting one type to another doesn't have any runtime cost.
Basicaly you just tell compliler to interpret given object as different type during compilation. But as I learned today
this is not true for Swift.

While doing some performance tuning I "discovered" that casing from `[String: Any]` to `[AnyHashable: Any]`
does have substantial runtime cost. That is happening because `AnyHashable` is not a protocol or
base class, but rather a `struct` that can be created from `String` or many other types. When casing from `String`
to `AnyHashable` Swift compliler uses its special knowledge to insert runtime conversion calls into generated code.
This effort by Swift compliler makes it easy to convert dictionaries, but it hides the fact that expensive copy
operation takes place from the user.

Another related issue is that if you have dictionary with `AnyHashable` keys, then accessing values with `String`s
or other primitive types will have a runtime penalty:
```swift
let dictionary: [AnyHashable: Any] = [ ... ]

let foo = dictionary["foo"] // compiler will turn it into dictionary[AnyHashable("foo")]

```

Casting from `[AnyHashable: Any]` to `[String: Any]` also caries similar performance penalty. Although that is less
unexpected since conversion from `AnyHashable` to `String` is not guaranteed.

One implication is that if conversion is unavoidable you have to decide if you'd rather pay the cost 
up front or on every access.

#### References

- [AnyHashable](https://developer.apple.com/documentation/swift/anyhashable)
- [How are Int and String accepted as AnyHashable?](https://stackoverflow.com/questions/42021207/how-are-int-and-string-accepted-as-anyhashable)
