pipeline {
    agent any

    stages {
        stage('Compile Code') {
            steps {
                script{
                    bat "mvn clean compile -e"  
                }                                           
            }
        }
        
        stage('SonarQube analysis') {
            steps {
                script{
                    def scannerHome = tool 'sonar-scanner';
                    withSonarQubeEnv('sonar-server') { 
                    bat "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ejemplo-maven -Dsonar.sources=src -Dsonar.java.binaries=build " 
                    }
                }                                                 
            }
        }
        
         stage('Test Code') {
            steps {
                script{
                    bat "mvn clean test -e"    
                }                                                 
            }
        }
         stage('Jar Code') {
            steps {
                script{
                    bat "mvn clean package -e" 
                }                                   
            }
        }
         stage('Run Jar') {
            steps {
                script{
                    bat "start /min mvn spring-boot:run &" 
                }                                    
            }
        }
        
        /*stage('Test Application') {
            steps {
                script{
                    bat "start chrome http://localhost:8081/rest/mscovid/test?msg=testing" 
                }                                    
            }
        }*/
        
        stage('Upload Nexus') {
            steps {
                script{
                    bat "curl -v --user admin:123456 --upload-file DevOpsUsach2020-0.0.1.jar https://44fe-186-79-184-102.ngrok.io/repository/test-repo/com/devopsusach2020/DevOpsUsach2020/0.0.2/DevOpsUsach2020-0.0.2.jar " 
                }                                    
            }
        }
        
    }
}
