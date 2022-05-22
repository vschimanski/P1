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
             //slackSend(color: 'good', message:"Finished: SUCCESS :: Pipeline: ${env.JOB_NAME} Build Number: ${env.BUILD_NUMBER}  URL: ${env.BUILD_URL}", channel: 'development-internal', teamDomain: 'poolparty-diaries.slack.com', token: 'cAjMSrttm0V6kbeYhT5MTTnK')
         }
         failure {
             echo 'Post pipeline :::  failure'
          // slackSend(color: 'good', message:"Finished: FAILURE :: Pipeline: ${env.JOB_NAME} Build Number: ${env.BUILD_NUMBER}  URL: ${env.BUILD_URL}", channel: 'development-internal', teamDomain: 'poolparty-diaries.slack.com', token: 'cAjMSrttm0V6kbeYhT5MTTnK')
         }
         unstable {
            echo 'This will run only if the run was marked as unstable'
            //mail  body: "<b>Finished: UNSTABLE </b><br>Pipeline: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL : ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "Build Successful CI: Project name -> ${env.JOB_NAME}", to: "viacheslav.schimanski@semantic-web.com,dmitry.ershov@semantic-web.com";
         }
         changed {
             echo 'State of the Pipeline has changed'
            //echo 'This will run only if the state of the Pipeline has changed'
            // echo 'For example, if the Pipeline was previously failing but is now successful'
         }
     }

}