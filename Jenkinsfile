pipeline{
    agent{
        node{
            label "agent"
        }
    }
    options{
        disableConcurrentBuilds()
    }
    environment{
        appVersion = ""
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        booleanParam(name: 'Deploy', defaultValue: false, description: 'Do you want to deploy?')

    }
    stages{
        stage('Read appVersion'){
            steps{
              script{
              def packageJSON = readJSON file: 'package.json'
              appVersion = packageJSON.version
              }
            }
        }
        stage('Build catalogue image'){
            steps{     
               sh"""
               docker build -t chakradhar05/catalogue:${appVersion} .
               docker images
               """
            }
        }
        stage('Test'){
            steps{
              sh"""
              echo "Testing"
              sleep 10
              """
            }
        }
        stage('Deploy'){
            when{
                expression { "${params.Deploy}" == "true" }
            }
            steps{
                 echo "Deploying"
            }
        }
    }
    post{
        always{
            echo "Deployment is completed"
            cleanWs()
        }
    }
}