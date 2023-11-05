This GitHub area contains apps and libraries used in the development of apps originally authored by Emerald Sequoia LLC.

The apps are:

*   Emerald Timestamp [`timestamp`]: the single iOS iPhone+iPad app "Timestamp" (Objective-C++)
*   Emerald Observatory [`observatory`]: the single iOS iPad app "Observatory" (Objective-C++)
*   Emerald Chronometer [`chronometer`]:

    *   The iPhone app "Chronometer" (Objective-C++)
    *   The iPad app "Chronomter for iPad" (Objective-C++)
    *   The WearOS app "Chronometer" and its subset apps (Java and C++ via JNI)

The libraries are:

*   `esutil`: A base set of common utilities (including threading) written in C++
*   `estime`: A set of utilities that provide NTP-corrected time
*   `eslocation`: A set of utilities that provide location, either through the device or selected by the user
*   `esastro`: A set of utilities for various astronomical calculations, including a caching manager

Not all apps use the libraries. For the iOS apps, the dependency tree looks like this:

```mermaid
flowchart
    classDef app fill:#f96

    esutil(esutil)
    estime(estime)
    eslocation(eslocation)
    esastro(esastro)

    Timestamp[[Timestamp]]
    Observatory[[Observatory]]

    estime-->esutil
    eslocation-->esutil
    eslocation-->estime
    esastro-->eslocation
    esastro-->estime
    esastro-->esutil

    Timestamp:::app-->eslocation
    Timestamp:::app-->estime
    Timestamp:::app-->esutil

    Observatory:::app-->esastro
    Observatory:::app-->eslocation
    Observatory:::app-->estime
    Observatory:::app-->esutil
```

The iOS Chronometer apps do not use these libraries; they contain similar code that predated the creation of the libraries. The WearOS (Android) Chronometer apps are documented in more detail in that app's directory.
