# docker with pip and docker-compose

Use this image in your `.gitlab-ci.yml` file:

```yml
phpunit:
  stage: tests
  image: troopers/docker-images:docker-pip-docker-compose
  variables:
    DOCKER_DRIVER: overlay
  services:
    - docker:dind
  script:
    - docker-compose up -d
```
