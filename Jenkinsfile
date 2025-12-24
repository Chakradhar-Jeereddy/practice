pipeline{
  agent{
    node{
      label "AGENT"
    }
  }
  stages{
    stage('Build'){
      steps{
        echo "Building"
      }
    }
    stage('Test'){
      steps{
        echo "Testing"
      }
    }
    stage('Deploy'){
      steps{
        echo "Deploying"
      }
    }
  }
  post{
    always{
      echo "always say hi"
    }
    success{
      echo "say the build successful"
    }
    failure{
      echo "say the build failed"
    }
  }
}
