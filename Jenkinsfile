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
    stage("Publish the code coverage report") {
      steps {
        sh 'mvn jacoco:report'
      }
      post {
        always {
          jacoco execPattern: '**/target/jacoco.exec', classPattern: '**/target/classes', sourcePattern: '**/src/main/java', exclusionPattern: '', changeBuildStatus: true
        }
      }
    }
    stage("Sonarquebe integration") {
      steps {

      }
    }
  }
}
