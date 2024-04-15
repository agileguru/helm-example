gcloud auth configure-docker

helm package deployment
helm push joinzoe-deployment-1.0.0.tgz oci://us-central1-docker.pkg.dev/guru-playground/devops-docker

helm package service 
helm push joinzoe-service-1.0.0.tgz oci://us-central1-docker.pkg.dev/guru-playground/devops-docker

helm dependency update ingress
helm package ingress 
helm push joinzoe-ingress-1.0.0.tgz oci://us-central1-docker.pkg.dev/guru-playground/devops-docker

helm fetch oci://us-central1-docker.pkg.dev/guru-playground/devops-docker/joinzoe-ingress --version 1.0.0

helm install joinzoe --dry-run oci://us-central1-docker.pkg.dev/guru-playground/devops-docker/joinzoe-ingress --version 1.0.0
helm install joinzoe oci://us-central1-docker.pkg.dev/guru-playground/devops-docker/joinzoe-ingress --version 1.0.0
