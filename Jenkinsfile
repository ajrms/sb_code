pipeline {
  agent any
  // any, none, label, node, docker, dockerfile, kubernetes
  tools {
    maven 'my_maven'
  }

  environment {
    gitName = 'ajrms'
    gitEmail = 'sun98415@gmail.com'
    gitWebaddress = 'https://github.com/ajrms/sb_code.git'
    gitSshaddress = 'git@github.com:ajrms/sb_code.git'
    gitCredential = 'git_cre' // github credential 생성 시의 ID
  }

  stages {
    stage('Example') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: gitCredential, url: gitWebaddress]]])
      }
      post {
        failure {
          echo 'Repository clone failure'
        }
        success {
          echo 'Repository clone success'
        }
      }
    }

    stage('Maven Build') {
      steps {
        sh 'mvn clean install'
        // maven 플러그인이 미리 설치 되어있어야 함
        }
        post {
            failure {
                echo 'Maven build failure'
            }
            success {
                echo 'Maven build success'
            }
        }
    }
  }
}
