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
}
