pipeline {
  agent { docker { image 'mcr.microsoft.com/dotnet/sdk:7.0'; args '--rm -v jenkins-nuget-cache:/root/.nuget/packages' } }
  stages {
    stage('Checkout') { steps { checkout scm } }
    stage('Restore')  { steps { sh 'dotnet restore' } }
    stage('Build')    { steps { sh 'dotnet build -c Release --no-restore' } }
    stage('Test')     { steps { sh 'dotnet test --no-build --verbosity normal' } }
    stage('Publish')  { steps { sh 'dotnet publish -c Release -o out'; archiveArtifacts artifacts: 'out/**' } }
  }
  post { always { echo 'Pipeline terminé' } }
}
