pipeline {
agent any
tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "Maven"
    }
   stages {
        stage (SCM) {
            steps {
                 git credentialsId: 'github_credentials', url: 'https://github.com/Abilash777/spring3-mvc-maven-xml-hello-world.git'
                }
           }
    stage ('Build') {
            steps {
                 sh "mvn -Dmaven.test.failure.ignore=true clean package"
                }
           }
   stage ('artifacts') {
            steps {
                
                 archiveArtifacts 'target/*.war'
                }
           }
    stage('deploy') {
            steps {
                // Tomcat deploy
                 deploy adapters: [tomcat8(credentialsId: 'tomcat_credentials', path: '', url: 'http://13.233.99.175:8181/')], contextPath: 'pipelineSpring4', war: '**/target/*.war'
                   }
                }    
	stage ('success'){
            steps {
                script {
                    currentBuild.result = 'SUCCESS'
                }
            }
	}
    stage ('failure'){
        steps {
            script {
                currentBuild.result = 'FAILURE'
            }
        }

	}
	stage ('mailer'){
            step {
            step([$class: 'Mailer',
                notifyEveryUnstableBuild: true,
                recipients: "abilashsr1991@gmail.com",
                sendToIndividuals: true])
        }
     }
       
   }
   
}

