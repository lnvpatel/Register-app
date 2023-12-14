pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'java17'
        maven 'maven3'
    }
    stages{
        stage("Cleanup Workspace"){
                steps {
                cleanWs()
                }
        }

        stage("Checkout from SCM"){
                steps {
                    git branch: 'main', credentialsId: 'GitHub', url: 'https://github.com/lnvpatel/Register-app.git'
                }
        }

        stage("Build Application"){
            steps {
                sh "mvn clean package"
            }

       }

       stage("Test Application"){
           steps {
                 sh "mvn test"
           }
       }
        
        stage("SonarQube Analysis"){
           steps {
               scripts{
                 withSonarCubeENV(credentialID: 'JenkinsSonarQubetoken') {
                 sh "mvn sonar:sonar"
                     }
                }
            }
        }
    }
}
