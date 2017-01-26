node{
    def projPath = pwd() + "\\src\\Ardanis.Demo"

  	def pscmd = { String cmd ->
  		"powershell -NoProfile -ExecutionPolicy Bypass -Command \"${cmd}\""
  	}

    dir(projPath)
    {
      stage('Building it')
      {
        bat "dotnet publish --output published-app --configuration Release"
      }
    }
}
