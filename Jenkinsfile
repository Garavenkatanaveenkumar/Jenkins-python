pipeline {
    agent any
     environment {
    DOCKERHUB_CREDENTIALS = credentials('e96d2081-ffd4-4ae3-9551-d0355b47f92d')
    }
    stages {
        stage('gitclone') {
            steps {
                git credentialsId: 'cd366127-54ec-4215-b962-902cedf32f97', url: 'https://github.com/Garavenkatanaveenkumar/Jenkins-python.git'
            }
        }
        stage ('Test'){
                steps {
                sh "pytest testRoutes.py"
                }
        }
        stage('Build') {
            steps {
             sh 'docker build -t python .'
            }
        }
        stage('login to dockerhub') {
            steps {
             sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                
            }
        }
         
        stage('push image to docker hub') {
            steps{
                sh '''
                docker tag local-image:tagname new-repo:tagname
                docker push new-repo:tagname
                '''
            }
        }
        
        stage('run') {
            steps {
             sh 'docker run -d -p 5000:5000 <IMAGE_NAME >'
            }
        }
        
        }
}


        
