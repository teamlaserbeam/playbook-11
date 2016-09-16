# `Semantic versioning`

## Releases

- Done at the end of each sprint.
- Doesn't mean things go-live in this moment.
- A new release means development phase is over, which occurs when all tests have passed.

### Major

> Major version update when you make incompatible API changes.

- Initial development user major version `0`, e.g. `0.1.0`.

### Minor

> Minor version update when you add functionality in a backwards-compatible manner.

### Patch

> Patch version update when you make backwards-compatible bug fixes.

## FAQ

### How should I deal with revisions in the 0.y.z initial development phase?

> The simplest thing to do is start your initial development release at 0.1.0 and then increment the minor version for each subsequent release.

### How do I know when to release `1.0.0`?

> If your software is being used in production, it should probably already be 1.0.0. If you have a stable API on which users have come to depend, you should be 1.0.0. If you’re worrying a lot about backwards compatibility, you should probably already be 1.0.0.

### Doesn’t this discourage rapid development and fast iteration?

> Major version zero is all about rapid development. If you’re changing the API every day you should either still be in version 0.y.z or on a separate development branch working on the next major version.
