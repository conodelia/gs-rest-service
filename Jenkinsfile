properties([ pipelineTriggers([ githubPush()])])
node  {
	stage('Source') { // for display purposes
	    // Get some code from our Git repository
	    //git 'https://github.com/conodelia/gs-rest-service'
	     git 'https://github.com/conodelia/gs-rest-service'
     }
    stage('Build') {
        // TO-DO: Execute the gradle build associated with this project
        //sh 'echo gradle build will go here' 
        sh './gradlew build'
    }

    try {
        stage('Test') {
            // TO-DO: Execute the gradle build associated with this project
            //sh 'echo gradle build will go here' 
            sh './gradlew check'
            sh 'touch build/test-results/**/*.xml'
        } 
    } finally {
        junit 'build/test-results/**/*.xml'
    }
    
    try {
        stage("Sonarqube") {
            sh './gradlew clean sonarqube -Dsonar.host.url=http://192.168.2.74:9000 -Dsonar.login=69e802c293441691578970cedaed34518c4bff20 -Dsonar.groovy.jacoco.reportPath=build/jacoco/test.exec'
        }
    } catch (e) { print 'mailing'
        step([$class: 'WsCleanup'])
        return
    }
    
    
}

