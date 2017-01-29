node{
    checkout scm
    def projPath = pwd() + "\\src\\Ardanis.Demo"

  	def pscmd = { String cmd ->
  		"powershell -NoProfile -ExecutionPolicy Bypass -Command \"${cmd}\""
  	}

    dir(projPath)
    {
      stage('Building it')
      {
        bat "rd /s /q published-app"
        bat "dotnet restore"
        bat "dotnet publish --output published-app --configuration Release"
        bat env.OCTOPUS_EXE + " pack --id Ardanis.Demo --version 1.0.0 --basePath published-app --overwrite"
        bat env.OCTOPUS_EXE + " push --package Ardanis.Demo.1.0.0.nupkg --replace-existing --server " + env.OCTOPUS_URL + " --apiKey " + env.OCTOPUS_API_KEY
      }
    }
}
