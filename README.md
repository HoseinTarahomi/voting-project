# voting-project
یک پروژه اپلیکیشن رأی‌گیری ساده که با Docker ساخته شده و برای مدیریت ایمیج‌ها از Nexus و برای CI/CD از GitLab استفاده می‌کند. این پروژه بخشی از مسیر یادگیری من در حوزه DevOps است


| Component               | Description                                                   |
| ----------------------- | ------------------------------------------------------------- |
| Voting app              | Backend + Frontend service — handles voting logic             |
| Database                | A database service (e.g. PostgreSQL / MySQL) to store votes   |
| Nexus                   | Acts as a private Docker registry for storing built images    |
| GitLab CI/CD            | Automated pipelines to build, test, push to Nexus, and deploy |
| Docker / Docker Compose | For containerizing and orchestrating services                 |


🚀 Prerequisites

* Docker
* Docker Compose
* Access to a Nexus registry
* GitLab account (for CI/CD)

🛠️ How to Run Locally

1- Clone the repo:
git clone https://github.com/HoseinTarahomi/voting-project.git
cd voting-project
2- Configure Nexus credentials / registry URL in environment variables or config file (for example in .env)
NEXUS_URL=your-nexus-domain.com
NEXUS_USERNAME=your-username
NEXUS_PASSWORD=your-password

3- Build & push images to Nexus (via Docker Compose or scripts):
docker-compose build
docker-compose push

4- Run the app:
docker-compose up
5- Open in browser: http://localhost:4000
                    http://localhost:4001

این پروژه با GitLab CI/CD به همراه Nexus برای مدیریت ایمیج‌ها و Docker Compose برای دیپلویمنت اتوماتیک پیاده‌سازی شده است. جزئیات در فایل docs/ci-cd.md
