# vue-sentinel

vue-sentinel is an authentication and authorization libary that comes with
_some_ batteries included, but gets out of your way when you need it to.

It makes it quick and easy to implement _login, logout, and access control_ in
vue js applications.

Note that vue-sentinel has **not** been tested with universal (server-side rendered)
apps. If you would like to help with this please see [contributions](#contributions)
for how to do it.

## Installation
To install vue-sentinel in your app:
```
npm install -s vue-sentinel
```
## Usage
### Setup
Vue-sentinel works as a vuejs plugin. So you set it up in the  application
entrypoint (main.js) like so:
```javascript
import Vue from 'vue'
import Sentinel from 'vue-sentinel'

// An built in authentication strategy we'll use later
import Local from 'vue-sentinel/authentication'

Vue.use(Sentinel, {
  /**
  * Sentinel has a pluggable  authentication system. You can choose one of the built-in
  * strategies or a custom authentication strategy.
  */
  authentication: Local({local strategy config goes here}),

  /**
  * Sentinel uses authorization strategies. It's default authorization strategy 
  * depends on [ casl ](https://stalniy.github.io/casl/)
  */
  authorization: {}, // a custom authorization strategy (optional),

  /**
  * the routes to redirect to when specific conditions occur.
  */
  routes: { 
    /*
    * Route to redirect to when a user has not yet logged in but is trying to
    * access a route that requires authorization.
    */
    'unauthenticated': '/login',

    /*
    * Route to redirect to when a user is not authorized for the action they are
    * attempting to take
    */
    'unauthorizaed': '/403' 	
  }
})
```
### Login
vue-sentinel makes no assumption about your UI components. You invoke the login
function in response to some user action in a UI component like so:
```vue
<template>
	<div>
		<input type="" v-model="username">
		<input type="" v-model="password+">
		<button @click="loginWithPassword()">Login with password</button>
		<button @click="loginWithFacebook()">Login with Facebook</button>
		<button @click="loginWithGithub()">Login with Github</button>
	</div>
</template>
<script>
export default {
  data {
    return {
      username: '',
      password: ''
    }
  },
  methods {
    loginWithPassword () {
      this.$sentinel.login('local', this.username, this.password)
        .then(() => {})
	.catch(err => {})
    },
    loginWithFacebook () {
      this.$sentinel.login('facebook')
        .then(() => {})
	.catch(err => {})
    },
    loginWithGithub () {
      this.$sentinel.login('github')
        .then(() => {})
	.catch(err => {})
    }
}
</script>
```
### Logout
Similarly, logout in response to some user action like so:
```vue
<template>
	<div>
		<ul>
			<li>Action 1</li>
			<li>Action 2</li>
			<li><button @click="logut">Logout</button></li>
		</ul>
	</div>
</template>
<script>
export default {
  data {
    return {}
  },
  methods {
    logout () {
      this.$sentinel.logout()
}
</script>
```
### Route protection

## More documentation
See the[ guide ](docs/guide.html)

## Contributing
Pull requests are welcome. For major changes, please open an issue first to
discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](/LICENSE)
