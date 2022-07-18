properties([pipelineTriggers([githubPush()])]) 
pipeline {
    agent any
    stages {
        stage('Build') {
        agent { label "agent1" }
            steps {
              //
                script { echo "Build"
                if (env.BRANCH_NAME == "development")
                
                { 
                sh "docker build -t arizalsandi/landingpage:dev-$(git rev-parse --short HEAD) . "
                sh "docker push arizalsandi/landingpage:dev-$(git rev-parse --short HEAD)"

                }else{ 
                sh "docker build -t arizalsandi/landingpage:master-$(git rev-parse --short HEAD) . "
                sh "docker push arizalsandi/landingpage:master-$(git rev-parse --short HEAD)"
                
                }
                
                
                }
                
              }
            }
        stage('Test') {
        agent { label "agent1" }
            steps {
              //
                script { echo "Test" }
              }
            }
        stage('Deploy') {
        agent { label "agent1" }
            steps {
              //
                script { echo "Deploy3" }
            }
          }
        }
      }
