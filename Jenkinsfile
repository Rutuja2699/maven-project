pipeline {
    agent any

    stages {
        stage('scm checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Rutuja2699/maven-project.git'
            }
        }

        stage('compile the job') { // validate then compile
            steps {
                withMaven(jdk: 'JDK_HOME', maven: 'MVN_HOME', traceability: true) 
                {
                    sh 'mvn compile'
                }
            }
        }

        stage('deploy the job') { // deply the war file on tomcat
            steps {
                sshagent(['DEV_CICD']) 
                {
                    sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.4.239:/usr/share/tomcat9/webapps'
                }
            }
        }

    }
}
