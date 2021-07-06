pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello World"'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
             }
         }
         stage('Setup'){
             steps{
                 sh '''
                    python3 -m venv ~/.devops
                    source ~/.devops/bin/activate
                    pip install --upgrade pip &&\
		                    pip install -r requirements.txt
                '''
             }
         }
         stage('Deliver for development') {
            when {
                branch 'develop'
            }
            steps {
              script{


                  def subject = "${env.JOB_NAME} - Build #${env.BUILD_NUMBER}"
					        def content = '${JELLY_SCRIPT,template="html"}'
					        // send email
					        emailext(body: content, mimeType: 'text/html',
						        replyTo: '$DEFAULT_REPLYTO', subject: subject,
						        to: '$DEFAULT_RECIPIENTS', attachLog: true )

                }
              }
            }
         
        }
}
