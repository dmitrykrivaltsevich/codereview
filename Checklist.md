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
5. Order is not expected in the code which iterates over HashSet values or HashMap keys.
   
Playframework (Scala)
---------------
1. `play.api.libs.concurrent.Execution.Implicits.defaultContext` is used instead of `scala.concurrent.ExecutionContext.Implicits.global`.
   This rule can be relaxed for tests.

Scala
---------------
1. Expected that `Future.fallbackTo { ... }` code inside curly brackets runs even when `Future` completes successfully.

AWS
---------------
1. Avoid "t2.*" family or make sure that CPU credits will be a positive number in order to avoid performance degradation. Note that initial amount of credits will expire after 24h. Scenario when _credits consumed = credits earned_ it will lead to performance degradation.
