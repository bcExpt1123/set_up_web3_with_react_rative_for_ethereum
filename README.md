# How to set up web3.js with CRNA

This is a simple guide to get you started with using the `Ethereum Javascript API` ([web3.js](https://github.com/ethereum/web3.js/)) with the `Create React Native App` project. This is not an in-depth guide.

### TL;DR
If you are lazy and just want to get started, I have [this project](https://github.com/dougbacelar/react-native-web3) ready for you. It should **work out-of-the-box**.

### Installation guide
1. Make sure you have Node version 6 or later installed, if not, get it on the [Node website](http://nodejs.org/)

	`node --version`
    
    
2. Install [Create React Native App](https://github.com/react-community/create-react-native-app)

	`npm install -g create-react-native-app`
    

3. Use create-react-native-app to create the project boilerplate

	`create-react-native-app my-app`

4. Install [node-libs-browser](https://github.com/webpack/node-libs-browser)
	
    `npm install --save node-libs-browser`


5. Create a file called *rn-cli.config.js* on the root of the project and add the following code into it:
	
    ```javascript
   	const extraNodeModules = require('node-libs-browser');
    
   	module.exports = {
   	  extraNodeModules,
   	};
	```

6. Create a file called *global.js* on the root of the project and add the following code into it:

	```javascript
    // Inject node globals into React Native global scope.
	global.Buffer = require('buffer').Buffer;
	global.process = require('process');
	
	if (typeof btoa === 'undefined') {
	  global.btoa = function (str) {
	    return new Buffer(str, 'binary').toString('base64');
	  };
	}

	if (typeof atob === 'undefined') {
	  global.atob = function (b64Encoded) {
	    return new Buffer(b64Encoded, 'base64').toString('binary');
	  };
	}

	```
    
7. Import the *global.js* file into your *[App.js]()* file
	
    ```javascript
   	import './global';
   	```
    
8. Install [babel-preset-es2015](https://www.npmjs.com/package/babel-preset-es2015)
	
	`npm install --save-dev babel-cli babel-preset-es2015`
    
9. Now we can install the [web3.js api](https://github.com/ethereum/web3.js/) 

	`npm install --save web3`
    

10. Require the API in your `App.js` file

	```javascript
    const Web3 = require('web3');
   	```

11. Add the following code inside your React component in `App.js` to get started with consuming the API. The code will print information of the latest block on the console.

	```javascript
    componentWillMount() {
      const web3 = new Web3(
        new Web3.providers.HttpProvider('https://mainnet.infura.io/')
      );

      web3.eth.getBlock('latest').then(console.log)
    }
	```
    
12. Test it

	`npm start`
    
    or
    
	`npm run ios`
    
    or
    
    `npm run android`

For more examples on the API usage, visit the [web3.js documentation](https://github.com/ethereum/wiki/wiki/JavaScript-API).

For a project with all this setup ready, check out [my repo](https://github.com/dougbacelar/react-native-web3).
