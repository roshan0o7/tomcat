pipeline {
    agent any
    
    stages {
        stage ('SCM chekout') {
            steps {
                git 'https://github.com/Akshay369vm/java-tomcat-maven-example.git'
            }
        }
        stage ('build') {
            steps {
                sh "mvn package"
            }
        }
        stage('sonarqube analysis') {
            environment {
            SCANNER_HOME = tool 'SonarQube'
            PROJECT_NAME = "Java-maven"
        }
        steps {
            script {
                withSonarQubeEnv('SonarQube') {
                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=$PROJECT_NAME \
                    -Dsonar.java.binaries=\"target/classes/\"'''
                }
            }
            }
        }
        stage('deploy'){
            steps {
                sh""" sudo cp /var/lib/jenkins/workspace/Java-Project/target/java-tomcat-maven-example.war /opt/tomcat/webapps
                sudo service tomcat restart
                """
            }
        }
        stage ('post build') {
            step {
                sh "echo "build Passed""
            }
        }
    }
}
