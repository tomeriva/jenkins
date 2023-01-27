pipeline{
    agent { node {label 'test'} }
    stages{
        stage("Login to DockerHub"){
            steps{
                sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_ID" --password-stdin'
            }
        }
        stage("Build Image"){
            steps{
                sh 'docker build -t tomeriva/testapp -f ./nodejs-app/Dockerfile.dev ./nodejs-app'
            }
        }
        stage("test app"){
            steps{
                sh 'docker run -e CI=true tomeriva/testapp npm test'
            }
        }
    }
    post{
        always{
            echo "========always========"
            cleanup()
        }
        success{
            echo "========pipeline executed successfully ========"
            cleanup()
        }
        failure{
            echo "========pipeline execution failed========"
            cleanup()
        }
    }
}