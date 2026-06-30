pipeline {
    agent any
    stages {
        stage('Pull') {
            steps {
                git branch: 'main', url: 'https://github.com/sakshigawale2112/jenkins-pipeline-scripts.git'
                //
            }
        }
        stage('Build') {
            steps {
                sh '''cd backend 
                    mvn clean package -DskipTests'''
                
            }
        }
        
        stage('Test') {
            steps {
                 withSonarQubeEnv(credentialsId: 'secret-cred') {
                     sh '''cd backend
                   mvn sonar:sonar -Dsonar.projectkey=studentapp'''
                     }
             }       
    }

       
        stage('Quality Gate') {
            steps {
                timeout(10) {
                waitForQualityGate abortPipeline: true, credentialsId: 'secret-cred'

                //
            }
        }


        stage('Delivery') {
            steps {
                echo "Deploy Success"
                //
            }
        }


    }
}



