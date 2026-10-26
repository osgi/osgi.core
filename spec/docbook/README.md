# DocBook of Core Release 8

The DocBook of the specification repositories at the versions of
Core Release 8, unpacked: `<artifactId>/<version>/` with `chapters/`,
`javadoc/`, `resources/` and `META-INF/docbook.properties`, as the
`docbook` goal of osgi-docbook-maven-plugin packs it.

A specification repository deploys the DocBook of each release as
`org.osgi.spec:<artifactId>:<version>` (type `zip`, classifier
`docbook`). The releases of Core Release 8 were made in the OSGi
monorepo, which deployed none, so the book takes them from here: an archive
listed in `docbooks` of `spec/pom.xml` comes from the Maven repositories,
and only when it is not there from this directory.

Converted once from the tag `r8-core-final` of the monorepo: for every chapter
of the core book and every package whose javadoc a chapter includes, the
sources and chapters of the tag were packed with the `docbook` goal, at the
version the API had at the tag. Do not edit; a correction belongs to the
specification repository and its next release.
