pipeline {
  agent any
  stages {
    stage('Simple Test') {
      steps {
        echo "Test simple - pipeline fonctionne !"
        sh 'echo "Vérification Shell OK"'
        sh 'date'
      }
    }
  }
  post {
    always {
      echo 'Pipeline test terminé'
    }
  }
}
