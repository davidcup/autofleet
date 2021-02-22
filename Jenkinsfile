import groovy.json.JsonOutput
import groovy.json.JsonSlurper
import hudson.tasks.test.AbstractTestResultAction
import hudson.tasks.junit.CaseResult

def version = "1.0"
def slackNotificationChannel = "#alerts"
def author = ""
def message = ""
def testSummary = ""
def total = 0
def failed = 0
def skipped = 0




def getLastChangedFiles = {
    def files = sh(returnStdout: true, script: 'git diff  HEAD')
    author = sh(returnStdout: true, script: "git --no-pager show -s --format='%an' ${commit}").trim()
}

def getLastCommitMessage = {
    message = sh(returnStdout: true, script: 'git log -1 --pretty=%B').trim()
}

def populateGlobalVariables = {
    getLastCommitMessage()
    getLastChangedFiles()   
}


pipeline {
	
	environment {
        BUILD_USER = ''		
    }

    options { 
          disableConcurrentBuilds() 
	      buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
		  timestamps()
	}

    agent {
		node {
		  label 'dotnetcore'
		  customWorkspace '/home/david/jenkins/workspace/autofleet'
		}
    }	
  
    stages {
						
	    stage('\u278A Init') {		
             steps {
				script{		
				     
				    def repoName = env.GIT_URL.replaceFirst(/^.*\/([^\/]+?).git$/, '$1')
				    populateGlobalVariables()
                   		 
				}
			 }
	    }
		  
		
		  
        stage('\u278C Build') {
            steps {												
					echo "Detected Git"
            }
        }
		
		
		
    }
	
	post {
        success {
			script {                
				echo "Detected Git"
            }
            
        }
        failure {
             script {                
				echo "Detected Git"
            }
        }
        unstable {
             script {              
				echo "Detected Git"
            }
        }
    }
  
}

