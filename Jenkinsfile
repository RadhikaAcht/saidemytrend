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
            environment {
                scannerHome = tool 'radhu-sonarcubescanner'
            }
            steps {
                withSonarQubeEnv('radhu_sonarcube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
