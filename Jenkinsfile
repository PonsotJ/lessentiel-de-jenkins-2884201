pipeline {
  agent {
    docker {
      image 'mcr.microsoft.com/dotnet/sdk:7.0'
      args '--rm -v jenkins-nuget-cache:/root/.nuget/packages'
    }
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        sh 'dotnet build eShopOnWeb.sln'
      }
    }

    stage('Tests') {
      parallel {
        stage('Unit') {
          steps {
            sh 'dotnet test tests/UnitTests --logger "trx;LogFileName=unit-results.trx"'
          }
        }

        stage('Integration') {
          steps {
            sh 'dotnet test tests/IntegrationTests --logger "trx;LogFileName=integration-results.trx"'
          }
        }

        stage('Functional') {
          steps {
            sh 'dotnet test tests/FunctionalTests --logger "trx;LogFileName=functional-results.trx"'
          }
        }
      }
    }

    stage('Deployment') {
      steps {
        sh 'dotnet publish eShopOnWeb.sln -o out'
        archiveArtifacts artifacts: 'out/**', fingerprint: true
      }
    }
  }

  post {
    always {
      junit '**/TestResults/*.trx' || true
      echo 'Pipeline eShopOnWeb completed'
    }
  }
}
