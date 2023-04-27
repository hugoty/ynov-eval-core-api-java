pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'add-pipeline-jar', url: 'https://github.com/hugoty/ynov-eval-core-api-java'
      }
    }
    stage('Build') {
      steps {
        bat './gradlew clean build'
      }
    }
    stage('Spotless Apply') {
      steps {
        // Exécution de la tâche spotlessApply
        bat './gradlew spotlessApply'
      }
    }
    stage('Test') {
      steps {
        bat './gradlew test'
      }
    }
 stage('Archive Artifacts') {
       steps {
         archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
       }
     }

    stage('Deploy') {
      steps {
        bat './gradlew publish '
      }
    }
  }


}
