pipeline{
  agent {label 'node1'}
  stages{
    stage('pull code'){
      steps{
      checkout scm
      echo 'pulling code'
    }
    }
    stage('run application'){
      steps{
        sh 'chmod +x app.sh'
        sh 'sudo ./app.sh'
      }
    }
  }
}
