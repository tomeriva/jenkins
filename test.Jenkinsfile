pipeline{
    agent{ node { label 'test' } }
    stages{
        stage("Build Image"){
            steps{
                dockerfile {
                    filename 'Dockerfile.build'
                    dir './nodejs-app'
                    label 'tomeriva/nodejs'
                    additionalBuildArgs  '--build-arg version=1.0.2'
                    args '-v /tmp:/tmp'
                }
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