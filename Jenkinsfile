pipeline{
    agent {
        label 'DevNode'
    }
    tools {
    maven 'MyMaven'
    }

    stages{
        stage('build'){
            steps{
                echo "checking push"
                echo "Running mvn"               
                sh 'mvn clean package'
            }
            post {
            success {
                // One or more steps need to be included within each condition's block.
                archiveArtifacts artifacts: '**/target/*.war'
            }
            }
        }
    }
    
}