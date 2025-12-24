pipeline{
  agent{
    node{
      label "AGENT"
    }
  }
  stages{
    stage('Build'){
      steps{
        script{
          sh"""
          echo "scripted build"
        }
      }
    }
    stage('Test'){
      steps{
        script{
          sh"""
          echo "scripted build"
        }
      }
    }
    stage('Deploy'){
      steps{
        script{
          sh"""
          echo "scripted build"
        }
      }
    }
  }
  post{
    always{
      echo "always say hi"
      cleanWs()
    }
    success{
      echo "say the build successful"
    }
    failure{
      echo "say the build failed"
    }
  }
}
