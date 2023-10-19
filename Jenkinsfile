pipeline {
	agent any
  	stages {
  stage ('Check secrets') {
    steps {
      sh 'trufflehog3 https://github.com/chaudharysurya14/WebGoat_DevSecOps.git -f json -o truffelhog_output.json || true'
          }
    }
      stage('Check Dependency') {
            steps {
                dependencyCheck additionalArguments: ' --scan ./ ', odcInstallation: 'DP-Check'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
	stage ('Static analysis') {
      steps {
        withSonarQubeEnv('sonarqube') {
          sh 'mvn sonar:sonar'
        //sh 'sudo python3 Devsecops.py'
	}
      }
    }
	     stage('Generate and build') {
            steps {
                sh "mvn compile"
            }
        }


  }
}

