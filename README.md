# osgi.core

[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/osgi/osgi.core/badge)](https://securityscorecards.dev/viewer/?uri=github.com/osgi/osgi.core)
[![build](https://github.com/osgi/osgi.core/actions/workflows/build.yml/badge.svg?branch=main)](https://github.com/osgi/osgi.core/actions/workflows/build.yml)
[![Maven Central](https://img.shields.io/maven-central/v/org.osgi/osgi.core)](https://central.sonatype.com/artifact/org.osgi/osgi.core)

OSGi Core Release: the `osgi.core` jar with the API of all Core
specifications, and the OSGi Core specification book (PDF and HTML).

Part of the [OSGi Specification Project](https://projects.eclipse.org/projects/technology.osgi).

## Contents

This repository holds no specification sources of its own. The API, the
specification chapters and the TCKs live in the specification repositories,
for example [org.osgi.framework](https://github.com/osgi/org.osgi.framework).
This repository pins one released version of each of them and builds from
those:

- `api`: `org.osgi:osgi.core`, the classes of the Core API packages,
  taken unchanged from the pinned `org.osgi` artifacts, with their sources
  and Javadoc as `-sources` and `-javadoc` jars. The build baselines the jar
  against the previous release of `osgi.core`.
- `spec`: `org.osgi.spec:osgi.core`, the Core specification as PDF and
  HTML, assembled from the pinned `org.osgi.spec` DocBook artifacts.

Each specification repository has one version property in `pom.xml`. It
selects both the API artifact (`org.osgi:<repo>`) and the DocBook artifact
(`org.osgi.spec:<repo>`) of that repository.

## Build

```
mvn clean verify
```

The `build` workflow builds every push and pull request the same way; every
push to `main` deploys a fresh SNAPSHOT to Sonatype Central snapshots, and
a weekly schedule keeps it fresh in quiet times.

## Versioning and releases

The version lives in exactly one place: the `-Drevision=` line in
[`.mvn/maven.config`](.mvn/maven.config). The poms only reference
`${revision}` — never add a second copy of the version anywhere else.

A release is the creation of a git tag whose name equals that version,
without any prefix: `1.2.3`, not `v1.2.3`.

1. Open a pull request that sets `-Drevision=1.2.3` in `.mvn/maven.config`
   and merge it.
2. Go to **Releases → Draft a new release**, type `1.2.3` under
   "Choose a tag" and select "Create new tag on publish". A saved draft
   does not create the tag yet, so a draft is a safe intermediate state.
3. Leave **Target: `main`** (the default) — the tag will point at the
   merge commit.
4. Click **Publish release**. Publishing creates the tag, and the tag
   triggers the release workflow.

The command-line equivalent is
`gh release create 1.2.3 --target main --generate-notes`.

The release workflow refuses a tag that does not exactly match
`.mvn/maven.config`, and refuses `-SNAPSHOT` versions. It builds and tests
the repository, then stages the signed artifacts to Maven Central — the
final publish stays a manual step in the Central portal.

## Contact

- Project contact page: <https://projects.eclipse.org/projects/technology.osgi/contact>
- Mailing lists:
  - [osgi-dev](https://accounts.eclipse.org/mailing-list/osgi-dev) —
    developer list for discussion of the OSGi Specification Project
  - [osgi-users](https://accounts.eclipse.org/mailing-list/osgi-users) —
    public list for discussion of OSGi technology and specifications; ask
    your technical questions about OSGi here
  - [osgi-wg](https://accounts.eclipse.org/mailing-list/osgi-wg) —
    OSGi Working Group mail list
- Slack: <https://osgiwg.slack.com/>
- Spec call: Zoom call every **second Wednesday** — see the
  [calendar](https://calendar.google.com/calendar/u/0/newembed?src=c_fh3lhb5p0l29f6phu2ndifh4a4@group.calendar.google.com)
  for the exact time (please mind your local timezone).
