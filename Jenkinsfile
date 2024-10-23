pipeline {
    agent any	
  environment {
    MAVEN_ARGS=" -e clean install"
    registry = ""
    dockerContainerName = 'bookapi'
    dockerImageName = 'bookapi-api'
  }
  stages {
    stage('Build') {
       steps {
                echo "everything is build before"
       }
    }
	  
 stage('clean container') {
      steps {
       sh 'sudo docker ps -f name=${dockerContainerName} -q | xargs --no-run-if-empty docker container stop'
       sh 'sudo docker container ls -a -fname=${dockerContainerName} -q | xargs -r docker container rm'
       sh 'sudo docker images -q --filter=reference=${dockerImageName} | xargs --no-run-if-empty docker rmi -f'
      }
  }
  stage('docker-compose start') {
      steps {
       sh 'sudo docker compose up -d'
      }
    }
  }
}
