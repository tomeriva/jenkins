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
                sh 'docker build -t tomeriva/test-app -f ./fibonacci/client/Dockerfile.dev ./fibonacci/client'
            }
        }
        stage("test app"){
            steps{
                sh 'docker run -e CI=true tomeriva/test-app npm run test'
            }
        }
        stage("delete images"){
            steps{
                sh 'docker rmi $(docker images -a -q)'
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