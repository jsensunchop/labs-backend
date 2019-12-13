pipeline {
  agent any
  stages {
    stage('Initialize') {
      steps {
        sh '''
                    TOKEN1=f0205833f5def61d264b
                    TOKEN2=71c2ed93acab668acdeb
                    curl "https://api.github.com/repos/software-engineering-II/labs-backend/statuses/$GIT_COMMIT?access_token=${TOKEN1}${TOKEN2}"                       -H "Content-Type: application/json"                       -X POST                       -d "{"state": "pending","context": "continuous-integration/jenkins", "description": "Jenkins", "target_url": "$BUILD_URL"}"
                '''
        sh '''
                    echo "PATH = ${PATH}"
                '''
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean install package spring-boot:repackage'
      }
    }

  }
  tools {
    maven 'Maven'
    jdk 'JDK 1.8'
  }
  post {
    always {
      sh '''
                TOKEN1=f0205833f5def61d264b
                TOKEN2=71c2ed93acab668acdeb
                curl "https://api.github.com/repos/software-engineering-II/labs-backend/statuses/$GIT_COMMIT?access_token=${TOKEN1}${TOKEN2}"                   -H "Content-Type: application/json"                   -X POST                   -d "{"state": "$BUILD_STATUS","context": "continuous-integration/jenkins", "description": "Jenkins", "target_url": "$BUILD_URL"}"
            '''
    }

  }
}