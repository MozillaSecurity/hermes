![](http://people.mozilla.com/~cdiehl/img/hermes.png)


Hermes is the codename for the integrated Message Manager fuzzer in Firefox.

**Bugzilla:** https://bugzilla.mozilla.org/show_bug.cgi?id=777600


<h3>Setup</h3>

In order to launch Hermes it is required to have a build of Firefox at hand, which was compiled with the "--enable-fuzzing" compile time option.

Look at https://github.com/MozillaSecurity/mozilla-build-configs/ for ready-made build configurations or
download such builds for your platform from our build server.

> Building by yourself gives you at the moment the advantage of easily running test-suites against Hermes.
To find out which test-suites are supported run "./mach --help" and look for the "Testing:" section.


<h3>Environment</h3>

Controlling Hermes is entirely done via environment variables.


Variable Name | Default Value | Usage
------------- | ------------- | -----
MESSAGEMANAGER_FUZZER_ENABLE | 1 | required
MESSAGEMANAGER_FUZZER_ENABLE_LOGGING | 1 | optional
MESSAGEMANAGER_FUZZER_MUTATION_PROBABILITY | 2 | optional
MESSAGEMANAGER_FUZZER_STRINGSFILE | none | optional


Additional environment variables exposed by Firefox which are helpful for debugging purposes and crash analyzes.

```
MOZ_IPC_MESSAGE_LOG=1
```


<h3>Examples</h3>

To run Hermes against the Mochitest test-suite:

```bash
MESSAGEMANAGER_FUZZER_ENABLE=1 MESSAGEMANAGER_FUZZER_ENABLE_LOGGING=1 MESSAGEMANAGER_FUZZER_STRINGSFILE=<path>/hermes.strings ./mach mochitest
```

**Expected output:**

```
[...]
[MessageManagerFuzzer] Message: RemoteLogins:insecureLoginFormPresent in process: 0
[MessageManagerFuzzer]     <Enumerating found object>
[MessageManagerFuzzer]     - Property: hasInsecureLoginForms
[MessageManagerFuzzer] Message: SessionStore:update in process: 0
[MessageManagerFuzzer]     <Enumerating found object>
[MessageManagerFuzzer]     - Property: data
[MessageManagerFuzzer]         <Enumerating found object>
[MessageManagerFuzzer]         - Property: historychange
[MessageManagerFuzzer]             <Enumerating found object>
[MessageManagerFuzzer]             - Property: entries
[MessageManagerFuzzer]                 <Enumerating found object>
[MessageManagerFuzzer]                 - Property: 0
[MessageManagerFuzzer]                 - Property: 1
[MessageManagerFuzzer]                 - Property: 2
[MessageManagerFuzzer]                     <Enumerating found object>
[MessageManagerFuzzer]                     - Property: url
[MessageManagerFuzzer]                     - Property: title
[MessageManagerFuzzer]                     ! Mutated value of type |string|: [...]
[MessageManagerFuzzer]                     - Property: subframe
[MessageManagerFuzzer]                     - Property: charset
[MessageManagerFuzzer]                     ! Mutated value of type |string|: [...]
[MessageManagerFuzzer]                     - Property: ID
[MessageManagerFuzzer]                     ! Mutated value of type |int32|: '2' to '2147483647'
[MessageManagerFuzzer]                     - Property: docshellUUID
[MessageManagerFuzzer]                     ! Mutated value of type |string|: [...]
[MessageManagerFuzzer]                     - Property: triggeringPrincipal_base64
[MessageManagerFuzzer]                     - Property: docIdentifier
[MessageManagerFuzzer]                     ! Mutated value of type |int32|: '2' to '65535'
[MessageManagerFuzzer]                     - Property: persist
[MessageManagerFuzzer]                     ! Mutated value of type |boolean|: '1' to '0'
[MessageManagerFuzzer]             - Property: userContextId
[MessageManagerFuzzer]             - Property: index
[MessageManagerFuzzer]             ! Mutated value of type |int32|: '3' to '-262144'
[MessageManagerFuzzer]             - Property: fromIdx
[MessageManagerFuzzer]         - Property: pageStyle
[MessageManagerFuzzer]     - Property: telemetry
[MessageManagerFuzzer]     - Property: flushID
[MessageManagerFuzzer]     - Property: isFinal
[MessageManagerFuzzer]     ! Mutated value of type |boolean|: '0' to '0'
[MessageManagerFuzzer]     - Property: epoch
[MessageManagerFuzzer]     ! Mutated value of type |int32|: '0' to '-2147483648'
[...]
```
