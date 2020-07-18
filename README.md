# homedayTask - Github user fetching

A simple Vue.js application for fetching GitHub user data.

## Solution

- I decided to build the project with Vue to get better acquainted with it (and I'm applying for a position where I'd use it extensively)
- I used Vue CLI to set up the project and built on the structure provided by it
- The only two modules I added are `axios` - for HTTP requests, because it has wider browser support than native `fetch()` and `vue-sessionstorage` for storing recent queries
- Available views: - `/` - Home: root view with search form - `/results/:username` - query result view with user info - `/recent` - a list of recent valid user queries available, stored per session - `/404`

## Installation

#### Project setup

```
npm install
```

#### Compiles and hot-reloads for development

```
npm run serve
```

#### Compiles and minifies for production

```
npm run build
```

#### Run unit tests

```
npm run test:unit
```

#### Lints and fixes files

```
npm run lint
```
