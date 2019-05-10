`Decodable` support in Swift is pretty handy, but it does have its challenges. One is decoding arrays. 
If one value in array fails to decode the array will fail to decode as well. That maybe acceptable or not 
depending on the situation.

If "failure is not an option" there is a simple fix to this issue: declaring array
elements as optional. But that creates it own problem. Now that array elements are optional they have to be unwrapped 
before every use creating code bloat and unnecessary complexity. 

So what can we do to get both: allow for some elements to fail and keep array elements non-optional?

One approach is to create inner struct that have same set of stored properties except arrays having optional elements.
Once inner struct is successfully decoded, array with optional values can be converted to array of non-optionals with
`compactMap`.

```swift
struct SectionModule: Decodable {
    let id: String
    let header: String?
    let subHeader: String?
    let items: [ContentItem]
    let tease: URL?
    let showMore: Bool

    private struct Inner: Decodable {
        let id: String
        let header: String?
        let subHeader: String?
        let items: [ContentItem?]
        let tease: URL?
        let showMore: Bool?
    }

    init(from decoder: Decoder) throws {
        let inner = try Inner(from: decoder)
        id = inner.id
        header = inner.header
        subHeader = inner.subHeader
        items = inner.items.compactMap({ $0 })
        tease = inner.tease
        showMore = inner.showMore ?? false
    }
}
```
