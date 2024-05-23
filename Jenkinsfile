pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
stages{
        stage('Build'){
            steps {
                sh 'mvn clean package -Dmaven.test.skip=true'
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
                        sshagent(['Tomcat']) {
                       sh "scp -v -o StrictHostKeyChecking=no ./web/target/*.war ec2-user@3.111.168.130:/opt/tomcat/webapps/"
      }
                    }
                }
    }
}
