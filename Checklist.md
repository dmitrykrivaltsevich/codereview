RESTful API
---------------
1. Endpoints don't contain _vebrs_ (should be _nouns_).
   Highlights flaws in the API in case of violation.

Code
---------------
1. There is a test (at least one) which covers added or modified functionality (all cases).
2. All method's (or function's) parameters are in use.
   Preferably: there is an automated check which fails a build when this rule is violated.
   Highlights "dead" code and missed functionality.
3. All configuration parameters are still in use.
   Highlights "dead" code.
4. Exceptions and error conditions are logged properly.
5. App doesn't log sensitive data (tokens, raw request or responses, PII).
6. Order is not expected in the code which iterates over HashSet values or HashMap keys.

RegEx
---------------
1. Expression is case-insensitive (`(?i)`) or it is clear that it should be case-sensitive.
2. Expression doesn't rely on position (`^$`). Spaces before first word could bypass checks that use such expressions.
3. Quantifiers (`{1,3}`) are well-reasoned. Malicious person can bypass such expression using more repetition than expected.
4. No ReDoS-like expressions `(a+)+`. Payload `aaaaaaa....aaaaaaaab` requires `2^n` comparisions.
5. Quantifiers (`+*`) are well-reasoned. Expression `a'\s+b` won't catch `a' space-0-times b`.
6. Blacklist includes all Unicode-alternatives. Expression `a[\n]*b` won't catch ` a\rb`.
   
Playframework (Scala)
---------------
1. `play.api.libs.concurrent.Execution.Implicits.defaultContext` is used instead of `scala.concurrent.ExecutionContext.Implicits.global`.
   This rule can be relaxed for tests.
2. `ActorSystem` is properly closed after usage (violation of this rule often happens in tests).

Scala
---------------
1. Expected that `Future.fallbackTo { ... }` code inside curly brackets runs even when `Future` completes successfully.

AWS
---------------
1. Avoid "t2.*" family or make sure that CPU credits will be a positive number in order to avoid performance degradation. Note that initial amount of credits will expire after 24h. Scenario when _credits consumed = credits earned_ it will lead to performance degradation.

