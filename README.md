
# Tobius Buildpack: Monorepo

This buildpack converts an individual application within a monorepo into the main Heroku application.

## Usage

1. Add .monorepo file
2. Add Buildpack
3. Add $APP_PATH
4. Push to Heroku

### 1. Add .monorepo file

This buildpack's detect script expects a `.monorepo` file to be found in the project's root folder.

```
[~/yourproject] touch .monorepo
[~/yourproject] git add .monorepo
[~/yourproject] git commit -m 'Support Monorepo Buildpack'
[~/yourproject] git push
```

_Note: The file contents do not matter._

### 2. Add Buildpack

This Monorepo buildpack works by moving the application subfolder up to the root folder level. Since this needs to happen before the application buildpacks are engaged (e.g. Node, Ruby, etc) this buildpack needs to run first.

1. Visit https://dashboard.heroku.com/apps/{YOURAPPNAME}/settings
2. Configure the first buildpack as https://github.com/tobiusventures/tobius-buildpack-monorepo.git

### 3. Add $APP_PATH

Since a Monorepo will presumably have more than one subfolder application you need to tell it which one to use.

1. Visit https://dashboard.heroku.com/apps/{YOURAPPNAME}/settings
2. Set the config var `APP_PATH` to the subfolder application that you want to deploy to this application container.

Example:

```
├── .monorepo
├── README.md
├── backend
│   ├── Procfile
│   ├── index.js
│   └── package.json
├── nested
|   └── api1
|       ├── Procfile
|       ├── index.js
|       └── package.json
└── frontend
│   ├── Procfile
│   ├── index.js
│   └── package.json
```

In the above example `APP_PATH` could be set to `backend`, `nested/api1` or `frontend`.

### 4. Push to Heroku

Your Monorepo subfolder application is now configured to run inside your Heroku application. Push it as you would any other.

## LICENSE

MIT

