[`CaseIterable`][1] is a new "magical" protocol that can be adopted by `enum` to give runtime access to all of enum's
cases in form of iterable sequence. 

One fun way to use `CaseIterable` is to select random case 
```swift
enum CatBreed: CaseIterable {
    case abyssinian
    case balinese
    case bengal
    case khaoManee
    case maineCoon
    case persian
    case russianBlue
    case siberian
}

print(CatBreed.allCases.randomElement())
```

Other classes can implement `CaseIterable` too if they represent enumerable values. 

[1]: https://developer.apple.com/documentation/swift/caseiterable
