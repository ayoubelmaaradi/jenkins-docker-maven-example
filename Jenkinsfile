pipeline {
   agent any

   tools {
      // Install the Maven version configured as "M3" and add it to the path.
      maven "M3"
   }

   stages {
      stage('Build') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/ayoubelmaaradi/jenkins-docker-maven-example'

            // Run Maven on a Unix agent.
            sh "mvn -Dmaven.test.failure.ignore=true clean package"
            sh "docker build -t xen0077/myjenkins ."
            withCredentials([usernamePassword(credentialsId: 'DOCKER_CREDENTIALS', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
            sh 'docker push xen0077/myjenkins:latest'
                }
            

            // To run Maven on a Windows agent, use
            // bat "mvn -Dmaven.test.failure.ignore=true clean package"
         }

         post {
            // If Maven was able to run the tests, even if some of the test
            // failed, record the test results and archive the jar file.
            success {
               junit '**/target/surefire-reports/TEST-*.xml'
               archiveArtifacts 'target/*.jar'
            }
         }
      }
   }
}
