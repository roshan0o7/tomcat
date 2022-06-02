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
        stage('deploy'){
            steps {
                sh""" sudo cp /var/lib/jenkins/workspace/Java-Project/target/java-tomcat-maven-example.war /opt/tomcat/webapps
                sudo service tomcat restart
                """
            }
        }
    }
}
