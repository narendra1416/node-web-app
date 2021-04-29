pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/narendra1416/node-web-app.git', branch:'master'
      }
    }
    
      stage("Build image") {
            steps {
                script {
                    myapp = docker.build("narendra1416/node-js-24042021:${env.BUILD_ID}")
                }
            }
        }
    
      stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'narendra1416') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

    
    stage('Deploy App') {
      steps {
            sshagent(['k8s-new']) {
                    script {
                         
                           sh 'ssh ubuntu@172.31.73.227 && sudo su'
                           sh 'kubectl get nodes'
                           
                }
              }
            }

         }

      }

    }
