node {
  stage('Checkout') {
    checkout scm
    sh "ls -l"
  }
  stage('Syntax') {
    sh "pylint *.py"
  }
}
