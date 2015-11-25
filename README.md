# SwiftCBOR [![unlicense](https://img.shields.io/badge/un-license-green.svg?style=flat)](http://unlicense.org) [![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)

A [CBOR (RFC 7049 Concise Binary Object Representation)](http://cbor.io) decoder and (TODO) encoder in Swift.

- No `Foundation` dependency! Ready for the cross-platform future of Swift.
- Configured as a [universal iOS / OS X framework](https://colemancda.github.io/programming/2015/02/11/universal-ios-osx-framework/).
- Maps can only contain string keys, like JSON. It's [possible](https://stackoverflow.com/questions/24119624/how-to-create-dictionary-that-can-hold-anything-in-key-or-all-the-possible-type) to support keys of any type in Swift, but that's kinda awkward and I don't need it.
- Negative 64-bit integers are decoded as `LargeNegativeInt(i: UInt)`, where the actual number is `-1 - i`, because CBOR's negative integers can be larger than 64-bit signed integers.
- If you want to decode from a stream, implement the `CBORInputStream` protocol on your stream and create the decoder like this: `CBORDecoder(stream: yourStream)`.
- [ObjectMapper](https://github.com/Hearst-DD/ObjectMapper) is recommended for, well, mapping to objects.
- [cbor.me](http://cbor.me) is recommended for viewing your CBOR-encoded data.

## Installation

Use [Carthage](https://github.com/Carthage/Carthage).

```
github "myfreeweb/SwiftCBOR"
```

## Usage

```swift
import SwiftCBOR

let decoded = try! CBORDecoder(input: [0x9f, 0x18, 255, 0x9b, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 2, 0x18, 1, 0x79, 0x00, 3, 0x41, 0x42, 0x43, 0x79, 0x00, 3, 0x41, 0x42, 0x43, 0xff]).decodeItem() as! [Any]
print(decoded)
// [255, [1, "ABC"], "ABC"]
```

## Contributing

By participating in this project you agree to follow the [Contributor Code of Conduct](http://contributor-covenant.org/version/1/2/0/).

[The list of contributors is available on GitHub](https://github.com/myfreeweb/SwiftCBOR/graphs/contributors).

## License

This is free and unencumbered software released into the public domain.  
For more information, please refer to the `UNLICENSE` file or [unlicense.org](http://unlicense.org).
