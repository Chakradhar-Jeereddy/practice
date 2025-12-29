library 'jenkins-shared-library'

// below function will pass the arguments to the pipeline in shared library
def configMap : [
    project: 'roboshop'
    component: 'catalogue'
]

// If this is not master branch
if (! env.BRANCH_NAME.equalsIgnoreCase('main')) {
    nodeJSEKSPipeline('configMap')
} else {
    echo "Please follow the CR process"
}