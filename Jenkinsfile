node{
    
    stage('Clone repo'){
        git branch: 'main', credentialsId: 'Partha-GitHub-Credentials', url: 'https://github.com/DevOpsAirflow/devsecops-class-java-cicd.git'
    }
    
    stage('Maven Build'){
        def mavenHome = tool name: "Maven-3.9.1", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
    }
    
    stage('SonarQube analysis') {       
        withSonarQubeEnv('sonar-server-8.3') {
        def mavenHome = tool name: "Maven-3.9.1", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
       	sh "${mavenCMD} sonar:sonar"    
        }	
    }
        
    stage('upload war to nexus'){
	steps{
		nexusArtifactUploader artifacts: [	
			[
				artifactId: '01-maven-web-app',
				classifier: '',
				file: 'target/01-maven-web-app.war',
				type: war		
			]	
		],
		credentialsId: 'nexus3',
		groupId: 'in.javacicd',
		nexusUrl: '',
		protocol: 'http',
		repository: 'java-cicd-release'
		version: '1.0.0'
	}
}
    
    stage('Deploy'){
        
    }
}
