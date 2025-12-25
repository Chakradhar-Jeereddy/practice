Follow catalogue documentation:
===
 https://github.com/daws-86s/roboshop-documentation/blob/main/02-catalogue.MD
- Install required softwares on Jenkin's agent to build the catalogue image
```
sudo dnf module disable nodejs -y
sudo dnf module enable nodejs:20 -y
sudo dnf install nodejs -y
```
- Update the version in package.json file.
-   "version": "1.1.0"
-   We need to read this version, need a plugin to read package json in jenkins pipeline
-   def packageJson = readJSON file: 'package.json'
-   Need pulgin ***Pipeline Utility Steps*** to get the above function.
```
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
    stage('Test'){
      steps{
          sh"""
          echo $course
          """
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
  }
}
```
***add a new stage***
- Install dependencies
- npm conflicts with openssl, therefore installing dependencies for openssl.
```
stage('Install dependencies'){
      steps{
          sh"""
          npm install
          dnf install openssl -y
          dnf install openssl-libs -y
          dnf install openssh -y 
          dnf install openssh-server -y
          dnf install openssh-clients -y
          """
      }
}
```

***Install docker on Jekins agent:***
```
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo systemctl daemon-reload
sudo systemctl start docker
sudo systemctl status docker
sudo systemctl enable docker
sudo usermod -G docker ec2-user
reconnect agent in jenkins after docker is installed
```
***add Another stage to build image***
```
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
```




