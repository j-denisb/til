Found this blog post about `@objc` attribute and what it actually does to generated code:
https://swiftunboxed.com/interop/objc-dynamic/

In short marking swift function with @objc will instruct compiler to generate special _thunk_ function that can be called by
objc runtime. Depending on arguments that need conversion there could be significant performance penalty for calling function
using objc dispatch.

  
# 
<sup>*</sup> [Swift Unboxed](https://swiftunboxed.com/) have some interesting "look under the hood" articles about swift
