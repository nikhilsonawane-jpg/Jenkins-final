// GIT WEBHOOK INTEGRATION CODE

// pipeline{
//   agent {label 'node1'}
//   stages{
//     stage('pull code'){
//       steps{
//       checkout scm
//       echo 'pulling code'
//     }
//     }
//     stage('run application'){
//       steps{
//         sh 'chmod +x app.sh'
//         sh 'sudo ./app.sh'
//       }
//     }
//   }
// }

// ----------- PARAMETERIZED PIPELINE-----------

pipeline {
    agent { label 'node1' }
    
    parameters {
        string(name: 'APP_VERSION', defaultValue: '1.0', description: 'Application version')
        choice(name: 'ENV', choices: ['Prod', 'ENF'], description: 'Deployment environment')
    }
    
    stages {
        stage('Print Parameters') {
            // when{
            //     expression{
            //         params.APP_VERSION == 100
            //     }
            // }

            steps {
                            script {
            if (params.APP_VERSION != '100') {
                // This will force the pipeline to stop and turn RED
                error "Invalid Environment: ${params.APP_VERSION}. Stopping the build!"
            }
                echo "Version: ${params.APP_VERSION}"
                echo "Environment: ${params.ENV}"
            }
        } 
    }
}
