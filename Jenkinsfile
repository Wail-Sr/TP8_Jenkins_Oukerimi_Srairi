pipeline {
  agent any
  stages {
    stage('Build') {
      post {
        failure {
          mail(subject: 'La phase Build', body: 'La phase Build a ete execute avec echec', to: 'ia_srairi@esi.dz')
        }

        success {
          mail(subject: 'La phase Build', body: 'La phase Build a ete execute avec success', to: 'ia_srairi@esi.dz')
        }

      }
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/*.*'
        junit 'build/test-results/test/*.*'
      }
    }

    stage('Code Analysis') {
      steps {
        bat 'gradle sonarqube'
        qualitygate = waitForQualityGate()
        if (qualitygate.status != "OK") {
           mail(subject: 'La phase Code Analysis', body: 'Quality gate failed', to: 'ia_srairi@esi.z', cc: 'ia_srairi@esi.dz')
        }
      }
    }

  }
}