def registry = 'https://trialsdspvj.jfrog.io/'

pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    stages {
        stage("build") {
            steps {
                echo "----------- build started ----------"
                sh 'mvn clean compile'
                echo "----------- build completed ----------"
            }
        }

        stage("test") {
            steps {
                echo "----------- running tests ----------"
                sh 'mvn test'
            }
            post {
                always {
                    junit testResults: 'target/surefire-reports/*.xml', allowEmptyResults: true
                }
            }
        }

        stage("package & deploy") {
            steps {
                echo "----------- packaging & deploying ----------"
                sh 'mvn package deploy -DskipTests'
                echo "----------- deploy completed ----------"
            }
        }

        stage('SonarQube analysis') {
            steps {
                script {
                    scannerHome = tool 'radhu-sonarcubescanner'
                }
                withSonarQubeEnv('radhu_sonarcube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
