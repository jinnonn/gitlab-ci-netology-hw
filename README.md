### Задание 1

**Что нужно сделать:**

1. Разверните GitLab локально, используя Vagrantfile и инструкцию, описанные в [этом репозитории](https://github.com/netology-code/sdvps-materials/tree/main/gitlab).   
2. Создайте новый проект и пустой репозиторий в нём.
3. Зарегистрируйте gitlab-runner для этого проекта и запустите его в режиме Docker. Раннер можно регистрировать и запускать на той же виртуальной машине, на которой запущен GitLab.

В качестве ответа в репозиторий шаблона с решением добавьте скриншоты с настройками раннера в проекте.

---

### Решение 1

![image](https://github.com/jinnonn/gitlab-ci-netology-hw/assets/146999555/41ee813d-6d60-4384-b910-471840d04e27)
![image](https://github.com/jinnonn/gitlab-ci-netology-hw/assets/146999555/ea7ca6a0-6d87-4d91-8c1b-0573e20766f7)
![image](https://github.com/jinnonn/gitlab-ci-netology-hw/assets/146999555/b5f9a527-ed52-4f16-886c-3829db77d3c0)

---

### Задание 2

**Что нужно сделать:**

1. Запушьте [репозиторий](https://github.com/netology-code/sdvps-materials/tree/main/gitlab) на GitLab, изменив origin. Это изучалось на занятии по Git.
2. Создайте .gitlab-ci.yml, описав в нём все необходимые, на ваш взгляд, этапы.

В качестве ответа в шаблон с решением добавьте: 
   
 * файл gitlab-ci.yml для своего проекта или вставьте код в соответствующее поле в шаблоне; 
 * скриншоты с успешно собранными сборками.
 
---

Содержимое gitlab-ci.yml
```
stages:
  - test
  - static-analysis
  - build

test:
  stage: test
  image: golang:1.16
  script: 
   - go test .

static-analysis:
 stage: test
 image:
  name: sonarsource/sonar-scanner-cli
  entrypoint: [""]
 variables:
 script:
  - sonar-scanner -Dsonar.projectKey=checkeray -Dsonar.sources=. -Dsonar.host.url=http://51.250.102.151:9000 -Dsonar.login=sqp_d7488143f45cd61c4d8de98b972ddf49ab52f910

build:
  stage: build
  image: docker:latest
  script:
   - docker build . --tag gitlab-ci:latest
```
Скриншоты:
![image](https://github.com/jinnonn/gitlab-ci-netology-hw/assets/146999555/7bb5db41-49c8-4508-948d-58c0672e2bca)
![image](https://github.com/jinnonn/gitlab-ci-netology-hw/assets/146999555/be51d2a0-f564-473b-b157-5366aa0e44c9)
