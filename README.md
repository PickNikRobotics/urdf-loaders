# urdf-loaders

URDF loading code in both [C# for Unity](./unity/Assets/URDFLoader/) and [Javascript for THREE.js](./javascript/), as well as example [JPL ATHLETE](https://en.wikipedia.org/wiki/ATHLETE) URDF files

[Demo Here!](https://gkjohnson.github.io/urdf-loaders/javascript/example/bundle/)

![Example](./unity/Assets/docs/asset%20store/all-urdfs.png)

### Flipped Models

The `_flipped` variants of the URDF ATHLETE models invert the revolute joint axes to model ATHLETE in a configuration with the legs attached to the bottom of the chassis.

### Publishing the PickNik JavaScript Package

The PickNik-scoped JavaScript package is published from `javascript/` as `@picknikrobotics/urdf-loader` to GitHub Packages.

1. Land the code change on `master`.
2. Bump the package version from `javascript/`:

```sh
cd javascript
npm version patch --no-git-tag-version
```

This updates `javascript/package.json` and `javascript/package-lock.json`. Open and merge a PR with those two files.

3. Create a GitHub Release after the version bump is on `master`:

```sh
gh release create vX.Y.Z \
  --repo PickNikRobotics/urdf-loaders \
  --target master \
  --title "vX.Y.Z" \
  --notes "Release notes."
```

The `.github/workflows/publish-package.yaml` workflow runs on the release `published` event and executes `cd javascript && npm ci && npm publish`. It uses the workflow `GITHUB_TOKEN` with `packages: write`; maintainers do not need a personal npm token for the normal release path.

4. Verify the package:

```sh
npm view @picknikrobotics/urdf-loader@X.Y.Z version --registry=https://npm.pkg.github.com
```

# LICENSE

The software is available under the [Apache V2.0 license](./LICENSE).

Copyright © 2020 California Institute of Technology. ALL RIGHTS
RESERVED. United States Government Sponsorship Acknowledged.
Neither the name of Caltech nor its operating division, the
Jet Propulsion Laboratory, nor the names of its contributors may be
used to endorse or promote products derived from this software
without specific prior written permission.
