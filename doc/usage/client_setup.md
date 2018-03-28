# Client setup
There are three different types of calls to Akismet:

1. [Key verification](../features/key_verification.md) will verify whether or not a valid API key is being used. This is especially useful if you will have multiple users with their own Akismet subscriptions using your application.
2. [Comment check](../features/comment_check.md) is used to ask Akismet whether or not a given post, comment, profile, etc. is spam.
3. [Submit spam](../features/submit_spam.md) and [submit ham](../features/submit_ham.md) are follow-ups to let Akismet know when it got something wrong (missed spam and false positives). These are very important, and you shouldn't develop using the Akismet API without a facility to include reporting missed spam and false positives.

All these calls go through the `Client` class that provides access to the Akismet API endpoints.

# The Akismet client
The `Client` class provides access to the Akismet API endpoints.

```
new Client(String apiKey, string|Blog blog, {
  Uri endPoint,
  bool isTest = false,
  String userAgent
})
```

```dart
import 'dart:async';
import 'package:akismet/akismet.dart';

final client = new Client('123YourAPIKey', 'http://www.yourblog.com');
```

To instantiate a new `Client`, you need the following elements:
- an API key:
- the URL of your blog or site

### Setting your user agent
If possible, your user agent string should always use the following format:

```
Application Name/Version | Plugin Name/Version
```

!!! info
    The default user agent string looks like: `Dart/1.24.3 | Akismet/4.0.0`

## Blog metadata
The `Blog` class provides metadata about your blog or site.

```
new Blog(string|Uri url, {
  String charset = '',
  List<String> languages
})
```

!!! tip
    The more data you send Akismet about each comment, the greater the accuracy.
    You should provide as much information as you can about your blog or site.