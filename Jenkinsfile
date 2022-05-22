pipeline {
    agent any

    environment {
        MVN_HOME = tool name: 'Maven3', type: 'hudson.tasks.Maven$MavenInstallation'
       def PROJECT_VERSION = 'UNKNOWN'
        zipCommand1="zip target/P1-"
        zipCommand2="target/P1-"
        zipCommand3=".jar"
        zipCommand4=".zip"

         def var1="cp target/P1-"
         def var2=".zip /tmp"

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


            stage("readFile") {
                        steps {
                            script {

                                 PROJECT_VERSION = sh(returnStdout: true, script: 'cat target/classes/version.txt').trim()

                            }

                            echo "${PROJECT_VERSION}"

                         }
                        }


            stage('Zip') {
                 steps {


                               echo '${PROJECT_VERSION}'
                                echo 'zip stage'
                                //  sh "zip target/P1-"${PROJECT_VERSION}".zip target/P1-"${PROJECT_VERSION}".jar"
                                //sh ${zipCommand1}${PROJECT_VERSION}${zipCommand4}${zipCommand2}${PROJECT_VERSION}${zipCommand3}
                               }
                      }

            stage('Upload&Deliver') {

               steps {

                      echo "${PROJECT_VERSION}"

                      sh '$vair1${PROJECT_VERSION}$var2'
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