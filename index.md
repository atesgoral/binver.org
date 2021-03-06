Binary Versioning 1.0.0
==============================

Summary
-------

Given a version number MAJOR.MINOR.PATCH, increment the:

1. MAJOR version when you make incompatible API changes,
1. MINOR version when you add functionality in a backwards compatible
   manner, and
1. PATCH version when you make backwards compatible bug fixes.

MAJOR, MINOR and PATCH can be either "0" or "1". Therefore there can be at most 8 versions.

Introduction
------------

Quote:

> In the world of software management there exists a dreaded place called
> "dependency hell." The bigger your system grows and the more packages you
> integrate into your software, the more likely you are to find yourself, one
> day, in this pit of despair.
>
> In systems with many dependencies, releasing new package versions can quickly become a nightmare. If the dependency specifications are too tight, you are in danger of version lock (the inability to upgrade a package without having to release new versions of every dependent package). If dependencies are specified too loosely, you will inevitably be bitten by version promiscuity (assuming compatibility with more future versions than is reasonable). Dependency hell is where you are when version lock and/or version promiscuity prevent you from easily and safely moving your project forward.

[Semantic Versioning](https://semver.org/) is a solution to this problem.

But Semantic Versioning allows just about any positive integer to be used, leading to developers taking the liberty to carelessly publish release after release, with no accountability on how varied the version numbers get, or how many different versions of a
piece of software get released into the wild. A simple solution is to constrain parts that make up a version to be just binary digits.

I call this system "Binary Versioning."

Binary Versioning Specification (BinVer)
------------------------------------------

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://tools.ietf.org/html/rfc2119).

1. Software using Binary Versioning MUST declare a public API. This API
could be declared in the code itself or exist strictly in documentation.
However it is done, it SHOULD be precise and comprehensive.

1. A normal version number MUST take the form X.Y.Z where X, Y, and Z are
binary digits, and MUST NOT contain leading zeroes. X is the
major version, Y is the minor version, and Z is the patch version.
Each element MUST increase numerically. For instance: 1.0.0 -> 1.1.0.

1. Once a versioned package has been released, the contents of that version
MUST NOT be modified. Any modifications MUST be released as a new version.

1. Major version zero (0.y.z) is for initial development. Anything MAY change
at any time. The public API SHOULD NOT be considered stable.

1. Version 1.0.0 defines the public API. The way in which the version number
is incremented after this release is dependent on this public API and how it
changes.

1. Patch version Z (x.y.Z | x = 1) MUST be incremented if only backwards
compatible bug fixes are introduced. A bug fix is defined as an internal
change that fixes incorrect behavior.

1. Minor version Y (x.Y.z | x = 1) MUST be incremented if new, backwards
compatible functionality is introduced to the public API. It MUST be
incremented if any public API functionality is marked as deprecated. It MAY be
incremented if substantial new functionality or improvements are introduced
within the private code. It MAY include patch level changes. Patch version
MUST be reset to 0 when minor version is incremented.

1. Major version X (X.y.z | X = 1) MUST be incremented if any backwards
incompatible changes are introduced to the public API. It MAY also include minor
and patch level changes. Patch and minor version MUST be reset to 0 when major
version is incremented.

1. Precedence refers to how versions are compared to each other when ordered.

   1. Precedence MUST be calculated by separating the version into major,
      minor, patch and pre-release identifiers in that order.

   1. Precedence is determined by the first difference when comparing each of
      these identifiers from left to right as follows: Major, minor, and patch
      versions are always compared numerically.

      Example: 0.0.1 < 0.1.0 < 1.1.0 < 1.1.1.

Backus–Naur Form Grammar for Valid BinVer Versions
--------------------------------------------------
```
<valid semver> ::= <version core>

<version core> ::= <major> "." <minor> "." <patch>

<major> ::= <binary digit>

<minor> ::= <binary digit>

<patch> ::= <binary digit>

<binary digit> ::= "0" | "1"
```

Why Use Binary Versioning?
----------------------------

Constraints stoke creativity. What if the entire lifecycle of your software was
limited to exactly 8 very intentional releases? Example scenario:

1. You just had an idea. Cut 0.0.0.
1. Wrote some code. Only some parts are working, but hey. Cut 0.0.1.
1. Ooh! Some actual features. Cut 0.1.0.
1. LOL. Stupid typo. Fix it. Cut 0.1.1.
1. Feature complete. Cut 1.0.0. Party.
1. Fix the bug. Cut 1.0.1.
1. Ooh! Good idea! Add it! Cut 1.1.0.
1. Forgot to add the README.md badges. Cut 1.1.1.
1. Move onto the next adventure!

FAQ
---

### How do I know when to release 1.0.0?

You'll know. Something deep inside will tell you.

### Doesn't this discourage rapid development and fast iteration?

Yes, it does.

### If even the tiniest backwards incompatible changes to the public API require a major version bump, won't I end up at version 42.0.0 very rapidly?

There's no "42" in binary.

### What do I do if I accidentally release a backwards incompatible change as a minor version?

As soon as you realize that you've broken the Binary Versioning spec, fix
the problem and release a new minor version that corrects the problem and
restores backwards compatibility. Unless you were already at minor version 1.
Then there's really nothing you can do.

### Does BinVer have a size limit on the version string?

Yes. 5 characters: "N.N.N"

### Is there a suggested regular expression (RegEx) to check a BinVer string?

Easy:

```
^[01]\.[01]\.[01]$
```

### Don't you have something actually useful to do?

Yes.

About
-----

This is some silliness by [Ates Goral](https://magnetiq.ca), whipped up in about two hours through unapologetic cloning and tweaking of the [Semantic Versioning specification website](https://semver.org/).

The Semantic Versioning specification was originally authored by [Tom
Preston-Werner](https://tom.preston-werner.com), inventor of Gravatar and
cofounder of GitHub.

If you'd like to leave feedback, please [open an issue on
GitHub](https://github.com/atesgoral/binver.org/issues).

License
-------

[Creative Commons ― CC BY 3.0](https://creativecommons.org/licenses/by/3.0/)
