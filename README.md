**Assignment**

**🚀 CI/CD Pipeline – Foundational Implementation**

**📌 Project Overview**

This repository demonstrates a basic end-to-end CI/CD pipeline implemented using GitHub Actions, Docker, and Kubernetes (AWS EKS).

The goal of this project is to showcase CI/CD fundamentals such as automated builds, security checks, artifact handling, containerization, and Kubernetes deployment.

While the original case study is focused on ROS2 Jazzy robotics software, a Java (Maven) application is used here as a demo workload to illustrate the CI/CD flow clearly.

**Note:-** This implementation serves as a starting point and is intentionally kept simple, with clear scope for improvements and extensions.

**🎯 What This Pipeline Demonstrates**

✔ Automated CI trigger on code changes
✔ Consistent build environment
✔ Basic security scans (filesystem & secrets)
✔ Artifact generation and storage
✔ Docker image creation and registry push
✔ Kubernetes-based deployment
✔ Clear separation of CI/CD stages

**🧱 Tools & Technologies Used**

Source Control-->	GitHub
CI/CD Platform-->	GitHub Actions
Build Tool-->	Maven
Language Runtime-->	Java 17
Security Scanning-->	Trivy, Gitleaks
Containerization-->	Docker
Container Registry-->	Docker Hub
Orchestration-->	Kubernetes
Cloud Platform-->	AWS (EKS)

**🔄 CI/CD Workflow Breakdown**

Note:- I Intentinally kept it simple and the improvement areas are clearly mentioned in the documentation — so please don’t judge it too early 😉

1️⃣ Compile Stage

Triggered on push to the release branch
Validates source code compilation using Maven

2️⃣ Security Checks

Basic security checks are performed early in the pipeline:
- Trivy filesystem scan to detect vulnerabilities and misconfigurations
- Gitleaks scan to identify hardcoded secrets
Reports are generated in JSON format and can be reviewed from the pipeline logs.

3️⃣ Build & Artifact Creation

Packages the application using Maven
Uploads the generated JAR as a GitHub Actions artifact
Enables traceability between builds and deployments

4️⃣ Docker Image Build & Push

Downloads the built artifact
Builds a Docker image using a Dockerfile
Pushes the image to Docker Hub

**5️⃣ Kubernetes Deployment- using Tearraform (EKS Cluster Setup)- https://github.com/Sagar7120/EKS_terraform**

Configures AWS credentials and Kubernetes access
Deploys the application to an AWS EKS cluster using a Kubernetes manifest


**📦 Repository Structure**
.
├── .github/
│   └── workflows/
│       └── main.yml
|       └── build.yml
|       └── sast_checkmarx.yml
|       └── sca_cxone.yml
|       └── opa.yml
|       └── variable.yml
|       └── push.yml
├── Dockerfile
├── deployment.yml
├── pom.xml
├── src/
└── README.md

**Note:-** We will be calling out multiple yml files in main file instead of having single main lengthy file. 
I have intentionally kept the deployment.yml file in the same repo. In actual project we will have seperate repos.

**🔐 Secrets Management**

Sensitive information is managed using GitHub Secrets:

DOCKERHUB_USERNAME --> Docker Hub authentication
DOCKERHUB_TOKEN	--> Docker Hub token
AWS_ACCESS_KEY_ID --> AWS access
AWS_SECRET_ACCESS_KEY --> AWS access
EKS_KUBECONFIG --> Kubernetes cluster access

🔧 Scope for Improvements

This project intentionally leaves room for enhancements. Possible improvements include:

**CI Enhancements**

- Integration of Branching strategy and Branch validation rules
- Add unit and integration test stages, For higher environment need to add Performance and Regression testing.
- Parallelize jobs for faster feedback

**Security Enhancements**

- SAST, SCA, OPA (Policy-as-Code) enforcement is pending
- Container image scanning
- SBOM generation
- Image signing and verification
- Dependency vulnerability gating

**Deployment Improvements**

- Helm-based deployments
- Blue-green or canary releases
- Environment-specific deployments
- Rollback strategies

**Monitoring & Observability**

- Centralized logging/Monitoring (Datadog)
- Metrics collection (Prometheus)
- Dashboards (Grafana)
- Alerting and health checks

**Robotics / ROS2 Extension**

- Replace Maven build with colcon build
- Add ROS2 unit and simulation tests
- Build robot-specific runtime images
- Deploy to edge or robotic environments


**👨‍💻 Author**
Sagar Shelki
