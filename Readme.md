## Architecture template with sass and npm of a web interface   

---  

## Description :  


Ready-to-use architecture model of a UI with sass and npm.   
Version : 1.0.0   
Date : 2020-05-06   
Responsable : HI   

---  

## Implementation :   


### project init :  

__$ npm install__

---

### dev environment :  

__$ npm run watch:sass__   

*This is the script in package.json :*  
  - `"watch:sass": "node-sass sass/main.scss css/style.css -w",` 


***or if you prefer to use the npm server*** 

__$ npm install live-server -g__  

__$ npm run start__

*This is the script in package.json :*  
  - `"devserver": "live-server", "start": "npm-run-all --parallel devserver watch:sass",`

***add --browser option if you need*** :  
  - `"devserver": "live-server --browser=firefox",`

---

### prod environment

__$ npm run build:css__


*This is the script in package.json :*

- It compiles all scss in css
  - `"compile:sass": "node-sass sass/main.scss css/style.comp.css",`
- It prefixes with browsers prefix
  - `"prefix:css": "postcss --use autoprefixer -b 'last 10 versions' css/style.comp.css -o css/style.prefix.css",`
- It compresses the output css file
  - `"compress:css": "node-sass css/style.prefix.css css/style.css --output-style compressed",`
- It runs the 3 commands above to be ready to production
  - `"build:css": "npm-run-all compile:sass prefix:css compress:css"`


***replace with these lines if you have used several .css files to concatenate them (like a font file for icons for example)***   
*(just rename the file to be concat with your file name)*   
`"compile:sass": "node-sass sass/main.scss css/style.comp.css",  
"concat:css": "concat -o css/style.concat.css css/icon-font.css css/style.comp.css",  
"prefix:css": "postcss --use autoprefixer -b 'last 10 versions' css/style.concat.css -o css/style.prefix.css",  
"compress:css": "node-sass css/style.prefix.css css/style.css --output-style compressed",  
"build:css": "npm-run-all compile:sass concat:css prefix:css compress:css"`  