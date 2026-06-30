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
                sh '''
                    cd backend
                    mvn clean package -DskipTests
                '''
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
                timeout(time: 10, Unit: 'Minutes' ) {
                    waitForQualityGate abortPipeline: true, credentialsId: 'secret-cred'
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



