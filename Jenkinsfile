pipeline {
  agent {
    label "jenkins-s2i"
  }
  environment {
    ORG               = 'jenkinsx-pw1'
    APP_NAME          = 'demo9'
    BRANCH_NAME       = "$GIT_BRANCH".replaceAll('^origin/','')
    REV               = "$GIT_COMMIT".trim().take(7)
    RELEASE_VERSION   = "$BRANCH_NAME-$BUILD_NUMBER-$REV"
    RELEASE_NAMESPACE = "$APP_NAME-$BRANCH_NAME".toLowerCase()
    IMAGE_NAME        = "$DOCKER_REGISTRY/$ORG/$APP_NAME"
  }
  stages {
    stage('First stage') {
      steps {
        container('s2i') {
          sh 's2i build . pingworks/demo-builder:2 demo9:1.0.2'
        }
      }
    }
    stage('Second stage') {
      steps {
        container('s2i') {
        }
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}
