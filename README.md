Travis CI Template
========

To use this template copy it and change the parts as you need it.


requirements
--------
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
settings
--------
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

path to your test folder:
```
.Build/bin/phpunit -c .Build/vendor/nimut/testing-framework/res/Configuration/UnitTests.xml Tests/Classes/
```