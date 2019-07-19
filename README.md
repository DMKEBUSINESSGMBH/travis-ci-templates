# Travis CI Template

To use this template you have to copy the .travis.yml and the phpunit.xml.dist into your project. Also you have to add the requirements down below.
In the .travis.yml you can change the php and typo3 version you want to test. 
In the phpunit.xml.dist you can change the test and src folder to match to your extension.

## requirements

You have to change the path to match your extension mktools is just the example
```
    "require-dev": {
        "nimut/testing-framework": "^4.0"
    },
    "config": {
        "vendor-dir": ".Build/vendor",
        "bin-dir": ".Build/bin",
        "preferred-install": {
            "typo3/cms": "source"
        }
    },
    "scripts": {
        "post-autoload-dump": [
            "mkdir -p .Build/Web/typo3conf/ext/",
            "[ -L .Build/Web/typo3conf/ext/mktools ] || ln -snvf ../../../../. .Build/Web/typo3conf/ext/mktools"
        ]
    },
    "extra": {
        "typo3/cms": {
            "cms-package-dir": "{$vendor-dir}/typo3/cms",
            "web-dir": ".Build/Web"
        }
    }
```
## settings

### .travis.yml

php versions that are used:
```
php:
   - 7.0
   - 7.1
   - 7.2
   - 7.3
```

typo3 versions that are used:
```
env:
  - TYPO3_VERSION="^8.7.0"
  - TYPO3_VERSION="^9.5.0"
```

excludes of the combination of php version and typo 3 version:
```
matrix:
  exclude:
    - php: 7.0
      env: TYPO3_VERSION="^9.5.0"
    - php: 7.1
      env: TYPO3_VERSION="^9.5.0"
```

### phpunit.xml.dist.yml

path to your test folder:
```
    <testsuites>
        <testsuite name="MK Postman Unit Tests">
            <directory>Tests/Unit/</directory>
        </testsuite>
    </testsuites>
```
path to your src folder:
```
    <filter>
        <whitelist processUncoveredFilesFromWhitelist="true">
            <directory suffix=".php">Classes</directory>
        </whitelist>
    </filter>
```
This define your Classes that are used to generate the code coverage. In some old projects you might have a structure like this:
```
<whitelist processUncoveredFilesFromWhitelist="true">
    <directory suffix=".php">./actions</directory>
    <directory suffix=".php">./controllers</directory>
    <directory suffix=".php">./exceptions</directory>
    <directory suffix=".php">./hooks</directory>
    <directory suffix=".php">./models</directory>
    <directory suffix=".php">./search</directory>
    <directory suffix=".php">./util</directory>
    <directory suffix=".php">./Classes</directory>
    <directory suffix=".php">./marker</directory>
    <directory suffix=".php">./view</directory>
    <directory suffix=".php">./interface</directory>
    <directory suffix=".php">./indexer</directory>
</whitelist>
```