pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Build started'
            }
        }

        stage('Test') {
            steps {
                bat '''
                    if exist index.html (
                        echo TEST PASSED
                    ) else (
                        echo TEST FAILED
                        exit /b 1
                    )
                '''
            }
        }

        stage('Docker Build') {
            steps {
                bat '''
                    set "PATH=C:\\Users\\Admin\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin;%PATH%"
                    docker build -t jenkins-pipeline-lab4 .
                '''
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                    set "PATH=C:\\Users\\Admin\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin;%PATH%"

                    docker stop jenkins-pipeline-lab4-container 2>nul
                    docker rm jenkins-pipeline-lab4-container 2>nul

                    docker run -d --name jenkins-pipeline-lab4-container -p 8083:80 jenkins-pipeline-lab4
                '''
            }
        }
    }
}
