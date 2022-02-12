
// library identifier: 'jenkins-shared@master', retriever: modernSCM(
//  [$class: 'GitSCMSource',
//   remote: 'https://github.com/arashsari/Jenkins-Docker-Django.git',
//  ])

pipeline {
  agent any
  environment {
    appName = "server"
    registry = "arashsari/arash-django/"
    registryCredential = "ArashsariDockerRegistry"
    projectPath = "/jenkins/data/workspace/django-server"
  }
  parameters {
    gitParameter name: 'TAG', defaultValue: '0.0.1', type: 'PT_TAG'
    // gitParameter branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH'
  }

 stages {

  stage('Basic Information') {
   steps {
    sh "echo tag: ${params.TAG}"
   }
  }

  stage('GIT Checkout') {
      steps {
        // git branch: "${params.BRANCH}", url: 'https://github.com/arashsari/Jenkins-Docker-Django.git'

        checkout([$class: 'GitSCM',
                          branches: [[name: "${params.TAG}"]],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [],
                          gitTool: 'Default',
                          submoduleCfg: [],
                          userRemoteConfigs: [[url: 'https://github.com/arashsari/Jenkins-Docker-Django.git']]
                        ])
      }
  }

  stage('Build Image') {
   steps {
    script {
      dockerImage = docker.build "$registry:latest"
    //  if (isMain()) {
    //   dockerImage = docker.build "$registry:latest"
    //  } else {
    //   dockerImage = docker.build "$registry:${params.TAG}"
    //  }
    }
   }
  }

  // stage('Deploy Image') {
  //  steps {
  //   script {
  //     docker.withRegistry("$registryURL", registryCredential) {
  //     dockerImage.push()
  //     }
  //   }
  //  }
  // }



//   stage('Garbage Collection') {
//    steps {
//     sh "docker rmi $registry:${params.TAG}"
//    }
//   }
 }

}

def getBuildName() {
 "${BUILD_NUMBER}_$appName:${params.TAG}"
}

def isMain() {
 "main" == "main"
//  "${params.TAG}" == "main"
}