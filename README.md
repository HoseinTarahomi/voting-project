# Voting Project

یک اپلیکیشن رأی‌گیری ساده که با **Docker** ساخته شده و برای مدیریت ایمیج‌ها از **Nexus** و برای CI/CD از **GitLab** استفاده می‌کند. این پروژه بخشی از مسیر یادگیری من در حوزه **DevOps** است.

---

## ساختار پروژه

| Component               | Description                                                   |
| ----------------------- | ------------------------------------------------------------- |
| Voting App              | Backend + Frontend service — handles voting logic             |
| Database                | Database service (PostgreSQL / Redis) to store votes          |
| Nexus                   | Private Docker registry for storing built images              |
| GitLab CI/CD            | Automated pipelines to build, test, push to Nexus, and deploy |
| Docker / Docker Compose | Containerization and orchestration of services                |

---

## 🚀 پیش‌نیازها

* Docker
* Docker Compose
* دسترسی به یک **Nexus registry**
* حساب **GitLab** (برای CI/CD)

---


## ⚙️ GitLab CI/CD

این پروژه شامل یک فایل **`.gitlab-ci.yaml`** است که مراحل **Build** و **Deploy** را خودکارسازی می‌کند.

### Stages

```yaml
stages:
  - build
  - deploy
```

### BuildVote

* مرحله build پروژه است.
* ساخت ایمیج Docker برای سرویس `vote` از مسیر `vote/Dockerfile`.
* تگ کردن ایمیج با commit جاری: `$CI_COMMIT_SHORT_SHA`.
* ورود به رجیستری خصوصی و پوش ایمیج ساخته‌شده:

```yaml
BuildVote:
  stage: build
  tags:
    - build
  script:
    - IMAGE_TAG=$CI_COMMIT_SHORT_SHA
    - docker build -f vote/Dockerfile -t $REGISTRY_URL/$REPO_NAME/vote:$IMAGE_TAG vote/
    - echo $REGISTRY_PASSWORD | docker login $REGISTRY_URL -u $REGISTRY_USERNAME --password-stdin
    - docker push $REGISTRY_URL/$REPO_NAME/vote:$IMAGE_TAG
```

### Deploy

* مرحله deploy پروژه است.
* استفاده از ایمیج ساخته‌شده در مرحله قبل.
* ورود به رجیستری خصوصی.
* کلون کردن ریپوی `docker-compose` روی سرور.
* ایجاد شبکه Docker در صورت عدم وجود.
* اجرای سرویس‌ها با docker-compose:

```yaml
Deploy:
  stage: deploy
  tags:
    - deploy
  script:
    - export VOTE_IMAGE=$REGISTRY_URL/$REPO_NAME/vote:$CI_COMMIT_SHORT_SHA
    - echo $REGISTRY_PASSWORD | docker login $REGISTRY_URL -u $REGISTRY_USERNAME --password-stdin
    - git clone http://root:$GITLAB_TOKEN@192.168.21.51/root/docker-compose.git app
    - cd app
    - docker network inspect myapp || docker network create myapp
    - docker-compose -f vote-compose.yaml up -d
```

---

## 📂 توضیحات بیشتر

* پروژه با **GitLab CI/CD** همراه است تا ساخت، تست و دیپلویمنت به صورت خودکار انجام شود.
* مدیریت ایمیج‌ها با **Nexus** انجام می‌شود.
* پروژه از **PostgreSQL** و **Redis** برای ذخیره‌سازی داده‌ها استفاده می‌کند.
