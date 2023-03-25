pipeline {
  agent any
  options {
    ansiColor('xterm')
  }
  parameters {
    choice(name: 'COMPONENT', choices: ['cart', 'catalogue', 'user', 'frontend', 'shipping', 'payment', 'dispatch'], description: 'Choose COMPONENT')
    choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Choose ENV')
    string(name: 'APP_VERSION', defaultValue: '', description: 'Which app version?')
  }

  stages {
    stage('terraform') {
      steps {
        sh '''
          terraform init
          terraform apply -auto-approve -var COMPONENT=${COMPONENT} -var ENV=${ENV} -parallelism=1
        '''
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}