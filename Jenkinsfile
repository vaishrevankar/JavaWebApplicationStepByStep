pipeline {
    agent any
   
    stages {

      stage('clean')
            {
                steps
                 { 
                    sh 'mvn clean package'
                 }
            }
        stage("build & SonarQube analysis") {
            steps {
              withSonarQubeEnv('sonarqube') {
                sh 'mvn clean package sonar:sonar'
              }
            } 
        }
        
        stage('deploy'){
        steps{  
          sshagent(['tomcat-dev']) {
            sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@http://13.233.4.245:~/apache-tomcat-9.0.26/webapps/'
            }
        }
        }
        }
        }
