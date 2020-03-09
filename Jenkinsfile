pipeline{
agent any
  stages{
    stage('SCM'){
      steps{
        git 'https://github.com/thunikipatla/OpenMRS.git'
      }
    }
    stage('Build'){
      steps{
        sh ''' mvn package '''
      }
    }
    stage('Archive-Artifacts'){
      steps{
        archiveArtifacts 'webapp/target/openmrs*'
      }
    }
    /* stage('Sonar-Stage'){
      steps{
        withSonarQubeEnv('sonar'){
            sh 'mvn clean package sonar:sonar'
        }
  }
 }
  stage('Quality-gate'){
      steps{ 
        sleep(60)
        script {
        qg=waitForQualityGate('sonarQuality')
        if (qg.status == 'OK'){
         echo "Quality gate passed"
        //error "Pipeline aborted due to quality gate check ${qg.status}"
        }
        else {
            error "The pipeline fialed due to my quality gate check"
        }
        }
         }
  } */
  /*stage('upload-artifacts'){
      steps {
        nexusArtifactUploader artifacts: [[artifactId: 'dev', classifier: '', file: "./webapp/target/openmrs.war", type: 'war']], credentialsId: 'nexus', groupId: 'dev_group', nexusUrl: '192.168.34.11:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'RepoR', version: '${BUILD_NUMBER}'
      }
  } */
  stage('Call-Deploy'){
  steps {
   build job: 'deploy-war', propagate: false, wait: false
  }
   }
}
}
