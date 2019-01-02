pipeline {  
	agent any
    stages { 
	    stage('Checkout_Code') {
		 steps {
		    echo 'Checkout code..'
				checkout([$class: 'GitSCM', branches: [[name: 'master']], doGenerateSubmoduleConfigurations: false, submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/nmadaan/demo-rf.git']]])
		 }
		}
	    stage ('Execute RF tests'){
	        steps {
			withEnv(["PATH+PYTHON=C:/Windows/System32;C:/Python27;C:/Python27/Scripts"]) 
					{
					bat '''
					    @echo off
						echo #######################################
						echo # Running tests first time #
						echo #######################################
						cmd /c robot "%WORKSPACE%\\tests.robot"
						'''
					}

            }
		post {
			always {
			 step([
						  $class: 'RobotPublisher',
						  outputPath: 'reports',
						  outputFileName: 'output.xml',
						  reportFileName: 'report.html',
						  logFileName: 'log.html',
						  otherFiles: '*.png',
						  disableArchiveOutput: false,
						  unstableThreshold: 50.0,
						  passThreshold: 50.0,
						  onlyCritical: true
				  ])
			  }
			}
	    }
    }
}
