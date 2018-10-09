## Example of integration with GitLab CI

1. Declare services that you need in `gitlab-ci.yml`:

    ```yml
    image: troopers/docker-images:2018.08
    
    variables:
      # binaries for front
      SYMFONY__NODE_PATH: /usr/bin/node
      SYMFONY__ASSETIC__SASS__BIN: /usr/local/bin/sass
      # mysql
      SYMFONY__DATABASE_HOST: mysql
      SYMFONY__DATABASE_TEST_USER: root
      SYMFONY__DATABASE_TEST_PASSWORD: ''
      SYMFONY__DATABASE_TEST_NAME: test
      MYSQL_ROOT_PASSWORD: ''
      MYSQL_ALLOW_EMPTY_PASSWORD: 'true'
      MYSQL_DATABASE: test
      # redis
      SYMFONY__VICTOIRE_REDIS_PATH_TEST: redis://redis/3
      SYMFONY__SESSION_REDIS_PATH_TEST: redis://redis/4
      # elastic
      SYMFONY__ELASTIC_HOST: elasticsearch
      SYMFONY__ELASTIC_PORT: '9200'
      # mailcatcher
      SYMFONY__MAILER_HOST: mailcatcher
      SYMFONY__MAILER_PORT: '1025'
      # rabbitmq
      RABBITMQ_DEFAULT_USER: guest
      RABBITMQ_DEFAULT_PASS: guest
      RABBITMQ_DEFAULT_VHOST: '/dev/'
    
    test:
      services:
        - mysql:5.7
        - redis:3.2
        - elasticsearch:2.3
        - name: yappabe/mailcatcher:latest
          alias: mailcatcher
        - rabbitmq:3
      # …
    ```

    The prefix `SYMFONY__` is required for [Symfony 2.8](https://symfony.com/doc/2.8/configuration/external_parameters.html)
    and has to be removed for [Symfony 3.4+](https://symfony.com/doc/3.4/configuration/external_parameters.html).

2. Update host of mailcatcher in the `behat.yml.dist` file:

    ```yml
    default:
        extensions:
            Alex\MailCatcher\Behat\MailCatcherExtension\Extension:
                url: http://mailcatcher:1080
                purge_before_scenario: true
    ```
3. Launch Selenium before tests:

    ```shell
    Xvfb :99 -ac &
    export DISPLAY=:99
    nohup java -jar /selenium-server-standalone-2.53.0.jar 2> /dev/null > /dev/null &
    ```
