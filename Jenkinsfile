pipeline {
  agent any
  stages {
    stage('Test 1') {
      steps {
        echo "Étape 1 - pipeline démarre"
      }
    }
    stage('Test 2') {
      steps {
        echo "Étape 2 - exécution shell"
        sh 'pwd'
        sh 'ls -la'
      }
    }
  }
  post {
    always {
      echo 'Pipeline terminé avec succès'
    }
  }
}
