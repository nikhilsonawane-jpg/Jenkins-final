pipeline{
  agent {label 'node1'}
  stages{
    stage('pull code'){
      steps{
      checkout SCM
      echo 'pulling code'
    }
    }
    stage('run application'){
      steps{
        sh './app.sh'
      }
    }
  }
}
