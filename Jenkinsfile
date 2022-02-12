ode('docker') {

    stage 'Checkout'
        checkout scm
    stage 'Build & UnitTest'
    sh "docker build -t accountownerapp:B${BUILD_NUMBER} -f Dockerfile ."
    sh "docker build -t accountownerapp:test-B${BUILD_NUMBER} -f Dockerfile.Integration ."
    
    stage 'Pusblish UT Reports'
        
        containerID = sh (
            script: "docker run -d accountownerapp:B${BUILD_NUMBER}", 
        returnStdout: true
        ).trim()
        echo "Container ID is ==> ${containerID}"
        sh "docker cp ${containerID}:/TestResults/test_results.xml test_results.xml"
        sh "docker stop ${containerID}"
        sh "docker rm ${containerID}"
        step([$class: 'MSTestPublisher', failOnError: false, testResultsFile: 'test_results.xml'])    
      
    stage 'Integration Test'
        //sh 'docker-compose -f docker-compose.integration.yml up'
        sh "docker-compose -f docker-compose.integration.yml up --force-recreate --abort-on-container-exit"
        sh "docker-compose -f docker-compose.integration.yml down -v"
}

// pipeline {
//   agent any
//   environment {
//     appName = "server"
//     registry = "arashsari/arash-django/"
//     registryCredential = "ArashsariDockerRegistry"
//     projectPath = "/jenkins/data/workspace/django-server"
//   }
//   parameters {
//     gitParameter name: 'TAG', defaultValue: '0.0.1', type: 'PT_TAG'
//   }

//  stages {

//   stage('Basic Information') {
//    steps {
//     sh "echo tag: ${params.TAG}"
//    }
//   }

//   stage('GIT Checkout') {
//       steps {
//         checkout([$class: 'GitSCM',
//                           branches: [[name: "${params.TAG}"]],
//                           doGenerateSubmoduleConfigurations: false,
//                           extensions: [],
//                           gitTool: 'Default',
//                           submoduleCfg: [],
//                           userRemoteConfigs: [[url: 'https://github.com/arashsari/Jenkins-Docker-Django.git']]
//                         ])
//       }
//   }

//   stage('Build Image') {
//    steps {
//     script {
//       dockerImage = docker.build "$registry:latest"
//     }
//    }
//   }

//  }

// }