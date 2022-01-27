pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc'
        junit 'build/test-results/test'
        mail(subject: 'La phase Build', body: 'La phase Build a ete execute', to: 'ia_srairi@esi.dz')
      }
    }

  }
}