Instance of empty `struct` has 0 memory footprint, but it is assigned an actual address.
That results in an instance of empty struct having the exact same memory address as instance that follows it.
```swift
struct EmptyStruct {
}

func wow() {
  var foo = EmptyStruct()
  var baz = "I am a struct too"
  
  withUnsafePointer(to: foo) {
    print(String(format: "%p", $0))
  }
  withUnsafePointer(to: baz) {
    print(String(format: "%p", $0))
  }
}

```
