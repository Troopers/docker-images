## Example of integration with gitlab-ci

```yml
#gitlab-ci.yml
image: troopers/docker-images:ci-victoire

before_script:
  - sh ci/services.sh
  - sh bin/install_test.sh

cache:
    paths:
        - node_modules
        - vendor/

variables:
  SYMFONY__DATABASE_TEST_HOST: 127.0.0.1
  SYMFONY__DATABASE_TEST_USER: root
  SYMFONY__DATABASE_TEST_PASSWORD: ''
  SYMFONY__DATABASE_PASSWORD: ''
  SYMFONY__DATABASE_NAME: dbname_test
  SYMFONY__DATABASE_USER: root
  SYMFONY__NODE_PATH: /usr/bin/node
  SYMFONY__ASSETIC__SASS__BIN: /usr/local/bin/sass
  SYMFONY__VICTOIRE_REDIS_PATH_TEST: redis://127.0.0.1/3
  SYMFONY__SESSION_REDIS_PATH_TEST: redis://127.0.0.1/4
  SYMFONY__ELASTIC_HOST: 127.0.0.1
  SYMFONY__ELASTIC_PORT: '9200'
  SYMFONY__ROUTER__REQUEST_CONTEXT__HOST: 127.0.0.1
  SYMFONY__ROUTER__REQUEST_CONTEXT__SCHEME: http
  SYMFONY__FOS_JS_BASE_URL: http://127.0.0.1
  SYMFONY__MAILER_PORT: '1025'
  SYMFONY__MAILER_HOST: 127.0.0.1

test:
  script:
    - mkdir fails
    - bin/behat -vv
  artifacts:
    paths:
      - fails/
      - var/logs/
    when: on_failure
```
