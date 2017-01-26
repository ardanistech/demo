node{
  	def pscmd = { String cmd ->
  		"powershell -NoProfile -ExecutionPolicy Bypass -Command \"${cmd}\""
  	}

    stage('Is powershell working?'){
      bat pscmd('Get-ChildItem')
    }
}
