node {

  // config 
  def to = emailextrecipients([
          [$class: 'CulpritsRecipientProvider'],
          [$class: 'DevelopersRecipientProvider'],
          [$class: 'RequesterRecipientProvider']
  ])

  // job
  try {
    stage('Build') {
        
            sh 'echo "Hello World"'
            sh '''
                echo "Multiline shell steps works too"
                ls -lah
            '''
        
    }
    stage('Setup'){
        
            sh '''
            python3 -m venv ~/.devops
            source ~/.devops/bin/activate
            pip install --upgrade pip &&\
                    pip install -r requirements.txt
        '''
        
    }
    def subject = "${env.JOB_NAME} - Build #${env.BUILD_NUMBER} "
    def content = '${JELLY_SCRIPT,template="html"}'

    // send email
      emailext(body: content, mimeType: 'text/html',
         replyTo: '$DEFAULT_REPLYTO', subject: subject,
         to: '$DEFAULT_RECIPIENTS', attachLog: true )
        
  } 
}