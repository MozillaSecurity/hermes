![Logo](https://github.com/posidron/posidron.github.io/raw/master/static/images/hermes.png)


Hermes is the codename for the integrated Message Manager fuzzer in Firefox.

**Bugzilla:** https://bugzilla.mozilla.org/show_bug.cgi?id=777600


<h3>Setup</h3>

In order to launch Hermes it is required to have a build of Firefox at hand, which was compiled with the "--enable-fuzzing" compile time option.

Look at https://github.com/mozillasecurity/mozilla-build-configs/ for ready-made build configurations or
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
MESSAGEMANAGER_FUZZER_BLACKLIST | none | optional

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
[MessageManagerFuzzer] Message: Content:LocationChange in process: 2
[MessageManagerFuzzer]     <Enumerating found object>
[MessageManagerFuzzer]     - Property: webProgress
[MessageManagerFuzzer]         <Enumerating found object>
[MessageManagerFuzzer]         - Property: isTopLevel
[MessageManagerFuzzer]         - Property: isLoadingDocument
[MessageManagerFuzzer]         ! Mutated value of type |boolean|: '1' to '1'
[MessageManagerFuzzer]         - Property: loadType
[MessageManagerFuzzer]         ! Mutated value of type |int32|: '1' to '-16'
[MessageManagerFuzzer]         - Property: DOMWindowID
[MessageManagerFuzzer]     - Property: requestURI
[MessageManagerFuzzer]     - Property: originalRequestURI
[MessageManagerFuzzer]     - Property: documentContentType
[MessageManagerFuzzer]     - Property: innerWindowID
[MessageManagerFuzzer]     - Property: location
[MessageManagerFuzzer]     - Property: flags
[MessageManagerFuzzer]     ! Mutated value of type |int32|: '0' to '1048575'
[MessageManagerFuzzer]     - Property: canGoBack
[MessageManagerFuzzer]     - Property: canGoForward
[MessageManagerFuzzer]     - Property: documentURI
[MessageManagerFuzzer]     - Property: title
[MessageManagerFuzzer]     - Property: charset
[MessageManagerFuzzer]     - Property: mayEnableCharacterEncodingMenu
[MessageManagerFuzzer]     - Property: principal
[MessageManagerFuzzer]     - Property: synthetic
[MessageManagerFuzzer]     ! Mutated value of type |boolean|: '0' to '1'
[MessageManagerFuzzer]     - Property: inLoadURI
[MessageManagerFuzzer] Mutated 'Content:LocationChange' Message: ({webProgress:{isTopLevel:true, isLoadingDocument:true, loadType:-16, DOMWindowID:4294967297}, requestURI:"https://www.google.de/?gfe_rd=cr&ei=D1_CWJ3hG5Gg8weFqIHYAg", originalRequestURI:"https://google.com/", documentContentType:"text/html", innerWindowID:4294967300, location:(void 0), flags:1048575, canGoBack:true, canGoForward:false, documentURI:"https://www.google.de/?gfe_rd=cr&ei=D1_CWJ3hG5Gg8weFqIHYAg", title:"", charset:"UTF-8", mayEnableCharacterEncodingMenu:true, principal:({}), synthetic:true, inLoadURI:false})
[...]
```
