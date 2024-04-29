pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
				sh 'mvn -B -DskipTests clean package'
			}
		}
		stage('Doc') {
			steps {
				sh 'mvn javadoc:jar'
			}
		}
		stage('pmd') {
			steps {
				sh 'mvn pmd:pmd'
			}
		}
		stage('Test report') {
			steps {
				sh 'mvn surefire-report:report'
			}
		}
	}

	post {
		always {
			archiveArtifacts artifacts: '**/target/surefire-reports/**', fingerprint: true
			archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
			archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
		}
	}
}
