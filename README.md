Swift InFlux
===========
The community is creating some incredible analyses and writing about Swift. What I keep asking myself whenever learning and reading about Swift is: how likely is this to change soon? 

This document is an attempt to gather the Swift features that are still in flux and likely to change.

### Contributing
To contribute just fork this project and add a section below (don't forget to update the Table of Contents!).

### Table of Contents

* [Character](#character)
* [Numerical data type conversion](#numerical-data-type-conversion-eg-cgfloat-and-swift-doubleswift-float)
* [Optionals for values conforming to the LogicValue protocol](#optionals-for-values-conforming-to-the-logicvalue-protocol-eg-bool)
* [Access control](#access-control)
* [C++ support](#c-support)
* [Better error handling](#better-error-handling-features-possibly-exceptions)
* [Usage of @-sign in front of keywords](#usage-of--sign-in-front-of-keywords)
* [Absence of math.h macros](#absence-of-mathh-macros)
* [Unowned references breaking in Beta 2 and 3](#unowned-references-breaking-in-beta-2-and-3)
* [Set of legal operator characters](#set-of-legal-operator-characters)
* [Mutable optional value types](#mutable-optional-value-types)
* [Recursive nested functions](#recursive-nested-functions)
* [Structs with both @lazy and non-lazy properties crashes compiler](#structs-with-both-lazy-and-non-lazy-properties-crashes-compiler)
* [C union support is coming](#c-union-support-is-coming)

___

* [Changed in Beta 3](#changed-in-beta-3)
  * [Array value semantics](#array-value-semantics)
  * [Array and Dictionary type declaration syntax](#array-and-dictionary-type-declaration-syntax)
  * [Range operators](#range-operators)

---

### Character

>Note that Character is still evolving and will settle down by the final release of 1.0. One of the reasons that we use double quote syntax to initialize Characters is that they are expected to be able to hold full grapheme clusters, which are composed of multiple code points. This will roll out in a later beta.
>
>-- Chris Lattner

Sources: https://devforums.apple.com/message/997759#997759 http://oleb.net/blog/2014/07/swift-strings/

### Numerical data type conversion, e.g. CGFloat and Swift Double/Swift Float

>What is happening here is that CGFloat is a typealias for either Float or Double depending on whether you're building for 32 or 64-bits.  This is exactly how Objective-C works, but is problematic in Swift because Swift doesn't allow implicit conversions.
> 
>We're aware of this problem and consider it to be serious: we are evaluating several different solutions right now and will roll one out in a later beta.  As you notice, you can cope with this today by casting to Double.  This is inelegant but effective :-)
>
>-- Chris Lattner

Sources: https://devforums.apple.com/message/998222#998222

### Optionals for values conforming to the LogicValue protocol (e.g. Bool)

Optional Bools in a boolean context are confusing.

```swift
var foo: Bool? = false
// This will print bar
if foo {
    println("bar")
}
```

>This problem exists with any optional of something that conforms to the LogicValue protocol (e.g. nested optionals, optional of bool, etc).  We consider it serious issue that needs to be fixed for 1.0 and have some ideas, but haven't settled on a solution yet.
>
>-- Chris Lattner

Sources: https://devforums.apple.com/thread/234399?tstart=0

### Access control

>We don't usually promise anything for the future, but in this case we are making an exception. Swift will have access control mechanisms.
>
>-- Greg Parker

>Access control (public/private/etc) is coming in a later beta, this is mentioned in the Xcode release notes.
>
>-- Chris Lattner

>The design is based around inline access-decorators (e.g. marking something public), not by adding headers back.  Please wait for it to come out in a later beta for details (yes, it is coming).
>
>-- Chris Lattner

Sources: https://devforums.apple.com/thread/228324?start=50&tstart=0 https://devforums.apple.com/message/996725#996725 https://devforums.apple.com/message/970220#970220 https://devforums.apple.com/message/1000948#1000948

### C++ support

>This is another obviously desirable feature, it is just a lot of work and didn't make it in 1.0 either.
>
>-- Chris Lattner

Sources: https://devforums.apple.com/thread/228324?start=50&tstart=0

### Better error handling features (possibly exceptions)

>We're aware of the opportunity and also desire better error handling features in Swift, but they didn't make it in time for 1.0.
>
>-- Chris Lattner

Sources: https://devforums.apple.com/thread/228324?start=50&tstart=0

### Usage of @-sign in front of keywords

>This is something we're continuing to evaluate, expect @ signs to change in subsequent betas.
>
>-- Chris Lattner

Sources: https://devforums.apple.com/thread/228324?start=25&tstart=0

### Absence of math.h macros

>This is a known problem, it will be fixed in later betas.
>
>-- Chris Lattner

Soruces: https://devforums.apple.com/message/989902#989902

### Unowned References [Breaking](http://openradar.appspot.com/radar?id=5300501415460864) in Beta 2 and 3

> This should be fixed in Beta 3.
>
>-- Chris Lattner

Still doesn't work in beta 3: see [#5](https://github.com/ksm/SwiftInFlux/pull/5)

Sources: https://devforums.apple.com/message/997278#997278

### Set of legal operator characters

> The set of characters is in flux, but yes, most unicode symbol characters in the BMP that are classified as 'symbol' and 'math' are available as operator characters.
>
>-- Joe Groff

> It's not documented yet, but the set of allowed operator characters includes 'math' and 'symbol' characters in the Unicode BMP, and operator characters can be augmented with combining characters. The full set of supported characters will be documented in one of the following seeds.
>
>-- Joe Groff

Sources: https://devforums.apple.com/thread/231723?tstart=450 https://devforums.apple.com/message/1000934#1000934

### Mutable optional value types

> The issue here is that optional forcing and binding operators (postfix ! and ?) return an immutable rvalue, even when the operand is a mutable lvalue.  This means that you cannot perform mutating operations on the result, which is why optional arrays, dictionaries and other value types are pretty useless right now.
> Unfortunately there isn't a great solution or workaround right now: one approach is to wrap the value in a class and use the optional on the class wrapper:
```
class StringArray {
    var elts : String[]
}
var myArray: StringArray?
```
> We consider this a significant problem and are investigating various solutions to incorporate in a later Beta.
>
>-- Chris Lattner

Sources: https://devforums.apple.com/message/998882#998882

### Recursive nested functions

> This is due to a known bug with recursive nested functions.  You can fix this by pulling them out to the top level.
>
>-- Chris Lattner

Sources: https://devforums.apple.com/message/997536#997536

### Structs with both @lazy and non-lazy properties crashes compiler

structs with a @lazy property followed by a non-lazy property crashes
the compiler.

> This is fixed, but didn't make it into Beta 3. Stay tuned for a later Beta,
>
> -- Chris Lattner

Source: https://devforums.apple.com/message/1000950#1000950

### C union support is coming

> We'll have at least partial support for importing unions in a future seed.
> 
>-- Joe Groff

Source: https://devforums.apple.com/message/1002630#1002630
___

## Changed in Beta 3

### Array value semantics
Since Beta 3, Array has full value semantics to match Dictionary, String and other value types.

>Array semantics were in flux at the time of Beta 1, and have been revised to provide full value semantics like Dictionary and String.  This will be available in later betas.
>
>-- Chris Lattner

Sources: https://devforums.apple.com/thread/228695?start=75&tstart=

### Array and Dictionary type declaration syntax
Before Beta 3, the shorthand for an Array type was `Type[]`, and Dictionary types were written `Dictionary<KeyType, ValueType>`. Array type shorthand was changed to `[Type]` and Dictionaries types now have a shorthand syntax `[KeyType: ValueType]` (e.g. `[String: Bool]`)

### Range operators
The half-closed range operator was changed from `..` to `..<`.

> We considered this carefully.  As you can see from this thread, small syntactic issues like this are polarizing, subject to personal preferences, and have no one right answer.  See also http://en.wikipedia.org/wiki/Bikeshed
>  
> For what it's worth, this approach is precendented in the groovy language.  It optimizes for readability and clarity: you're unlikely to mistake one operator for the other when skimming code, and new people coming to Swift are unlikely to assume that ..< is an inclusive range operator (like most assumed when they saw "0..5")
> 
> --Chris Lattner
> 
> I'd really like it if there was only a single range operator, but that isn't possible (AFAIK):
> 
> - You need to have a half-open range operator to be able to represent an empty range.
> - You need an inclusive range operator to represent finite enumerated sequences when you want to include the last element (e.g. enums, but also integers that you want to include the largest integer value in)..
> 
> --Chris Lattner

Sources: https://devforums.apple.com/message/1000100#1000100, https://devforums.apple.com/message/999669#999669
