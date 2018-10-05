# Ruby from Alpine Linux with OpenSSH

Use this image in your `.gitlab-ci.yml` file:

```yml
deploy:
  stage: deploy
  image: troopers/docker-images:ruby-capistrano-ssh
  before_script:
    - eval "$(ssh-agent -s)"
    - echo "$SSH_PRIVATE_KEY" | ssh-add - > /dev/null
    - mkdir -p ~/.ssh
    - '[[ -f /.dockerenv ]] && echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config'
  environment:
    name: prod
    url: https://example.com
  script:
    - cap prod deploy
  only:
    - master
```
