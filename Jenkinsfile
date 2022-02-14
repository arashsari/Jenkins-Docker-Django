node('docker') {
    stage 'Checkout'
        checkout scm
    stage 'Build & UnitTest'
        sh "docker build -t app:B${BUILD_NUMBER} -f Dockerfile ."
  
    stage 'Integration Test'
        sh "docker-compose -f docker-compose.app.yml up --force-recreate --abort-on-container-exit"
        sh "docker-compose -f docker-compose.app.yml down -v"
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