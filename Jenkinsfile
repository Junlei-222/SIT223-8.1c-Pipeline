pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        // 如果是 Java 项目用 Maven，C# 项目用 MSBuild
        sh 'mvn clean package'          // 或者：bat 'msbuild Solution.sln'
      }
    }
    stage('Unit & Integration Tests') {
      steps {
        sh 'mvn test'                  // 或者：bat 'dotnet test'
      }
    }
    stage('Code Analysis') {
      steps {
        sh 'sonar-scanner'             // 需预装 Sonar Scanner
      }
    }
    stage('Security Scan') {
      steps {
        sh 'dependency-check.sh --project SIT223'
      }
    }
    stage('Deploy to Staging') {
      steps {
        sh './deploy-staging.sh'
      }
    }
    stage('Integration Tests on Staging') {
      steps {
        sh 'newman run postman_collection.json'
      }
    }
    stage('Deploy to Production') {
      steps {
        sh './deploy-prod.sh'
      }
    }
  }
}

