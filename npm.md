# npm

## Update all locals node modules
```
ncu
ncu -u
ncu -a
npm install
```

## Update some locals node modules
```
ncu
npm install [package1 package2 …]
```

## Update all global node modules
```
ncu -g
npm install -g [package1 package2 …]
```
## Upgrade node to the latest LTS
Use nvm

## Running a project-local bin
```
npm i -D webpack		# install
npx webpack			    # run
```

## When npm scripts are fired?

The following table is a non-exhaustive list of when scripts are executed

|   | `npm install` during development | `npm publish` during development | `npm install` in production |
|-|-|-|-|
| install | ✅ |  | ✅ |
| prepublish | ✅ | ✅ |  |
| prepublishOnly |  | ✅ | |
