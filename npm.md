# npm
## Update all locals node modules
```
ncu
ncu -u
```
## Update all global node modules
```
ncu -g
npm install -g [package1 package2 …]
```
## Upgrade node to the latest LTS
```
sudo npm cache clean -f
sudo npm install -g n
sudo n 4.4.2
```
## Running a project-local bin
```
npm i -D webpack		# install
npx webpack			    # run
```
