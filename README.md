# example-ci

`store_test_results` uploads the JUnit test metadata from the `build/test-results/test` directory so that it can show up in the CircleCI dashboard.

`store_artifacts` upload the test metadata as artifacts in case there is a need to examine them. 

```
  - store_test_results:
      path: build/test-results/test
  - store_artifacts:
      path: build/test-results/test
      when: always
```



```
  - slack/status:
    fail_only: true
    mentions: 'U014CSLUYF5,U01485RM66P'
    only_for_branches: 'master'
    webhook: '${SLACK_WEBHOOK}'
    channel: 'C013T77J5HV'
```



```
orbs:
  slack: circleci/slack@3.4.2
```

```
orbs:
  heroku: circleci/heroku@1.0.1
```

```
jobs:
  - build
  - heroku/deploy-via-git:
    requires:
      - build
    filters:
      branches:
        only: master
```

```
workflows:
    version: 2.1
    workflow:
        jobs:
            - build
            - heroku/deploy-via-git:
                requires:
                    - build
                filters:
                    branches:
                        only: master
```