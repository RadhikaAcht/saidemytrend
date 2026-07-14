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
                sh 'mvn clean deploy'
                echo "----------- build completed ----------"
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
