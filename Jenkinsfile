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

        stage('Integration / Shell Script') {
          steps {
            sh 'dotnet test tests/IntegrationTests'
          }
        }

        stage('Functionnal') {
          steps {
            sh 'dotnet test tests/functionnalTests'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh 'dotnet publish eShopOnWeb.sln -o /var/aspnet'
      }
    }

  }
}