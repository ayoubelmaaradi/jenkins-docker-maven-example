pipeline{
     agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages{
        stage("Build"){
            steps{
                echo "========executing A========"
                git 'https://github.com/ayoubelmaaradi/jenkins-docker-maven-example'
                sh 'mvn clean package'
            }
         
        }
    }
}
