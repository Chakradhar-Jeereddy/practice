pipeline{
  agent{
    node{
      label "AGENT"
    }
  }
  environment{
    course = "jenkins"
    appVersion = ""
  }
  options{
    disableConcurrentBuilds()
  }
  stages{
    stage('Read Version'){
      steps{
        script{
            def packageJSON = readJSON file: 'package.json'
            appVersion = packageJSON.version
            echo "app version: ${appVersion}"
        }
      }
    }
    stage('Install dependencies'){
      steps{
          sh"""
          sudo npm install
          sudo dnf install openssl -y
          sudo dnf install openssl-libs -y
          sudo dnf install openssh -y 
          sudo dnf install openssh-server -y
          sudo dnf install openssh-clients -y
          """
      }
    }
    stage('Build Image'){
      steps{
        script{
           sh"""
            docker build -t chakradhar05:${appVersion} .
            docker images
           """
        }
      }
    }
    stage('Deploy'){
      when{
        expression { "${params.Deploy}" == "true" }
      }
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
