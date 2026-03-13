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

// -------------- Matrix (run pipeline on multiple agents) --------------

// pipeline {
//     agent none
//     stages {
//         stage('Deploy Matrix') {
//             matrix {
//                 axes {
//                     axis {
//                         name 'OS'
//                         values 'node1', 'built-in'
//                     }
//                 }
//                 stages {
//                     stage('Deploy') {
//                         agent { label "${OS}" }
//                         steps {
//                             echo "Deploying to agent: ${OS}"
//                         }
//                     }
//                 }
//             }
//         }
//     }
// }


// ------------------- parallel pipeline -----------------

// pipeline{
//     agent none
//     stages{
//         stage('Global Deployment'){
//         parallel{
//                 stage('agent 1'){
//                     agent{label 'built-in'}
//                     steps{
//                         echo 'im mac'
//                     }
//                 }
//                 stage('agent 2'){
//                     agent{label 'node1'}
//                     steps{
//                         echo 'im EC2' 
//                     }
//                 }
//             }
//         }
//     }
// }


// -------------input ---------------
// pipeline {

//     agent any

//     stages {

//         stage('Build') {
//             steps {
//                 echo "Building application"
//             }
//         }

//         stage('Approval') {
//             steps {
//                 input message: "Approve?"
//             }
//         }

//         stage('Deploy') {
//             steps {
//                 echo "Deploying to production"
//             }
//         }

//     }

// }

// ---------------- parameterized input ----------------

// pipeline{
//     agent any
//          options{
//             timeout(time: 1, unit: 'MINUTES')
//             }
//     stages{
//         stage('Initial Approval'){
//             steps{
//             input message: 'Deploy?', id: '1', submitter: 'admin,nikhil'
//             }
//         }
//         stage('deployment gate'){
//             steps{
//             script{
//                 def userInput = input(
//                 id: 'confirm',
//                 message: 'Promote to Production?',
//                 parameters: [
//                     string(name: 'RELEASE_NOTE', defaultValue: '', description: 'Reason for this release'),
//                     choice(name: 'APPROVER', choices: ['Nikhil', 'Manager'], description: 'Who is approving?')
//                 ]
//             )
//             // Accessing the values provided during the pause
//             echo "Release approved by: ${userInput.APPROVER}"
//             echo "Notes: ${userInput.RELEASE_NOTE}"
//             }
//             }
            
                
//             }
//         }
//     }

// ------------------ parameterized verified input -------------------
pipeline {
    agent any
    
    options {
        timeout(time: 1, unit: 'MINUTES') 
    }

    stages {
        stage('deployment gate') {

            steps {
                script {
                    // def userInput = input(
                    //     id: 'confirm',
                    //     message: 'Promote to Production?',
                    //     submitter: 'admin,nikhil', // Fixed submitter syntax
                    //     parameters: [
                    //         string(name: 'RELEASE_NOTE', defaultValue: '', description: 'Reason for this release'),
                    //         choice(name: 'APPROVER', choices: ['Nikhil', 'Manager'], description: 'Who is approving?')
                    //     ]
                    // )
                    // echo "Release approved by: ${userInput.APPROVER}"
                    // echo "Notes: ${userInput.RELEASE_NOTE}"
                    // ----or-------
                //     def userInput = input(
                //           id: 'approval',
                //         message: 'Promote to Production?',
                //         submitter: 'admin,nikhil',
                //         submitterParameter: 'APPROVED_BY',
                //         parameters: [
                //             string(name: 'RELEASE_NOTE', defaultValue: '', description: 'Reason for release'),
                //             choice(name: 'APPROVER', choices: ['Nikhil', 'Manager'], description: 'Who is approving?')
                //         ]
                //     )
                //     if (userInput.APPROVER == 'Manager' && userInput.APPROVED_BY != 'Manager') {
                //     error "Security Violation: User ${userInput.APPROVED_BY} tried to approve as a Manager!"
                // }

                //     echo "Approved by: ${userInput.APPROVED_BY}"
                //     echo "Notes: ${userInput.RELEASE_NOTE}"
                    // ----------or---------

                    def rolePermissions = [
                    'Manager' : 'admin',
                    'Lead'    : 'nikhil',
                    'Trainee' : 'intern_user',
                    'Nikhil'  : 'nikhil'
                    ]

                    def userInput = input(
                    id: 'approval',
                    message: 'Promote to Production?',
                    submitter: 'admin,intern_user,nikhil', 
                    submitterParameter: 'REAL_USER',
                    parameters: [
                    choice(name: 'ROLE', 
                    choices: ['Nikhil', 'Manager', 'Lead', 'Trainee'], 
                    description: 'Select your authorized role')
                    ]
                )



                def authorizedUser = rolePermissions[userInput.ROLE]

                if (userInput.REAL_USER != authorizedUser) {
                   error "Security Violation: ${userInput.REAL_USER} is not authorized to approve as ${userInput.ROLE}. Required user: ${authorizedUser}"
                }

                echo "Verified: ${userInput.REAL_USER} approved as ${userInput.ROLE}"


                }
            }
        }
    }
}

// pipeline{
//     agent {label 'built-in'}
//     options{
//         timeout(time: 1, unit: 'MINUTES')
//     }
//     stages{
//       stage('deployment'){
//         steps{
//             script{
//             def list = [
//             'Nikhil' : 'nikhil',
//             'Jinesh' : 'security',
//             'aryant' : 'CEO',
//             ]
            
//             def inputuser = input(
//             id: '1',
//             message: 'want to approve?',
//             submitter: 'admin,security,CEO,nikhil',
//             submitterParameter: "CurrentUser",
//             parameters: [
//             choice(name: 'role', choices: ['Nikhil','Jinesh','aryan'], description: 'select your role')

//             ]
//             )
            
//             def auth = list[inputuser.CurrentUser]
//             if(inputuser.CurrentUser != auth){
//             error "not auth user"
//             }
//             echo "success"
//             }
//         }
//         }
//     }
// }
        
