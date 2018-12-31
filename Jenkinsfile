node {
  stage('Checkout') {
    checkout scm
    sh "ls -l"
    sh "False"
  }
  stage('Syntax') {
    sh "pylint *.py"
  }
}
