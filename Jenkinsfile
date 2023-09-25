pipeline {
    agent any
    
    tools{
        jdk "jdk17"
        maven "maven3"
    } 
    environment{
        SONAR_HOME = tool "sonar-scanner"
    }
    stages {
        stage('Git CheckOut') {
            steps {
              git branch: 'main', url: 'https://github.com/DevOpsWorld-9959/javaProject.git'
            }
        }
        stage("Code Compile"){
            steps{
                sh "mvn compile"
            }
        }
        stage("OWASP dependency Check"){
            steps{
              dependencyCheck additionalArguments: '--scan ./',odcInstallation:'DC'
              dependencyCheckPublisher pattern:'**/dependency-check-report.xml'                   
            }
        }        

        stage("Trivy scan"){
            steps{
                sh "trivy fs ."
            }
        }       
 
    }
}
