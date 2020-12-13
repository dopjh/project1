node {
    
	

    def newApp
    def registry = 'dopjh/project1'
    def registryCredential = 'dopjh'
	
	stage('Git') {
		git 'https://github.com/dopjh/project1.git'
	}
	stage('Build') {
		sh 'npm install'
		sh './node_modules/.bin/bower install'
	}
	stage('Test') {
		sh 'npm test'
	}
	stage('Building image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
	}
	stage('Registring image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
    		newApp.push 'latest2'
        }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
