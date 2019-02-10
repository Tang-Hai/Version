# Version ![badge-platforms][] ![badge-languages][] [![badge-ci][]][travis] [![badge-jazzy][]][docs] [![badge-codecov][]][codecov]

A µ-framework for representing, comparing, encoding and utilizing
[semantic versions][semver], eg. `1.2.3` or `2.0.0-beta`.

This is `Version.swift` from the [Swift Package Manager], with some minor
adjustments:

1. More compact `Codable` implementation †
2. Implements `LosslessStringConvertible` ‡
3. Not a massive-single-source-file (MSSF)
4. [Online documentation][docs]
5. Extensions for `Bundle` and `ProcessInfo`
6. Removal of the potentially fatal `ExpressibleByStringLiteral` conformance
7. A “tolerant” initializer for user input like `10.0` or `3`
8. Idiomatic implementations for `Range<Version>`

We have automatic monitoring for changes at Apple’s repo to alert us if we
should need merge any fixes.

> † [Semantic versions][semver] can be losslessly expressed as strings; thus we
> do so.

> ‡ Like `Int` we can losslessly store a semantic version from a valid string,
> so we conform to the same protocol.

[semver]: https://semver.org
[docs]: https://mxcl.github.io/Version/Structs/Version.html
[badge-platforms]: https://img.shields.io/badge/platforms-macOS%20%7C%20Linux%20%7C%20iOS%20%7C%20tvOS%20%7C%20watchOS-lightgrey.svg
[badge-languages]: https://img.shields.io/badge/swift-4.2%20%7C%205.0-orange.svg
[badge-jazzy]: https://raw.githubusercontent.com/mxcl/Version/gh-pages/badge.svg?sanitize=true
[badge-codecov]: https://codecov.io/gh/mxcl/Version/branch/master/graph/badge.svg
[badge-ci]: https://travis-ci.com/mxcl/Version.svg
[travis]: https://travis-ci.com/mxcl/Version
[codecov]: https://codecov.io/gh/mxcl/Version
[Swift Package Manager]: https://github.com/apple/swift-package-manager/blob/master/Sources/SPMUtility/Version.swift

# Support mxcl

Hey there, I’m Max Howell. I’m a prolific producer of open source software and
probably you already use some of it (for example, I created [`brew`]). I work
full-time on open source and it’s hard; currently *I earn less than minimum
wage*. Please help me continue my work, I appreciate it 🙏🏻

<a href="https://www.patreon.com/mxcl">
	<img src="https://c5.patreon.com/external/logo/become_a_patron_button@2x.png" width="160">
</a>

[Other ways to say thanks](http://mxcl.github.io/donate/).

[`brew`]: https://brew.sh

# Installation

SwiftPM:

```swift
package.append(.package(url: "https://github.com/mxcl/Version.git", from: "1.0.0"))
```

Carthage:

> Waiting on: [@Carthage#1945](https://github.com/Carthage/Carthage/pull/1945).

## Ranges

Ranges work as you expect, but there are caveats for prerelease identifiers,
here are the rules:

>  `1.0.0..<2.0.0` does not include eg. `2.0.0-alpha`

This is probably what you expected. However:

> `1.0.0..<2.0.0` also does not include eg. `1.5.0-alpha`

However:

> `1.0.0..<2.0.0-beta` **does** include eg. `2.0.0-alpha`

This is how the majority of Semantic Version libraries work.
