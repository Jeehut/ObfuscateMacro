# ObfuscateMacro

Swift macros for string obfuscation in your iOS/macOS applications to protect sensitive string data from binary analysis.

<!-- # Badges -->

[![Github issues](https://img.shields.io/github/issues/p-x9/ObfuscateMacro)](https://github.com/p-x9/ObfuscateMacro/issues)
[![Github forks](https://img.shields.io/github/forks/p-x9/ObfuscateMacro)](https://github.com/p-x9/ObfuscateMacro/network/members)
[![Github stars](https://img.shields.io/github/stars/p-x9/ObfuscateMacro)](https://github.com/p-x9/ObfuscateMacro/stargazers)
[![Github top language](https://img.shields.io/github/languages/top/p-x9/ObfuscateMacro)](https://github.com/p-x9/ObfuscateMacro/)

## Overview

ObfuscateMacro helps protect sensitive strings in your application by obfuscating them at compile-time. When the macro is expanded during compilation, your original strings are transformed into obfuscated data, making it harder for attackers to extract sensitive information through binary analysis.

### Key Features

- Compile-time string obfuscation
- Multiple obfuscation methods
- Dynamic seed generation for each macro execution
- Runtime decoding of obfuscated strings
- No original strings stored in the binary

## Installation

Add ObfuscateMacro as a dependency in your `Package.swift`:

```swift
dependencies: [
    .package(url: "https://github.com/p-x9/ObfuscateMacro.git", from: "1.0.0")
]
```

## How It Works

1. When you use the `#ObfuscatedString` macro, it processes your string at compile-time
2. The macro generates a new random seed each time it's executed
3. Your string is obfuscated using the selected method(s) and stored in the binary in its obfuscated form
4. At runtime, when your code needs the string, it's automatically decoded back to its original form

This approach ensures that only obfuscated data exists in your compiled binary, making it much harder for attackers to extract sensitive strings through binary analysis.

## Usage

### Basic Usage

First, import the macro:
```swift
import ObfuscateMacro
```

Then use the macro to obfuscate your strings:
```swift
let text = #ObfuscatedString("hello")
```

### Obfuscation Methods

The following methods are available for string obfuscation:

- **bit shift**: Applies bit shifting operations
- **bit XOR**: Uses XOR operations
- **base64**: Applies base64 encoding with additional obfuscation
- **AES**: Uses AES encryption
- **random**: Randomly selects from the above methods

#### Specify Method

You can explicitly choose an obfuscation method:
```swift
let string = #ObfuscatedString("Hello", method: .bitXOR)
```

#### Random Method Selection

Use random selection from all available methods:
```swift
let string = #ObfuscatedString("Hello", method: .randomAll)
```

Or specify which methods to choose from:
```swift
let string = #ObfuscatedString("Hello", method: .random([.bitXOR, .AES]))
```

### Enhanced Security

For stronger protection, you can apply multiple layers of obfuscation:

```swift
#ObfuscatedString(
    "hello",
    repetitions: 5
)
```

This will apply the obfuscation process 5 times, making it even harder to reverse-engineer the original string.

## Best Practices

1. Use this macro for sensitive strings like:
   - API keys
   - Secret tokens
   - Internal URLs
   - Encryption keys
2. Consider using different obfuscation methods for different types of strings
3. Use repetitive obfuscation for highly sensitive data
4. Remember that while obfuscation adds protection, it's not a replacement for proper security measures

## License

ObfuscateMacro is released under the MIT License. See [LICENSE](./LICENSE)
