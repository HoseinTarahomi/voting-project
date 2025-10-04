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

## 🛠️ نحوه اجرا به صورت محلی

1. کلون کردن مخزن:

```bash
git clone https://github.com/HoseinTarahomi/voting-project.git
cd voting-project
```


2. اجرای اپلیکیشن:

```bash
docker-compose up
```

3. دسترسی به اپلیکیشن در مرورگر:

```
http://localhost:4000  # Vote
http://localhost:4001  # Result
```

---

## 📂 توضیحات بیشتر

* پروژه با **GitLab CI/CD** همراه است تا ساخت، تست و دیپلویمنت به صورت خودکار انجام شود.
* مدیریت ایمیج‌ها با **Nexus** انجام می‌شود.