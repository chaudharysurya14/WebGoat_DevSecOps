pipeline {
	agent any
	  tools{
        jdk 'java11'
        maven 'maven3'
        // sonarqube scanner 'sonarqube'
    }
    stages {
      stage('SonarQube Analysis') {
        steps{  // def mvn = tool 'Default Maven';
          withSonarQubeEnv('sonarqube') {
            sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=hello_world_pipeline -Dsonar.projectName='hello_world_pipeline'"
         }
       }
     }
  }
}
// pipeline {
// 	agent any
//   	stages {
//   stage ('Check secrets') {
//     steps {
//       sh 'trufflehog3 https://github.com/chaudharysurya14/WebGoat_DevSecOps.git -f json -o truffelhog_output.json || true'
//           }
//     }
//       stage('Check Dependency') {
//             steps {
//                 dependencyCheck additionalArguments: ' --scan ./ ', odcInstallation: 'DP-Check'
//                 dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
//             }
//         }
// 	stage ('Static analysis') {
//       steps {
//         withSonarQubeEnv('sonarqube') {
//           sh 'mvn sonar:sonar'
//         //sh 'sudo python3 Devsecops.py'
// 	}
//       }
//     }
//    stage('Generate and build') {
//  steps {
//      sh "mvn compile"
//             }
//         }
//  stage ('Deploy to server') {
// steps {
// sshagent(['application_server']) {
//       sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/CDAC_Intern_Project/target/webgoat-server-v8.2.0.jar root@192.168.80.22:~/WebGoat'
//       // sh 'ssh -o  StrictHostKeyChecking=no root@192.168.80.22 "lsof -i :8088 -t"'
//       // sh 'ssh -o  StrictHostKeyChecking=no root@192.168.80.22 "sudo fuser 8080/tcp"'
//       sh 'ssh -o  StrictHostKeyChecking=no root@192.168.80.22 "nohup java -jar /root/WebGoat/webgoat-server-v8.2.0.jar --server.address=0.0.0.0 --server.port=8088 &"'
//           }
//         }
//       }
//     stage ('Dynamic analysis') {
//             steps {
//            sshagent(['application_server']) {
//                 sh 'ssh -o  StrictHostKeyChecking=no root@192.168.80.22 "sudo docker run --rm -v /root:/zap/wrk/:rw -t owasp/zap2docker-stable zap-full-scan.py -t http://192.168.80.22:8088/WebGoat -x zap_report || true"'
// 	   }
//         }
//      }
//   }
// }

