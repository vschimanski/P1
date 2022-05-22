pipeline {
    agent any

    environment {
        MVN_HOME = tool name: 'Maven3', type: 'hudson.tasks.Maven$MavenInstallation'
        PROJECT_VERSION=""
    }

   stages {



        stage('Build') {

                    steps {

                        sh '${MVN_HOME}/bin/mvn clean install -Dmaven.javadoc.skip=true'
                    }
           }


           stage('Run') {

                    steps {

                        sh 'java -jar target/P*.jar'
                    }
           }




            stage('Zip') {
                 steps {
                    script {
                             env.FILENAME = readFile 'target/classes/version.txt'
                                }
                                   sh 'zip target/P1-${env.FILENAME}.zip target/P1-${env.FILENAME}}.jar'

                               }
                      }

            stage('Upload') {

               steps {
                        script {
                                   env.FILENAME = readFile 'target/classes/version.txt'
                               }

                        sh 'cp target/P1-${env.FILENAME}.zip /tmp'
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