## Publishing (until automated)

- `npm run changeset` for changelog worthy changes
- `npm run version` to bump `package.json` version based on changesets, materialize changesets into CHANGELOG.md
- Commit as `Version bump to x.y.z` (TODO: automate)
- `npm run publish` to publish version to npm
- `git push --tags` to publish tags to Github
