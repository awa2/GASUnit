[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

# GASUnit
Testing library for Google Apps Script.
Result will be logged to Logger, or posted to Slack.
You can use **Exports** style to write tests (for now).

## Usage
### Add library
project key: `MSnMmw8hLWgjUG6uKSTQBEzVZgzu5bsVr`

### Write tests
#### Exports style
Exports style is inspired by [Mocha](https://mochajs.org/#exports).

##### Use Logger
```js
var exports = GASUnit.exports
var assert = GASUnit.assert

function test_array () {
  exports({
    'Array': {
      '#indexOf()': {
        'should return -1 when not present': function () {
          assert([1, 2, 3].indexOf(4) === -1)
        },
        'should return the index when present': function () {
          assert([1, 2, 3].indexOf(3) === 3)
        }
      }
    }
  })
}
```

##### Use Slack
```js
var exports = GASUnit.slack('https://...').exports
var assert = GASUnit.assert

function test_array () {
  exports({
    'Array': {
      '#indexOf()': {
        'should return -1 when not present': function () {
          assert([1, 2, 3].indexOf(4) === -1)
        },
        'should return the index when present': function () {
          assert([1, 2, 3].indexOf(3) === 3)
        }
      }
    }
  })
}
```

If you're publishing source code, should **not** write webhook url as a literal.
You can use properties as environment variables.

```js
var exports = GASUnit.slack(PropertiesService.getScriptProperties().getProperty('WEBHOOK_URL')).exports
var assert = GASUnit.assert

function test_array () {
  exports({
    'Array': {
      '#indexOf()': {
        'should return -1 when not present': function () {
          assert([1, 2, 3].indexOf(4) === -1)
        },
        'should return the index when present': function () {
          assert([1, 2, 3].indexOf(3) === 3)
        }
      }
    }
  })
}
```

## Assertion
GASUnit provides minimum assert function which verify whether value is truthy.
You can add any assertion library and use it.

## Development

```sh
# install dependencies
$ npm install

# lint code by ESLint
$ npm run lint

# lint and fix code by ESLint
$ npm run lint:fix

# login to Google Drive
$ npm run login

# logout from Google Drive
$ npm run logout

# pull code from Google Drive
$ npm run pull

# push code to Google Drive
$ npm run push

# open project page on Google Drive
$ npm run open
```
