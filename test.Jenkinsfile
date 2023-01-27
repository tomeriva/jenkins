pipeline{
    agent { node {label 'test'} }
    stages{
        stage("Login to DockerHub"){
            steps{
                sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_ID" --password-stdin'
            }
        }
        stage("Build Test App Image"){
            steps{
                sh 'docker build -t tomeriva/test-app -f ./fibonacci/client/Dockerfile.dev ./fibonacci/client'
            }
        }
        stage("Run Test App"){
            steps{
                sh 'docker run -e CI=true tomeriva/test-app npm run test'
            }
        }
        stage("Build PROD Images"){
            steps{
                sh '''
                docker build -t tomeriva/client ./fibonacci/client
                docker build -t tomeriva/nginx ./fibonacci/nginx
                docker build -t tomeriva/server ./fibonacci/server
                docker build -t tomeriva/worker ./fibonacci/worker
                '''
            }
        }
        stage("Push Prod Images"){
            steps{
                sh '''
                docker build -t tomeriva/client ./fibonacci/client
                docker build -t tomeriva/nginx  ./fibonacci/nginx
                docker build -t tomeriva/server ./fibonacci/server
                docker build -t tomeriva/worker ./fibonacci/worker
                '''
            }
        }
        stage("Delete Docker Builds"){
            steps{
                sh 'docker system prune -a -f'
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