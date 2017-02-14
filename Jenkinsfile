node{
    stage('Checkout SCM')
    {
      checkout scm
    }
    def projPath = pwd() + "\\src\\Ardanis.Demo"
    def projectName = "Ardanis.Demo"
    def version = "1.0.$BUILD_NUMBER"
    def packageName = "${projectName}.${version}.nupkg"
    def octopusProject = "DTS2017-Demo"

    dir(projPath)
    {
      stage('Building')
      {
        bat "dotnet restore"
        bat "dotnet publish --output published-app --configuration Release"
      }
      stage('Packaging')
      {
        bat "$OCTOPUS_EXE pack --id $projectName --version $version --basePath published-app --overwrite"
        bat "$OCTOPUS_EXE push --package $packageName --replace-existing --server $OCTOPUS_URL --apiKey $OCTOPUS_API_KEY"
      }
      stage('Release creation')
      {
        bat "$OCTOPUS_EXE create-release --project $octopusProject --version $version --server $OCTOPUS_URL --apiKey $OCTOPUS_API_KEY"
      }
    }
}
