pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        jdk "Java11"
        maven "MAVEN"
    }
    
    environment {
        BLACKDUCK_URL="BLACKDUCK_URL%"
        BLACKDUCK_TOKEN="%BLACKDUCK_TOKEN%"
    }


    stages {
        stage('Get Code') {
            steps {
                git branch: 'main', url: 'https://github.com/sig-demo/insecure-bank/'   // Download code from GitHub             
            }
        }
        
        stage('Análise Black Duck') {
            steps {
                synopsys_detect detectProperties: '', downloadStrategyOverride: [$class: 'ScriptOrJarDownloadStrategy']
            }
        }        
        stage('Synopsys Polaris') {
            steps {
                polaris arguments: 'analyze -w', polarisCli: 'Polaris - Demo'// Run Polaris (SAST) analysis
            }
        }
    }
}
