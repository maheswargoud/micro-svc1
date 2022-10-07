pipeline {
    agent any

    stages {
        stage('Docker Build') {
            steps {
                sh '''
                sudo docker build -t 101275806917.dkr.ecr.ap-southeast-2.amazonaws.com/static-apache:$BUILD_NUMBER .
                # login to ecr 
                aws ecr get-login-password --region ap-southeast-2 | sudo docker login --username AWS --password-stdin 101275806917.dkr.ecr.ap-southeast-2.amazonaws.com
                #push the image to ecr 
                sudo docker push 101275806917.dkr.ecr.ap-southeast-2.amazonaws.com/static-apache:$BUILD_NUMBER
                '''
            }
        }
        stage('EKS Deploy') {
            steps {
                sh '''
                # apply kubectl 
                cd k8s/
                sed -i 's/TAG/$BUILD_NUMBER/g' deployment.yaml
                kubectl apply -f .
                '''

            }
        }
    }
}
