CI:
Dockerbuild: 
    aws ecr login | docker login
    docker build -t ecrRepourl:tag 
    docker push ecrrepourl:tag 
CD:   
kubectl apply -f deployment.yaml services.yaml ingress.yaml 
  
Jenkins 