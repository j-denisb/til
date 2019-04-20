In my project [SwiftNotifications][1] I needed to get struct/class name in a protocol extension. Searching the internet
produces many results telling you to use [`String(describing:)`][3]. It works well, but a string you get back
just contains a name of the class or struct without a module name. In my case, I needed to get a fully qualified name to avoid
potential name collision. After some digging (it was surprisingly hard), I found [`String(reflecting:)`][2]. It 
returns just what I need - a fully qualified class or struct name.

:exclamation: Another thing the internet sugested is [`NSStringFromClass`][4]. One problem though: if you pass it struct type,
it will crash. This is both expected, since ObjC doesn't support structs, and unexpected. _Discitur lectio_: mixing objc
runtime calls with Swift should be done with caution.

<sup>*</sup> [Discitur lectio][5]

[1]: https://github.com/nbcnews/SwiftNotifications
[2]: https://developer.apple.com/documentation/swift/string/1541282-init
[3]: https://developer.apple.com/documentation/swift/string/3129029-init
[4]: https://developer.apple.com/documentation/foundation/1395143-nsstringfromclass
[5]: https://translate.google.com/?sl=la&tl=en&text=Discitur+lectio
