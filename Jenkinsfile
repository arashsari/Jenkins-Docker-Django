    node {
        stage('Checkout') {
            // Clean the workspace
            cleanWs()
            // Get some code from a GitHub repository
            checkout scm
        }
        stage('Setup') {
            sh "echo hello"
        }

        stage('Build') {
          dockerImage = docker.build "$registry:latest"
            // withCredentials([usernamePassword(credentialsId: 'aws_access_keys', usernameVariable: 'AWS_ACCESS_KEY', passwordVariable: 'AWS_SECRET_KEY')]) {
            // // Run the packer build
            // sh "packer build -var 'aws_region=us-west-2' ubuntu.json"
            // }
        }

    }

// // library identifier: 'jenkins-shared@main', retriever: modernSCM(
// //  [$class: 'GitSCMSource',
// //   remote: 'https://github.com/arashsari/Jenkins-Docker-Django.git',
// //  ])

// pipeline {
//  environment {
//   appName = "server"
//   registry = "arashsari/arash-django/"
//   registryCredential = "ArashsariDockerRegistry"
//   projectPath = "/jenkins/data/workspace/django-server"
//  }

//  agent any

// //  parameters {
// //   gitParameter name: 'RELEASE_TAG',
// //    type: 'PT_TAG',
// //    defaultValue: 'main'
// //  }

//  stages {

//   stage('Basic Information') {
//    steps {
//     sh "echo tag: ${params.RELEASE_TAG}"
//    }
//   }

//   stage('Build Image') {
//    steps {
//     script {
//       dockerImage = docker.build "$registry:latest"
//     //  if (isMain()) {
//     //   dockerImage = docker.build "$registry:latest"
//     //  } else {
//     //   dockerImage = docker.build "$registry:${params.RELEASE_TAG}"
//     //  }
//     }
//    }
//   }

//   // stage('Deploy Image') {
//   //  steps {
//   //   script {
//   //     docker.withRegistry("$registryURL", registryCredential) {
//   //     dockerImage.push()
//   //     }
//   //   }
//   //  }
//   // }



// //   stage('Garbage Collection') {
// //    steps {
// //     sh "docker rmi $registry:${params.RELEASE_TAG}"
// //    }
// //   }
//  }

//  post {
//   failure {
//    script {
//     telegram.sendTelegram("Build failed for ${getBuildName()}\n" +
//      "Checkout Jenkins console for more information. If you are not a developer simply ignore this message.")
//    }
//   }
//  }

// }

// def getBuildName() {
//  "${BUILD_NUMBER}_$appName:${params.RELEASE_TAG}"
// }

// def isMain() {
//  "main" == "main"
// //  "${params.RELEASE_TAG}" == "main"
// }