pipeline {
    agent {
        node {
            label 'master'
            customWorkspace '/mnt/adinath11'
        }
    }
    stages {
        stage('git repository clone') {
          
             steps {
                   cleanWs ()
                   
                   
                sh "git clone https://github.com/adinathshelke/webapp.git"
            }
        }
        stage('build the java application') {
            agent {
                node {
                    label 'master'
                    customWorkspace '/mnt/adinath11/webapp'
                }
            }
            steps {
                sh "mvn clean install"
            }
        }
        stage('deploying on slave1 jenkins machine') {
            agent {
                node {
                    label 'master'
                    customWorkspace '/mnt/adinath11/'
                }
            }
            steps {
               sh "ssh -i /mnt/adimumbai.pem ec2-user@172.31.7.231 -o StrictHostKeyChecking=no"


             sh "scp -i /mnt/adimumbai.pem /mnt/adinath11/webapp/target/WebApp.war ec2-user@172.31.7.231:/mnt/servers/apache-tomcat-9.0.76/webapps/"
            }
        }
        stage('deploying on slave2 jenkins machine') {
            agent {
                node {
                    label 'master'
                    customWorkspace '/mnt/adinath11/'
                }
            }
            steps {
            sh "ssh -i /mnt/adimumbai.pem ec2-user@172.31.11.169 -o StrictHostKeyChecking=no"


            sh "scp -i /mnt/adimumbai.pem /mnt/adinath11/webapp/target/WebApp.war ec2-user@172.31.11.169:/mnt/servers/apache-tomcat-9.0.76/webapps/"
            }
        }
    }
}
