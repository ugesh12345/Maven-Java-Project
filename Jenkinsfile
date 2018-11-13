#!groovy

node {
    currentBuild.result = "SUCCESS"

    try {

       stage('Checkout'){

          checkout scm
       }

       stage('Compiling'){
	       def mvn_version = 'maven'
         withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] )
	       {

          sh 'mvn clean install'
	       }
       }
	   
      stage('Sonar') {
                    //add stage sonar
	      def mvn_version = 'maven'
         withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] )
	      {
                    sh 'mvn sonar:sonar'
	      }
                }
	    
	stage('Checkstyle') {
		def mvn_version = 'maven'
         withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] )
		{
                    sh 'mvn checkstyle:checkstyle'
		}
                }

               stage('PMD') {
		       def mvn_version = 'maven'
         withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] )
		       {
                    sh 'mvn pmd:check'
		       }
                }
      /* stage('mail'){

         mail body: 'project build successful',
                     from: 'devopstrainingblr@gmail.com',
                     replyTo: 'mithunreddytechnologies@gmail.com',
                     subject: 'project build successful',
                     to: 'mithunreddytechnologies@gmail.com'
       }*/
	    
	    

    }
    catch (err) {

        currentBuild.result = "FAILURE"

           /* mail body: "project build error is here: ${env.BUILD_URL}" ,
            from: 'devopstrainingblr@gmail.com',
            replyTo: 'mithunreddytechnologies@gmail.com',
            subject: 'project build failed',
            to: 'mithunreddytechnologies@gmail.com'
            */
        throw err
    }
}
