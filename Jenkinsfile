pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        jdk "Java11"
        maven "MAVEN"
    }

    stages {
        stage('Get Code') {
            steps {
                git branch: 'main', url: 'https://github.com/sig-demo/insecure-bank/'   // Download code from GitHub             
            }
        }
        
        stage('Análise Black Duck') {
            steps {
                bat 'echo %BLACKDUCK_URL%'
                bat 'echo ${env.BLACKDUCK_URL}'
                synopsys_detect detectProperties: '--blackduck.url="${env.BLACKDUCK_URL}" --blackduck.access.token="${env.BLACKDUCK_TOKEN}"', downloadStrategyOverride: [$class: 'ScriptOrJarDownloadStrategy']
            }
        }        
        stage('Synopsys Polaris') {
            steps {
                polaris arguments: 'analyze -w', polarisCli: 'Polaris - Demo'// Run Polaris (SAST) analysis
            }
        }
    }
}
