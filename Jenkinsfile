node {
  checkout scm
  env.PATH = "${tool 'Maven3'}/bin:${env.PATH}"
  stage('Package') {
    dir('webapp') {
      sh 'mvn clean package -DskipTests'
    }
  }

  stage('Create Docker Image') {
    dir('webapp') {
      docker.build("arungupta/docker-jenkins-pipeline:${env.BUILD_NUMBER}")
    }
  }

  
  stage('Push Docker Image') {
    dir('webapp') {
        docker.build("arungupta/docker-jenkins-pipeline:${env.BUILD_NUMBER}").push()
      }
    } 
}
