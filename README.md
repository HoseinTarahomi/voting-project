# Voting Project

یک اپلیکیشن رأی‌گیری ساده که با **Docker** ساخته شده و برای مدیریت ایمیج‌ها از **Nexus** و برای CI/CD از **GitLab** استفاده می‌کند. این پروژه بخشی از مسیر یادگیری من در حوزه **DevOps** است.

---

## ساختار پروژه

| Component               | Description                                                   |
| ----------------------- | ------------------------------------------------------------- |
| Voting App              | Backend + Frontend service — handles voting logic             |
| Database                | Database service (PostgreSQL / MySQL) to store votes          |
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

2. پیکربندی دسترسی به Nexus (در فایل `.env` یا متغیرهای محیطی):

```bash
NEXUS_URL=your-nexus-domain.com
NEXUS_USERNAME=your-username
NEXUS_PASSWORD=your-password
```

3. ساخت و پوش ایمیج‌ها به Nexus:

```bash
docker-compose build
docker-compose push
```

4. اجرای اپلیکیشن:

```bash
docker-compose up
```

5. دسترسی به اپلیکیشن در مرورگر:

```
http://localhost:4000  # Frontend
http://localhost:4001  # Backend / API
```

---

## 📂 توضیحات بیشتر

* پروژه با **GitLab CI/CD** همراه است تا ساخت، تست و دیپلویمنت به صورت خودکار انجام شود.
* مدیریت ایمیج‌ها با **Nexus** انجام می‌شود.