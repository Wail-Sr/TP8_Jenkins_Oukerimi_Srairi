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
        withSonarQubeEnv('sonar') {
          bat 'gradle sonarqube'
        }
        waitForQualityGate abortPipeline: true
      }

      post {
        failure {
          mail(subject: 'La phase Code Analysis', body: 'Quality gate failed', to: 'ia_srairi@esi.dz', cc: 'ia_srairi@esi.dz')
        }

      }
    }

  }
}