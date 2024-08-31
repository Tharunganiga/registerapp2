pipeline {
    agent { label 'Jenkins_Agent' }
    tools {
        jdk 'java17'
        maven 'maven3'
    }
 stages{
        stage("Cleanup Workspace"){
                steps {
                cleanWs()
                }
        }
        stage("Checkout from SCM"){
                steps {
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/Tharunganiga/registerapp2.git'
                }
        }
	 stage("Build Application"){
            steps {
                sh "mvn clean package"
            }

        }
	 stage("Test Application"){
           steps {
                 sh "mvn test"
           }
       }
	  stage("SonarQube Analysis"){
           steps {
	           script {
		           withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token') {
                       sh "mvn sonar:sonar"
		               }
	            }	
            }
         }

 }
}
	 
