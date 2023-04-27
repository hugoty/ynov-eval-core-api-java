pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'add-pipeline-docker', url: 'https://github.com/hugoty/ynov-eval-core-api-java'
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

   stage('Push sur le registry docker via jib') {
               steps {
                   // push sur le registry Docker via Jib
                   bat './gradlew jib --image=nexus-ynov-sandbox.asys-cloud.fr/repository/ynov-docker/${project.name}:${version} --username=jenkins --password=hDkxFxBSwmQ3ANLBFt'
               }
           }
    }
  }



