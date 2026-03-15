# Todo

1. Navbar
1. Rich text editor (a complete nighmare)
1. Every to pick something
    1. Pick day
    1. Pick week
    1. Pick month
    1. Pick year
    1. Pick date
    1. Pick colour
1. Charts (a real nightmare)
1. _Inputs chips_ doesn't work on mobile enters
1. On mobile devices, you cannot dismiss the _toast_ by dragging it left or right.

# Fix in build (work in dev)

1. The touch function of the app _drawer-sheet_ does not work on mobile devices.
1. Carousel dots (there are more, looks broken)

# Something else

1. Error/danger icon is awful (I know)

## Minifies

1. Javascript: teser
1. css: csso not working well so use an web site online (awful)

### Scripts

```json
{
	"name": "at",
	"version": "1.0.0",
	"description": "",
	"main": "index.js",
	"scripts": {
		"test": "echo \"Error: no test specified\" && exit 1",
		"csso:build": "bash build.css.csso.sh",
		"css:dev": "npx @tailwindcss/cli -i ./src/tailwind/index.css -o ./public/custom/css/index.css --watch",
		"css:build": "npx @tailwindcss/cli -i ./src/tailwind/index.css -o ./public/custom/css/index.css && npm run csso:build",
		"js:build": "npx tsc && bash build.js.terser.sh",
		"js:dev": "npx tsc --watch",
		"cssjs:build": "npm run css:build && npm run js:build",
		"cssjs:dev": "concurrently \"npm run css:dev\" \"npm run js:dev\"",
		"server": "browser-sync start --proxy localhost/at/ --files './public/custom/**/*.js, ./public/custom/**/*.css, ./**/*.php', ./**/*.html'",
		"dev": "rm -rfv public/custom && concurrently \"npm run cssjs:dev\" \"npm run server\"",
		"build": "npm run cssjs:build"
	},
	"keywords": [],
	"author": "",
	"license": "ISC",
	"dependencies": {
		"@tailwindcss/cli": "^4.2.1",
		"browser-sync": "^3.0.4",
		"concurrently": "^9.2.1",
		"csso": "^5.0.5",
		"tailwindcss": "^4.2.1",
		"terser": "^5.46.0",
		"typescript": "^5.9.3"
	}
}
```

```bash
#!/bin/bash
# create
# find public/custom/js/ -name '*.js' -exec sh -c 'terser "$1" --compress --mangle --output "${1%.js}.min.js"' _ {} \;

# replace
find public/custom/js/ -name '*.js' -exec sh -c 'terser "$1" --compress --mangle --output "${1}.tmp" && mv "${1}.tmp" "$1"' _ {} \;

```

```bash
#!/bin/bash
# create
# find public/custom/css/ -name '*.css' -exec sh -c 'csso "$1" --output "${1%.css}.min.css"' _ {} \;

# replace
find public/custom/css/ -name '*.css' -exec sh -c 'csso "$1" --output "${1}.tmp" && mv "${1}.tmp" "$1"' _ {} \;

```
