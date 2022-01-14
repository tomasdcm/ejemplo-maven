pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                script{
                    dir('C:/Programming/devops-usach/tomas-del-campo/ejemplo-maven'){
                        env.JAVA_HOME = "C:/Program Files/Java/jdk-11.0.13"
                        bat './mvnw.cmd clean compile -e'
                    }
                }
            }
        }
        stage('SonarQube analysis') 
        {
            steps{
                script{
                    def scannerHome = tool 'sonar-scanner';
                    withSonarQubeEnv('sonarqube-server') {
                        bat "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ejemplo-maven -Dsonar.sources=src -Dsonar.java.binaries=build"
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script{
                    dir('C:/Programming/devops-usach/tomas-del-campo/ejemplo-maven'){
                        env.JAVA_HOME = "C:/Program Files/Java/jdk-11.0.13"
                        bat './mvnw.cmd clean test -e'
                    }
                }
            }
        }
        stage('Jar') {
            steps {
                script{
                    dir('C:/Programming/devops-usach/tomas-del-campo/ejemplo-maven'){
                        env.JAVA_HOME = "C:/Program Files/Java/jdk-11.0.13"
                        bat './mvnw.cmd clean package -e'
                    }
                }
            }
        }
        stage('Run') {
            steps {
                script{
                    dir('C:/Programming/devops-usach/tomas-del-campo/ejemplo-maven'){
                        env.JAVA_HOME = "C:/Program Files/Java/jdk-11.0.13"
                        bat './mvnw.cmd spring-boot:run &'
                        sleep 10
                    }
                }
            }
        }
        stage('TestApp') {
            steps {
                script{
                  /*  bat 'start "chrome" "http://localhost:8081/rest/mscovid/test?msg=testing"'  */
                  /*  bat 'curl http://localhost:8081/rest/mscovid/test?msg=testing' */
                  sleep 5
                }
            }
        }
    }
}
