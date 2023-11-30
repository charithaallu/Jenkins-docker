### Multi-stage Jenkins pipeline where each stage runs on a different docker agent
pipeline {
  agent none
  stages {
    stage('Backend') {
      agent {
        docker { image 'maven:3.9.5-adoptopenjdk-11' }
      }
      steps {
        sh 'mvn clean package'
      }
    }
    stage('Frontend') {
      agent {
        docker { image 'node:16-alpine' }
      }
      steps {
        sh 'npm build'
      }
    }
  }
}
