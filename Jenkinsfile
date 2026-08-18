@Library('jenkins-shared-library') _ 

// /vars/nodeJSEKSPipeline
def mymap = [
     project: 'roboshop',
     component: 'catalogue',
     acc_id: '406682759639'
]

if( ! env.BRANCH_NAME.equalsIgnoreCase('main') ){
      nodeJSEKSPipeline(mymap)
}
else{
  echo "Please fallow the CR process"
}