pipeline{
    agent {
        label 'DevNode'
    }
    parameters {
    parameters {
    choice choices: ['Dev', 'Prod'], name: 'Environment'
    }

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
                sh 'mvn clean package -DskipTests=true'                
            }
        }
        stage(test){
            parallel {
                stage('testA'){
                    agent {
                        label 'DevNode'
                    }
                    steps{
                        echo "This is stage A"
                        sh 'mvn test'  
                    }
                    
                }
                stage('testB'){
                    agent {
                        label 'DevNode'
                    }                    
                    steps{
                        echo "This is stage B"
                        sh 'mvn test'  
                    }
                    
                }
            }
            post {
            success {
                // One or more steps need to be included within each condition's block.
                dir("webapp/target/")
                {
                    stash includes: '*.war', name: 'maven-build'
                }
            }
            }            
        }
    stage(deploy){
        when{
            expression {
                {params.environment == 'dev'}
                beforeAgent true
            }
            agent{label 'DevNode'}
            steps{
                dir("/var/www/html"){
                    unstash 'maven-build'
                }
                sh """
                cd /var/www/html/
                jar -xvf webapp.war
                """
            }
        }
    }

    }
    
}