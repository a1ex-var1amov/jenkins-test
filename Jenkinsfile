node {
  stage('Checkout') {
    checkout scm
    sh "ls -l"
    sh "env"
  }
  stage('Syntax') {
    sh "pylint *.py"
  }
  stage('pre-False') {
    sh 'False'
  }
  stage('False') {
    sh "false"
  }
}
