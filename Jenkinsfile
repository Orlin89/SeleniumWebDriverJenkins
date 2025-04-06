pipeline{
    agent any
	
	stages{
	    stage('Checkout git code'){
		    steps{
			    git branch: 'main', url: 'https://github.com/Orlin89/SeleniumWebDriverJenkins'
			}
		}
		
		stage('Setup dotnet 6'){
		    steps{
			    bat '''
				choco install dotnet-sdk -y --version=6.0.100
				'''
			}	
		}
		
		stage('Install nuget packages'){
		    steps{
			    bat 'dotnet restore SeleniumBasicExercise.sln'
			}
		}
		
		stage('Build project'){
		    steps{
			   bat 'dotnet build SeleniumBasicExercise.sln' 
			}
		}
		
		stage('Run tests for TestProject1'){
		    steps{
			   bat 'dotnet test TestProject1/TestProject1.csproj --logger "trx;LogFileName=TestResults.trx"'
			}
		}
		
		stage('Run tests for TestProject2'){
		    steps{
			   bat 'dotnet test TestProject2/TestProject2.csproj --logger "trx;LogFileName=TestResults.trx"'
			} 
		}
		
		stage(''){
		    steps{
			   
			}
		}
	}
	
	post{
	   always{
	       archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
		   step([
		       $class: 'MSTestPublisher',
			   testResultsFile: '**/TestResults/*.trx'
		   ])		  
	   }
	}
}