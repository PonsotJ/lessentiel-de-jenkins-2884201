pipeline {
  agent {
    docker {
      image 'mcr.microsoft.com/dotnet/sdk:7.0'
      args '-v /var/jenkins_home/.nuget:/root/.nuget'
      reuseNode true
    }
  }
  stages {
    stage('Build') {
      steps {
        sh 'dotnet build eShopOnWeb.sln'
      }
    }

    stage('Tests') {
      parallel {
        stage('Unit') {
          steps {
            sh 'dotnet test tests/UnitTests'
          }
        }

        stage('Integration') {
          steps {
            sh 'dotnet test tests/IntegrationTests'
          }
        }

        stage('Functional') {
          steps {
            sh 'dotnet test tests/FunctionalTests'
          }
        }
      }
    }

    stage('Deployment') {
      steps {
        sh 'dotnet publish eShopOnWeb.sln -o out'
        echo 'Artifacts published to out/ folder'
      }
    }
  }

  post {
    always {
      echo 'Pipeline completed'
    }
  }
}
