properties([pipelineTriggers([githubPush()])]) 
pipeline {
    agent any
    stages {
        stage('Test') {
        agent { label "agent1" } // Define mau running di agent yang mana
            steps {
              // Test menggunakan Sonarqube
                script { echo "Begin Testing Using Sonarqube" 
                def scannerHome = tool 'sonarqube1' ; //sonarqube by Global Tools Configuration
                withSonarQubeEnv('sonarqube') {  //sonarqube by Endpoint Server Sonarqube
                sh "${scannerHome}/bin/sonar-scanner"}
                } 
              }
            
            }
        stage('Build') {
        agent { label "agent1" } // Define mau running di agent yang mana
            steps {
              // Build Image
                script { echo "Begin Build"
                if (env.BRANCH_NAME == "development")
                
                { 
                sh "docker build -t arizalsandi/landingpage:dev-$BUILD_NUMBER . "
                sh "docker push arizalsandi/landingpage:dev-$BUILD_NUMBER"

                }else{ 
                sh "docker build -t arizalsandi/landingpage:master-$BUILD_NUMBER . "
                sh "docker push arizalsandi/landingpage:master-$BUILD_NUMBER"
                
                }
                
                
                }
                
              }
            }
        stage('Deploy') {
        agent { label "agent1" }  // Define mau running di agent yang mana
            steps {
              // Deploy to Kubernetes
                script { echo "Begin to Deploy" 
                sh "kubectl set image deployment/landingpage landingpage=arizalsandi/landingpage:dev-$BUILD_NUMBER -n app-landingpage"
                sh "docker image rmi arizalsandi/landingpage:dev-$BUILD_NUMBER"
                }
            }
          }
        }
      }
