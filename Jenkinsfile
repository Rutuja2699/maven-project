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

        stage('deploy the job') { // deploy the war file on tomcat
    steps {
        sshagent(['DEV_CICD']) {
            sh '''
                # 1) Copy WAR to a writable location
                scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.4.239:/tmp/webapp.war

                # 2) Move WAR to Tomcat webapps using sudo, then restart Tomcat
                ssh -o StrictHostKeyChecking=no ec2-user@172.31.4.239 '
                    sudo mv /tmp/webapp.war /usr/share/tomcat9/webapps/webapp.war &&
                    sudo systemctl restart tomcat9
                '
            '''
        }
    }
}

    }
}
