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
	 stage ('Deploy to server') {
            steps {
           sshagent(['application_server']) {
                sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/CDAC _Intern_Project/target/webgoat-2023.5-SNAPSHOT.jar root@65.2.191.49:/WebGoat'
                sh 'ssh -o  StrictHostKeyChecking=no root@65.2.191.49 "nohup java -jar /WebGoat/webgoat-server-v8.2.0-SNAPSHOT.jar &"'
              }
           }
    }
  }
}

