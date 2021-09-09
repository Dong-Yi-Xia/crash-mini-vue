# crash-mini-vue

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

### Deployment
After `npm run build` a new folder call dist
Use the dist folder to deploy the single page app.
Install preview deployment
```
npm i -g serve
```
To preview deployment locally
```
serve -s dist
```
- Developement= localhost:8080
- Production= localhost:5000

### JSON Server
```
npm i json-server
```
A full fake RESP API \
https://www.npmjs.com/package/json-server

Create a `db.json` file with some data \

Start JSON Server
```
json-server --watch db.json
```
### Notes
Rather than writing out `json-server --watch db.json` create an alias \
Create an alias name and add it to the scripts in package.json 
```
"backend": "json-server --watch db.json --port 5000"
```
It will run it on port 5000 \
To start `npm run backend`

