pipeline{
  agent{
    node{
      label "AGENT"
    }
  }
  environment{
    course = "jenkins"
  }
  options{
    timeout(time: 10, unit: 'SECONDS')
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
          sh"""
          echo $course
          sleep 20
          """
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
    aborted{
      echo "timeout exceeded"
    }
  }
}
