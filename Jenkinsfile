pipeline {
    agent any
    environment {
        SONARSERVER = 'sonarserver'
        SONARSCANNER = 'sonarscanner'
    }

    stages {
        stage('Checkout') {
            steps {
                // Step 1: Get code from GitHub
                git branch: 'main', url: 'https://github.com/arshavardan/jenkins-sonarqube.git'
            }
        }

        stage('CODE ANALYSIS with SONARQUBE') {
          
		  environment {
             scannerHome = tool "${SONARSCANNER}"
          }

          steps {
            withSonarQubeEnv("${SONARSERVER}") {
               sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=onix-website-scan \
                   -Dsonar.projectName=onix-website-scan \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=/var/lib/jenkins/workspace/pipeline/src/
                '''
            }
            }
        }
    }
}
