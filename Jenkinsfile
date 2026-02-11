pipeline {
  agent {
    docker {
      image 'mcr.microsoft.com/dotnet/sdk:7.0'
      args '-e DOTNET_CLI_HOME=/tmp -e HOME=/tmp -e DOTNET_SKIP_FIRST_TIME_EXPERIENCE=1 -e DOTNET_CLI_TELEMETRY_OPTOUT=1'
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