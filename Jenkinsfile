pipeline {
  agent any
  tools {
    maven 'Maven-3.9.9' // 这里必须和你在 Jenkins 设置时填写的名字一致！
  }
  stages {
    stage('Build') {
      steps {
        bat 'mvn -v'
        bat 'mvn clean package'
      }
    }
    stage('Finish') {
      steps {
        bat 'echo Pipeline finished successfully!'
      }
    }
  }
}


