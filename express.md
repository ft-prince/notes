Express cheat list
===

[![NPM version](https://img.shields.io/npm/v/express.svg?style=flat)](https://npmjs.org/package/express)
[![Downloads](https://img.shields.io/npm/dm/express.svg?style=flat)](https://www.npmjs.com/package/express)
[![Repo Dependents](https://badgen.net/github/dependents-repo/expressjs/express)](https://github.com/expressjs/express/network/dependents)
[![Github repo](https://badgen.net/badge/icon/Github?icon=github&label)](https://github.com/expressjs/express)

This is a fast, eclectic, minimalist web framework for Node.js, including an API reference list and some examples for [Express.js](http://expressjs.com/)
<!--rehype:style=padding-top: 12px;-->

getting Started
---

### Hello World
<!--rehype:wrap-class=row-span-2-->

- Create a project and add `package.json` configuration

  ```bash
  $ mkdir myapp # Create directory
  $ cd myapp # Enter directory
  $ npm init -y # Initialize a configuration
  ```

- Install dependencies

  ```bash
  $ npm install express # Install dependencies
  ```

- Add code to the entry file `index.js`:

  ```js
  const express = require('express')
  const app = express()
  const port = 3000
  app.get('/', (req, res) => {
    res.send('Hello World!')
  })
  app.listen(port, () => {
    console.log(`Listening port ${port} example application`)
  })
  ```

- Run the application using the following command

  ```bash
  $ node index.js
  ```
<!--rehype:className=style-timeline-->

### express -h
<!--rehype:wrap-class=row-span-2-->

```bash
Usage: express [options] [dir]
Options:
  -h, --help output usage information
      --version output version number
  -e, --ejs add ejs engine support
      --hbs Add hbs engine support
      --pug Add pug engine support
  -H, --hogan add hogan.js engine support
      --no-view No view engine generated
  -v, --view <engine> Add view <engine> support (ejs|hbs|hjs|jade|pug|twig|vash) (default jade)
  -c, --css <engine> Add style sheet <engine> support (less|stylus|compass|sass) (default css)
      --git add .gitignore
  -f, --force force non-empty directory
```
<!--rehype:className=wrap-text -->

Create a `myapp` project

```bash
$ express --view=pug myapp
# Run the application
$ DEBUG=myapp:* npm start
```

### express()

:- | :-
:- | :-
`express.json()` | [#](http://expressjs.com/en/4x/api.html#express.json)
`express.raw()` | [#](http://expressjs.com/en/4x/api.html#express.raw)
`express.Router()` | [#](http://expressjs.com/en/4x/api.html#express.router)
`express.static()` | [#](http://expressjs.com/en/4x/api.html#express.static)
`express.text()` | [#](http://expressjs.com/en/4x/api.html#express.text)
`express.urlencoded()` | [#](http://expressjs.com/en/4x/api.html#express.urlencoded)

### Router

:- | :-
:- | :-
`router.all()` | [#](http://expressjs.com/en/4x/api.html#router.all)
`router.METHOD()` | [#](http://expressjs.com/en/4x/api.html#router.METHOD)
`router.param()` | [#](http://expressjs.com/en/4x/api.html#router.param)
`router.route()` | [#](http://expressjs.com/en/4x/api.html#router.route)
`router.use()` | [#](http://expressjs.com/en/4x/api.html#router.use)

### Application

```js
var express = require('express')
var app = express()

console.dir(app.locals.title)
// => 'My App'
console.dir(app.locals.email)
// => 'me@myapp.com'
```

#### **Attributes**

:- | :-
:- | :-
`app.locals` | Local variables in the application[#](http://expressjs.com/en/4x/api.html#app.locals)
`app.mountpath` | Path pattern for installing sub-applications[#](http://expressjs.com/en/4x/api.html#app.mountpath)

#### **Events**

:- | :-
:- | :-
`mount` | The child application is mounted to the parent application, and the event is triggered on the child application [#](http://expressjs.com/en/4x/api.html#app.onmount)

#### **method**

:- | :-
:- | :-
`app.all()` | [#](http://expressjs.com/en/4x/api.html#app.all)
`app.delete()` | [#](http://expressjs.com/en/4x/api.html#app.delete.method)
`app.disable()` | [#](http://expressjs.com/en/4x/api.html#app.disable)
`app.disabled()` | [#](http://expressjs.com/en/4x/api.html#app.disabled)
`app.enable()` | [#](http://expressjs.com/en/4x/api.html#app.enable)
`app.enabled()` | [#](http://expressjs.com/en/4x/api.html#app.enabled)
`app.engine()` | [#](http://expressjs.com/en/4x/api.html#app.engine)
`app.get(name)` | [#](http://expressjs.com/en/4x/api.html#app.get)
`app.get(path, callback)` | [#](http://expressjs.com/en/4x/api.html#app.get.method)
`app.listen()` | [#](http://expressjs.com/en/4x/api.html#app.listen)
`app.METHOD()` | [#](http://expressjs.com/en/4x/api.html#app.METHOD)
`app.param()` | [#](http://expressjs.com/en/4x/api.html#app.param)
`app.path()` | [#](http://expressjs.com/en/4x/api.html#app.path)
`app.post()` | [#](http://expressjs.com/en/4x/api.html#app.post.method)
`app.put()` | [#](http://expressjs.com/en/4x/api.html#app.put.method)
`app.render()` | [#](http://expressjs.com/en/4x/api.html#app.render)
`app.route()` | [#](http://expressjs.com/en/4x/api.html#app.route)
`app.set()` | [#](http://expressjs.com/en/4x/api.html#app.set)
`app.use()` | [#](http://expressjs.com/en/4x/api.html#app.use)

### Request

#### Attributes

:- | :-
:- | :-
`req.app` | [#](http://expressjs.com/en/4x/api.html#req.app)
`req.baseUrl` | [#](http://expressjs.com/en/4x/api.html#req.baseUrl)
`req.body` | [#](http://expressjs.com/en/4x/api.html#req.body)
`req.cookies` | [#](http://expressjs.com/en/4x/api.html#req.cookies)
`req.fresh` | [#](http://expressjs.com/en/4x/api.html#req.fresh)
`req.hostname` | [#](http://expressjs.com/en/4x/api.html#req.hostname)
`req.ip` | [#](http://expressjs.com/en/4x/api.html#req.ip)
`req.ips` | [#](http://expressjs.com/en/4x/api.html#req.ips)
`req.method` | [#](http://expressjs.com/en/4x/api.html#req.method)
`req.originalUrl` | [#](http://expressjs.com/en/4x/api.html#req.originalUrl)
`req.params` | [#](http://expressjs.com/en/4x/api.html#req.params)
`req.path` | [#](http://expressjs.com/en/4x/api.html#req.path)
`req.protocol` | [#](http://expressjs.com/en/4x/api.html#req.protocol)
`req.query` | [#](http://expressjs.com/en/4x/api.html#req.query)
`req.route` | [#](http://expressjs.com/en/4x/api.html#req.route)
`req.secure` | [#](http://expressjs.com/en/4x/api.html#req.secure)
`req.signedCookies` | [#](http://expressjs.com/en/4x/api.html#req.signedCookies)
`req.stale` | [#](http://expressjs.com/en/4x/api.html#req.stale)
`req.subdomains` | [#](http://expressjs.com/en/4x/api.html#req.subdomains)
`req.xhr` | [#](http://expressjs.com/en/4x/api.html#req.xhr)

#### method

:- | :-
:- | :-
`req.accepts()` | [#](http://expressjs.com/en/4x/api.html#req.accepts)
`req.acceptsCharsets()` | [#](http://expressjs.com/en/4x/api.html#req.acceptsCharsets)
`req.acceptsEncodings()` | [#](http://expressjs.com/en/4x/api.html#req.acceptsEncodings)
`req.acceptsLanguages()` | [#](http://expressjs.com/en/4x/api.html#req.acceptsLanguages)
`req.get()` | Get HTTP request header field[#](http://expressjs.com/en/4x/api.html#req.get)
`req.is()` | [#](http://expressjs.com/en/4x/api.html#req.is)
`req.param()` | [#](http://expressjs.com/en/4x/api.html#req.param)
`req.range()` | [#](http://expressjs.com/en/4x/api.html#req.range)

### Response

```js
app.get('/', function (req, res) {
  console.dir(res.headersSent) // false
  res.send('OK')
  console.dir(res.headersSent) // true
})
```

#### Attributes

:- | :-
:- | :-
`res.app` | [#](http://expressjs.com/en/4x/api.html#res.app)
`res.headersSent` | [#](http://expressjs.com/en/4x/api.html#res.headersSent)
`res.locals` | [#](http://expressjs.com/en/4x/api.html#res.locals)

#### method

:- | :-
:- | :-
`res.append()` | [#](http://expressjs.com/en/4x/api.html#res.append)
`res.attachment()` | [#](http://expressjs.com/en/4x/api.html#res.attachment)
`res.cookie()` | [#](http://expressjs.com/en/4x/api.html#res.cookie)
`res.clearCookie()` | [#](http://expressjs.com/en/4x/api.html#res.clearCookie)
`res.download()` | Prompt for the file to be downloaded[#](http://expressjs.com/en/4x/api.html#res.download)
`res.end()` | End the response process[#](http://expressjs.com/en/4x/api.html#res.end)
`res.format()` | [#](http://expressjs.com/en/4x/api.html#res.format)
`res.get()` | [#](http://expressjs.com/en/4x/api.html#res.get)
`res.json()` | Send JSON response[#](http://expressjs.com/en/4x/api.html#res.json)
`res.jsonp()` | Send response with JSONP support[#](http://expressjs.com/en/4x/api.html#res.jsonp)
`res.links()` | [#](http://expressjs.com/en/4x/api.html#res.links)
`res.location()` | [#](http://expressjs.com/en/4x/api.html#res.location)
`res.redirect()` | Redirect request[#](http://expressjs.com/en/4x/api.html#res.redirect)
`res.render()` | Render view template[#](http://expressjs.com/en/4x/api.html#res.render)
`res.send()` | Send various types of responses[#](http://expressjs.com/en/4x/api.html#res.send)
`res.sendFile()` | Send file as octet stream[#](http://expressjs.com/en/4x/api.html#res.sendFile)
`res.sendStatus()` | [#](http://expressjs.com/en/4x/api.html#res.sendStatus)
`res.set()` | [#](http://expressjs.com/en/4x/api.html#res.set)
`res.status()` | [#](http://expressjs.com/en/4x/api.html#res.status)
`res.type()` | [#](http://expressjs.com/en/4x/api.html#res.type)
`res.vary()` | [#](http://expressjs.com/en/4x/api.html#res.vary)

Example
----

### Router
<!--rehype:wrap-class=row-span-2-->

Called for any request passed to this router

```js
router.use(function (req, res, next) {
  // .. there is some logic here.. like any other middleware
  next()
})
```

Any request ending with `/events` will be processed

```js
// Depends on where the router is "use()"
router.get('/events', (req, res, next) => {
  // ..
})
```

### Response

The `res` object represents the HTTP response sent by the `Express` application when it receives an HTTP request.

```js
app.get('/user/:id', (req, res) => {
  res.send('user ' + req.params.id)
})
```

### Request

The `req` object represents an `HTTP` request and has properties such as the request query string, parameters, body, HTTP headers, etc.

```js
app.get('/user/:id', (req, res) => {
  res.send('user ' + req.params.id)
})
```

### res.end()

```js
res.end()
res.status(404).end()
```

End the response process. This method actually comes from the core of Node, specifically the `response.end()` method of `http.ServerResponse`

### res.json([body])

```js
res.json(null)
res.json({ user: 'tobi' })
res.status(500).json({ error: 'message' })
```

### app.all

```js
app.all('/secret', function (req, res, next) {
  console.log('Access secret part...')
  next() // Pass control to the next handler
})
```

### app.delete

```js
app.delete('/', function (req, res) {
  res.send('DELETE request to homepage')
})
```

### app.disable(name)

```js
app.disable('trust proxy')
app.get('trust proxy')
// => false
```

### app.disabled(name)

```js
app.disabled('trust proxy')
// => true

app.enable('trust proxy')
app.disabled('trust proxy')
// => false
```

### app.engine(ext, callback)

```js
var engines = require('consolidate')

app.engine('haml', engines.haml)
app.engine('html', engines.hogan)
```

### app.listen([port[, host[, backlog]]][, callback])

```js
var express = require('express')

var app = express()
app.listen(3000)
```

### Routing

```js
const express = require('express')
const app = express()

//Respond to "hello world" when making a GET request to the homepage
app.get('/', (req, res) => {
  res.send('hello world')
})
```

```js
// GET method routing
app.get('/', (req, res) => {
  res.send('GET request to the homepage')
})

// POST method routing
app.post('/', (req, res) => {
  res.send('POST request to the homepage')
})
```

### middleware

```js
function logOriginalUrl (req, res, next) {
  console.log('ReqURL:', req.originalUrl)
  next()
}

function logMethod (req, res, next) {
  console.log('Request Type:', req.method)
  next()
}

const log = [logOriginalUrl, logMethod]

app.get('/user/:id', log,
  (req, res, next)=>{
    res.send('User Info')
  }
)
```

### Use templates

```js
app.set('view engine', 'pug')
```

Create a `Pug` template file named `index.pug` in the `views` directory with the following content

```pug
html
  head
    title= title
  body
    h1= message
```

Create a route to render the `index.pug` file. If the view engine property is not set, the view file extension must be specified

```js
app.get('/', (req, res) => {
  res.render('index', {
    title: 'Hey', message: 'Hello there!'
  })
})
```
