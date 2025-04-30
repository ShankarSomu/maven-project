pipeline{
    agent {
        label 'DevNode'
    }
    parameters {
    string defaultValue: 'Somasundaram', name: 'LASTNAME'
    }
    environment{
        NAME="Shankar"
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
                echo "Hello $NAME ${params.LASTNAME}"
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