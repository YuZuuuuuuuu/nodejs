
#Pipeline CI/CD Node.js avec Docker, Trivy, AWS

Ce projet illustre la mise en place d'une chaîne DevSecOps avec l'intégration de l'application Node.Js. Celui-cu intègre l'automatisation des tests, la conteneurisation, l'analyse de sécurité et le déploiement sur une infrastructure sécurisé aws.

#Architecture globale

Le pipeline suit le flux suivant :
flowchart LR
    Dev -->|Push| GitHub
    subgraph CI_CD_Pipeline [GitHub Actions]
        Test[Build & Test NPM] --> Docker[Build & Push Image]
        Docker --> Security[Scan Trivy]
    end
    subgraph Infrastructure [AWS & Terraform]
        Terraform -->|Provisionning| EC2[Instance EC2]
        SG[Security Group] --> EC2
    end
    GitHub --> CI_CD_Pipeline
    Security -->|Image Validée| Hub[Docker Hub]
    Hub -->|Docker Pull| EC2
