pipeline {
  agent any

  stages {
  stages {
      stage('Checkout') {
        steps {
          git branch: 'main', url: 'https://github.com/hugoty/ynov-eval-core-api-java'
        }
      }
      stage('Build') {
            steps {
              sh './gradlew clean build'
            }
          }


      stage('Spotless Apply') {
        steps {
          // Exécution de la tâche spotlessApply
          sh './gradlew spotlessApply'
        }
      }

     stage('Test') {
            steps {
              sh './gradlew test'
            }
          }
    stage('Gradle Build') {
      steps {
        // Exécution de la vérification Spotless
        sh './gradlew spotlessCheck'

        // Compilation du code
        sh './gradlew clean build'
      }
    }
  }
stage('Deploy') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'nexus-credentials', usernameVariable: 'NEXUS_USERNAME', passwordVariable: 'NEXUS_PASSWORD')]) {
          sh './gradlew publish -PnexusUsername=$NEXUS_USERNAME -PnexusPassword=$NEXUS_PASSWORD'
        }
      }
    }
  post {
    always {
      // Archivage des artefacts
      archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
    }
  }
}
