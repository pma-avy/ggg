pipeline {
  agent any
  stages {
    stage('setup') {
      steps {
        properties([parameters([choice(choices: ['61', '62'], description: '', name: 'ENV1')])])
        echo 'hello'
      }
    }
  }
}
