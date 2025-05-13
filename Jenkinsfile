pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        // Windows 上使用 bat 执行构建
        bat 'mvn clean package'          // 如果是 C# 项目可改为：bat 'msbuild Solution.sln'
      }
    }
    stage('Unit & Integration Tests') {
      steps {
        bat 'mvn test'                  // 或者：bat 'dotnet test'
      }
    }
    stage('Code Analysis') {
      steps {
        // 假设已在系统中安装 Sonar Scanner，并且配置了环境变量
        bat 'sonar-scanner'
      }
    }
    stage('Security Scan') {
      steps {
        // OWASP Dependency-Check 脚本
        bat 'dependency-check.bat --project SIT223'
      }
    }
    stage('Deploy to Staging') {
      steps {
        // 自定义的部署脚本
        bat 'deploy-staging.bat'
      }
    }
    stage('Integration Tests on Staging') {
      steps {
        // 使用 Newman 运行 Postman 接口测试
        bat 'newman run postman_collection.json'
      }
    }
    stage('Deploy to Production') {
      steps {
        bat 'deploy-prod.bat'
      }
    }
  }
}

