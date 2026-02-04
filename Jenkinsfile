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

    }
}
