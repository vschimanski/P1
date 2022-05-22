pipeline {
    agent any

    environment {
        MVN_HOME = tool name: 'Maven3', type: 'hudson.tasks.Maven$MavenInstallation'
    }

   stages {



        stage('Build') {

                    steps {

                        sh '${MVN_HOME}/bin/mvn -T4C clean install -Dmaven.javadoc.skip=true'
                    }
           }


    }
     post {
         always {
             echo 'Post pipeline ::: END'
             deleteDir()
           }
         success {
             echo 'Post pipeline ::  successful'
         }
         failure {
             echo 'Post pipeline :::  failure'
          }
         unstable {
            echo 'This will run only if the run was marked as unstable'
          }
         changed {
             echo 'State of the Pipeline has changed'
             }
     }

}