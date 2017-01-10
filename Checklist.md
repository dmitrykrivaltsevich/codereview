RESTful API
---------------
1. Endpoints don't contain _vebrs_ (should be _nouns_).
   Highlights flaws in the API in case of violation.

Code
---------------
1. All method's (or function's) parameters are in use.
   Preferably: there is an automated check which fails a build when this rule is violated.
   Highlights "dead" code and missed functionality.
2. All configuration parameters are still in use.
   Highlights "dead" code
3. Exceptions and error conditions are logged properly
4. App doesn't log sensitive data (tokens, raw request or responses, PII).
   
Playframework (Scala)
---------------
1. `play.api.libs.concurrent.Execution.Implicits.defaultContext` is used instead of `scala.concurrent.ExecutionContext.Implicits.global`.
   This rule can be relaxed for tests.

Scala
---------------
1. Expected that `Future.fallbackTo { ... }` code inside curly brackets runs even when `Future` completes successfully.

