# Emerald Sequoia code

## Overview

This GitHub area contains apps and libraries used in the development of apps originally authored by Emerald Sequoia LLC.

## Apps, Libraries, and Tools

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

The tools are:
*   `buildscripts`: A collection of scripts used as part of the app or library build process.

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

## Installing

All library and app directories must live at the same level (they refer to each other using relative `../` paths). So, for example, to download all of the necessary components for Emerald Timestamp:

```shell
mkdir emeraldsequoia
cd emeraldsequoia
git clone git@github.com:EmeraldSequoia/Timestamp.git Timestamp
git clone git@github.com:EmeraldSequoia/buildscripts.git buildscripts
git clone git@github.com:EmeraldSequoia/esutil.git esutil
git clone git@github.com:EmeraldSequoia/estime.git estime
git clone git@github.com:EmeraldSequoia/eslocation.git eslocation
```

## Using Xcode

A Mac with Xcode installed is required.

The Xcode project for each app includes all of the dependent library
projects that it needs, to simplify development as you work on one
app: You can edit library code within the same Xcode window as the
app. Note that this means when you are ready to commit your changes,
you will also need to commit any library code that you have edited.

Xcode is a very complicated app and is beyond the scope of this
document, but each app directory's README has some instructions about
where to find the project file and what to build.
