Travis CI Template
========

To use this template copy it and change the parts as you need it.

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