# Oxygen CircleCI Orb [![CircleCI Orb Version](https://img.shields.io/badge/endpoint.svg?url=https://badges.circleci.io/orb/cloudbeat/oxygen)](https://circleci.com/orbs/registry/orb/cloudbeat/oxygen)

The Oxygen CircleCI Orb is a piece of configuration set in your `circle.yml` or `.circleci/config.yml` file to use the Oxygen open source framework to run automated tests on CircleCI with minimal configuration. See this orb in [CircleCI Registry](https://circleci.com/orbs/registry/orb/cloudbeat/oxygen).

## How to Enable

To use CircleCI Orbs in your projects, you need to enable two settings:

- From organization settings allow using uncertified orbs: `Settings -> Security -> Allow uncertified orbs`
- From the project's settings allow beta features: `Settings -> Advanced Settings -> Enable build processing (preview)`

See the official [CircleCI documentation](https://circleci.com/docs/2.0/using-orbs/).

## Examples

Each example below should be placed into `circle.yml` or `.circleci/config.yml` file.

### Test Case

Test case is a single test script, which you can run with Oxygen CircleCI Orb by passing it as `file` parameter.

```yaml
version: 2.1

orbs: 
  oxygen: cloudbeat/oxygen@0.0.2

workflows:
  oxygen_install-start-run-case:
    jobs:
      - oxygen/install-start-run-tests:
          selenium-minor-version: "3.5"
          selenium-patch-version: "3.5.3"
          file: 'tests/testcase1.js'
```

### Test Suite

Test suite is a JSON file, which allows defining and running collection of test cases with Oxygen CircleCI Orb by passing it as `file` parameter.

```yaml
version: 2.1

orbs: 
  oxygen: cloudbeat/oxygen@0.0.2

workflows:
  oxygen_install-start-run-case:
    jobs:
      - oxygen/install-start-run-tests:
          selenium-minor-version: "3.5"
          selenium-patch-version: "3.5.3"
          file: 'tests/testsuite.js'
```

Example of test suite:

```json
{
  "iterations": 2,
  "parallel": 1,
  "url": "http://localhost:4444/wd/hub",
  "cases": [
    {
      "name": "case1",
      "path": "./testcase1.js"
    },
    {
      "name": "case2",
      "path": "./testcase2.js"
    }
  ],
  "environment": {
    "some_parameter": "foo",
    "another_parameter": "bar"
  },
  "capabilities": [
    {
      "browserName": "ie"
    },
    {
      "browserName": "chrome"
    }
  ],
  "options": {
    "autoReopen": true
  }
}
```

## License

This project is licensed under the terms of the [MIT license](/LICENSE.md).