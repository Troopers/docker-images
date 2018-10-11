# docker with pip and docker-compose

Use this image in your `.gitlab-ci.yml` file:

```diff
 phpunit:
   stage: tests
-  image: docker:latest
+  image: troopers/docker-images:docker-pip-docker-compose
   script:
-    - apk add --no-cache python py2-pip
-    - pip install --no-cache-dir docker-compose
     - docker-compose up -d
```
