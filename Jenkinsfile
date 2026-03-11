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

// pipeline {
//     agent { label 'node1' }
    
//     parameters {
//         string(name: 'APP_VERSION', defaultValue: '1.0', description: 'Application version')
//         choice(name: 'ENV', choices: ['Prod', 'ENF'], description: 'Deployment environment')
//     }
    
//     stages {
//         stage('Print Parameters') {
//             when{
//                 expression{
//                     params.APP_VERSION == '100'
//                 }
//             }
//             steps {
//                 echo "Version: ${params.APP_VERSION}"
//                 echo "Environment: ${params.ENV}"
//             }
//         } 
//     }
// }


// ----------- PARAMETERIZED PIPELINE WITH ERRORS-----------
    
// pipeline {
//     agent { label 'node1' }
    
//     parameters {
//         string(name: 'APP_VERSION', defaultValue: '1.0', description: 'Application version')
//         choice(name: 'ENV', choices: ['Prod', 'ENF'], description: 'Deployment environment')
//     }
    
//     stages {
//         stage('Validate and Print') {
//             steps {
//                 script {
//                     // Note the quotes around '100'
//                     if (params.APP_VERSION != '100') {
//                         error "Build Stopped: Version ${params.APP_VERSION} is not authorized. Only version 100 is allowed!"
//                     }
                    
//                     // These only run if the error above wasn't triggered
//                     echo "Version: ${params.APP_VERSION}"
//                     echo "Environment: ${params.ENV}"
//                 }
//             }
//         }
//     }
// }
