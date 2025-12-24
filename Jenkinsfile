pipeline{
  agent{
    node{
      label "AGENT"
    }
  }
  environment{
    course = "jenkins"
  }
  stages{
    stage('Build'){
      steps{
        script{
          sh"""
          echo "hello"
          """
        }
      }
    }
    stage('Test'){
      steps{
       echo $course
      }
    }
    stage('Deploy'){
      steps{
        script{
          sh"""
          echo "scripted build"
          """
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
