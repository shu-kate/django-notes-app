@Library('shared') _
pipeline {
    agent { label 'shubh' }


    stages {
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage("Code") {
            steps {
              script{  
                clone('https://github.com/shu-kate/django-notes-app.git', 'main')
              }
            }
        }
        stage("Build") {
            steps {
                script{
                docker_build("notes-app","latest","kateshubhangi")
               }
            }
        }
        stage("push to DockerHub") {
            steps {
                script{
                    docker_push("notes-app","latest","kateshubhangi")
                }
                
            }
        }
        
        stage("Deploy") {
            steps {
                echo "This is deploying the code"
        sh '''
            docker rm -f django_cont || true
            docker rm -f db_cont || true
            docker rm -f nginx_cont || true
            docker compose up -d
        '''
            }
        }
    }
}
