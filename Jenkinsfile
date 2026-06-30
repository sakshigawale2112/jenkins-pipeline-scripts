pipeline {
    agent any
    stages {
        stage('Pull') {
            steps {
                git branch: 'main', url: 'https://github.com/jambhulkarcloudblitz-alt/CDEC-studentapp.git'
                
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
                 withSonarQubeEnv(installationName: 'sonarqube', credentialsId: 'secret-cred') {
                     sh '''
                     cd backend
                     mvn sonar:sonar -Dsonar.projectkey=studentapp
                     '''
                     }
             }       
    }

       
        stage('Quality Gate') {
            steps {
                timeout(10) {
                waitForQualityGate abortPipeline: true
                }
        }
        }

        stage('Delivery') {
            steps {
                echo "Deploy Success"
                
            }
        }


    }
}



