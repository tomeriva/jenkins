pipeline{
    agent { {label "test"}
    }
    stages{
        stage("Build Image"){
            steps{
                sh 'docker build -t tomeriva/testapp ./nodejs-app/.'
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