# rush-dependency-versions

## Repro
`rush install`

### Expected
Downloads `repeat-string@1.6.0` as specified in `pnpm-lock.yaml`

### Actual
Downloads `repeat-string@1.6.1` (latest on npmjs.com)

## Setup
These steps were used to generate the files currently in this repo (like `pnmp-lock.yaml`).  They do not need to be run again to repro the actual issue.

1. Download dependencies from npmjs.com to local disk
   1. `npm pack pad-left@2.1.0`
   2. `npm pack repeat-string@1.6.0`
2. Upload `pad-left@2.1.0` and `repeat-string@1.6.0` to a private registry (e.g. [Verdaccio](https://github.com/verdaccio/verdaccio))
3. Edit `common/config/rush/.npmrc` and change `registry` to your private registry
4. `rush update`
5. Note that `pnpm-lock.yaml` contains:
```
packages:
  /pad-left/2.1.0:
    dependencies:
      repeat-string: 1.6.0
  /repeat-string/1.6.0:
```
6. Revert changes to `common/config/rush/.npmrc`
7. `git commit`
