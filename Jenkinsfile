pipeline {
    agent any

    stages {
        stage('Docker Build') {
            steps {
                sh '''
                docker build -t 101275806917.dkr.ecr.ap-southeast-2.amazonaws.com/static-apache:$BUILD_NUMBER .
                # login to ecr 
                aws ecr get-login-password --region ap-southeast-1 | sudo docker login --username AWS --password-stdin 101275806917.dkr.ecr.ap-southeast-1.amazonaws.com
                #push the image to ecr 
                docker push 101275806917.dkr.ecr.ap-southeast-2.amazonaws.com/static-apache:$BUILD_NUMBER
                '''
            }
        }
        stage('EKS Deploy') {
            steps {
                sh '''
                # apply kubectl 
                kubectl apply -f ns.yaml deployment.yaml service.yaml ingress.yaml 
                '''

            }
        }
    }
}
