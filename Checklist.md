General Code Review Rules
---------------
1. The intention of a code review is to find defects and not style variations. Defects can be:
  - failures (e.g. certain parameters lead to unexpected behaviour, unspecified results, exceptions or errors reports) 
  - defects in logic
  - security vulnerabilities
  - specification mismatch
  - missed implementation
  - inefficient implementation
    - usage of O(n^2) algorithms for the task where O(log(n)) algorithms is available
    - similar computations can be done with a smaller version of a program (less code - better)
    - similar code is available in a known and well-tested library
  - violations of best practices which leads to defects.
2. Use words _can_ or _could_ instead of _don't_ in your comments.
3. Always show _how_ as a part of any suggestion.
4. _Be_-sentences are forbidden, (e.g. be more patient, be smart, be nice, etc)

RESTful API
---------------
1. Endpoints contain _nouns_ (and never _verbs_).
   Highlights flaws in the API in case of violation.
2. Use UUID or random hashes as IDs instead of numbers in order to prevent data leakage.

Code
---------------
1. There is a test (at least one) which covers added or modified functionality (all cases / branches).
2. All method's (or function's) parameters are in use.
   Preferably: there is an automated check which fails a build when this rule is violated.
   Highlights "dead" code and missed functionality.
3. All configuration parameters are still in use.
   Highlights "dead" code.
4. Exceptions and error conditions are logged properly.
5. App doesn't log sensitive data (tokens, raw request or responses, PII).
6. Order is not expected in the code which iterates over HashSet values or HashMap keys.
7. Serialization and deserialization are aligned and work with same fields in the same order.

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
   Use DI: `class Service @Inject() (...)(implicit ec: ExecutionContext) { ... }`. This rule can be relaxed for tests.
2. `ActorSystem` is properly closed after usage (violation of this rule often happens in tests).
3. Sequence of `route(app, request)` in tests can be executed in any order and it's expected.

Scala
---------------
1. Expected that `Future.fallbackTo { ... }` code inside curly brackets runs even when `Future` completes successfully.
2. Expected that `Option.forall( ... )` or `Seq.forall( ... )` returns `true` for _any_ predicate when the value is `None` or `Nil` respectively. See [Vacuous truth](https://en.wikipedia.org/wiki/Vacuous_truth)
3. All fields in case class have either case class type or implement `equals` and `hashCode` methods. For example, `scala.util.matching.Regex` cannot be defined as a field in a case class.
4. Variable (`var`) or mutable collection is not a memeber of class or it is expected that modification of this collection is not thread safe (pattern: read -> modify -> save back).

JavaScript
---------------
1. String checks with `indexOf` also work for strings in different registers (i.e. case-insensitive).

AWS
---------------
1. Avoid "t2.*" family or make sure that CPU credits will be a positive number in order to avoid performance degradation. Note that initial amount of credits will expire after 24h. In case when _credits consumed = credits earned_ it will lead to performance degradation.

