pipeline {
    agent any
    stages {
        stage('Create deployment') {
          steps {
              sh 'kubectl create -f https://raw.githubusercontent.com/MiloWical/SimpleHTTPServer/master/SimpleHttpServer/SimpleHttpServer.Static.Metric/simple-http-server-nodeport.yml'
          }
        }
        stage('Wait for deployment to complete')
        {
            steps{
                sleep 15    
            }
        }
        stage('Test') {
            steps {
              script {
                def hostname = sh(script: 'hostname', returnStdout: true).trim()
                sh "echo Calling Container: http://${hostname}:30000"
                sh "curl http://${hostname}:30000"
              }
            }
        }
        stage('Delete deployment') {
            steps {
              sh 'kubectl delete -f https://raw.githubusercontent.com/MiloWical/SimpleHTTPServer/master/SimpleHttpServer/SimpleHttpServer.Static.Metric/simple-http-server-nodeport.yml'
          }
        }
    }
}
