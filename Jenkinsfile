pipeline {
  agent any

  tools {
    maven 'Maven'
  }

  environment {
        MAVEN_OPTS = '-Dnet.bytebuddy.experimental=true -XX:+EnableDynamicAgentLoading'
  }

  stages {
    stage("code checkout") {
      steps {
        git branch: 'master', url:'https://github.com/Sumanth-H20/Test-Project.git'
      }
    }
    stage("compile") {
      steps {
        sh 'mvn clean compile'
      }
    }
    stage("Test") {
      steps{
        sh 'mvn test'
      }
    }
    stage("Build") {
      steps {
        sh 'mvn clean package -DskipTests=true'
      }
    }
  }
}
