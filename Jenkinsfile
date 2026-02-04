pipeline {
    agent any

    stages {
        stage('scm checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Rutuja2699/maven-project.git'
            }
        }

        stage('package the job') { // validate,compile,test then package
            steps {
                withMaven(jdk: 'JDK_HOME', maven: 'MVN_HOME', traceability: true) 
                {
                    sh 'mvn package'
                }
            }
        }

    }
}
