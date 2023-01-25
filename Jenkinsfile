pipeline{
    
    agent any 
              
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/KAMMANICHANDRASEKHAR/demo-counter-app.git'
                }
            }
        }
        stage('UNIT testing'){
           def mvnHome = tool name: "maven-3.8.7", type: "maven"
            def mvncmd ="${mvnHome}/bin/mvn"
            
            steps{
                
                script{
                    
                    sh "${mvncmd} install"
                }
            }
        }
       /*
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh "${mvnHome}/bin/mvn verify -DskipUnitTests"
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh "${mvnHome}/bin/mvn clean install'
                }
            }
        }
        */
        stage('Static code analysis'){
            def mvnHome = tool name: "maven-3.8.7", type: "maven"
            def mvncmd ="${mvnHome}/bin/mvn"
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'sonarr') {
                        
                        sh "${mvncmd} clean package sonar:sonar"
                    }
                   }
                    
                }
            }
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonarr'
                    }
                }
            }
        }
        
}
