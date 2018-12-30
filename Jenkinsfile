node 
 {
  node {
    dir('pipeline_handover') {
        checkout([$class: 'GitSCM', 
branches: [[name: "origin-pull/$GITHUB_PR_NUMBER/$GITHUB_PR_COND_REF"]], 
doGenerateSubmoduleConfigurations: false,
extensions: [], 
submoduleCfg: [],
userRemoteConfigs: [
                [credentialsId: "${GITHUB_AUTH}",
name: 'origin-pull',
refspec: "+refs/pull/$GITHUB_PR_NUMBER/*:refs/remotes/origin-pull/$GITHUB_PR_NUMBER/*",
url: "${GITHUB_PROJECT}"]]])
    }
    load 'pipeline_handover/Jenkinsfile'
    
  stage('Checkout') {
    checkout scm
    sh "ls -l"
  }
  stage('Syntax') {
    sh "pylint *.py"
  }
}
