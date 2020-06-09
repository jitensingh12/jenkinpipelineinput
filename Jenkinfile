//def LABEL_ID = "yourappname-${UUID.randomUUID().toString()}"
def BRANCH_NAME = "master"
def GIT_URL = "https://github.com/jitensingh12/jenkinpipelineinput.git"
// Start Agent
node {
    stage('Checkout') {
        doCheckout(BRANCH_NAME, GIT_URL)
    }
    stage('Build') {
        echo 'hello'
        sh 'javac test.java'
    }
    stage('Tests') {
        echo 'hello test'
    }    
}
// Kill Agent
// Input Step
timeout(time: 2, unit: "MINUTES") {
    input message: 'Do you want to approve the deploy in production?', ok: 'Yes'
}
// Start Agent Again
node {
    doCheckout(BRANCH_NAME, GIT_URL) 
    stage('Deploy') {
        sh 'java test'
        echo 'successfully runned'
    }
}
def doCheckout(branchName, gitUrl){
    checkout([$class: 'GitSCM',
        branches: [[name: branchName]],
        doGenerateSubmoduleConfigurations: false,
        extensions:[[$class: 'CloneOption', noTags: true, reference: '', shallow: true]],
        userRemoteConfigs: [[credentialsId: 'b0f25a4f-9107-411b-85b2-ad7d4d89a6d4', url: gitUrl]]])
}
