pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
                             steps {
                        sshagent(['webserver']) {
                       sh "scp -v -o StrictHostKeyChecking=no ./web/target/*.war ec2-user@13.232.92.191:/opt/tomcat/webapps/"
      }
                    }
                }
    }
}
