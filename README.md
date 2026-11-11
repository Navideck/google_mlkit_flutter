# google_mlkit_flutter (SwiftPM pin patch)

A trimmed copy of the two packages from
[flutter-ml/google_ml_kit_flutter](https://github.com/flutter-ml/google_ml_kit_flutter)
at 1.0.1, with exactly one change each:

```diff
-            exact: "9.0.2"
+            exact: "9.0.3"
```

in `ios/*/Package.swift`, i.e. the pinned `google-mlkit-swiftpm` version.

Nothing else is modified. Everything here is MIT licensed by
[flutter-ml.dev](https://flutter-ml.dev); see each package's `LICENSE`.

## Why

`google-mlkit-swiftpm` 9.0.2 requires `gtm-session-fetcher` `3.5.0..<4.0.0`,
while `firebase-ios-sdk` 13.1.1 requires `4.0.0..<6.0.0`. The ranges do not
intersect, so Swift Package Manager cannot resolve an app that depends on both:

```
'google-mlkit-swiftpm' is incompatible with 'firebase-ios-sdk' because
'google-mlkit-swiftpm' 9.0.2 depends on 'gtm-session-fetcher' 3.5.0..<4.0.0
and 'firebase-ios-sdk' 13.1.1 depends on 'gtm-session-fetcher' 4.0.0..<6.0.0.
```

`google-mlkit-swiftpm` 9.0.3 widened that range to `3.5.0..<6.0.0`, which
covers both. The Dart packages still pin 9.0.2.

## Usage

```yaml
dependency_overrides:
  google_mlkit_commons:
    git:
      url: https://github.com/Navideck/google_mlkit_flutter.git
      ref: v1.0.1+navideck.1
      path: packages/google_mlkit_commons
  google_mlkit_text_recognition:
    git:
      url: https://github.com/Navideck/google_mlkit_flutter.git
      ref: v1.0.1+navideck.1
      path: packages/google_mlkit_text_recognition
```

## When to delete this

Once `google_mlkit_commons` / `google_mlkit_text_recognition` publish a version
whose `Package.swift` pins `google-mlkit-swiftpm` 9.0.3 or later, drop the
overrides and go back to the hosted packages.
