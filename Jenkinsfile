pipeline {
   agent any
   tools {
      // Install the Maven version configured as "M3" and add it to the path.
      maven "M3"
   }
   stages {

      stage('Build') {
         steps {
            // Run Maven on a Unix agent.
            sh "mvn -Dmaven.test.failure.ignore=true clean package"

         }
       }

      stage('Test') {
         steps {
               // Run Maven on a Unix agent.
            sh "mvn test"
         }

		 post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }

       }
      stage('Deploy') {
         steps {
		sh "java -jar /var/lib/jenkins/workspace/Saurabh-java-project/target/my-app-1.0-SNAPSHOT.jar"
         }
      }
    }
}
