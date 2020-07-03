pipeline{
    agent any
    stages {
        stage ('Build Backend') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage ('Unit tests') {
            steps {
                sh 'mvn test'
            }
        }
         stage ('Sonar Analysis') {
             environment {
                 scannerHome = tool 'SONAR_SCANNER'

             }
            steps {
                withSonarQubeEnv('SONAR_LOCAL'){
                    sh "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://localhost:9000 -Dsonar.login=5a6af7248b1b99d2d2cfb0e875c6cf11b7d1f89c -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**.**/src/teste/**,**/model/**.**Aplication.Java"
                }
            }
        }
        stage ('Quality Gqate') {
            steps {
                timeout(time: 1, unit: 'MINUTES'){
                    waitForQualityGate abortPipeline: true
                }
                    
            }   

        }
    }
}


