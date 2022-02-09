import groovy.json.JsonOutput

pipeline{
   agent any //You can specify which stage/machine you want to execute, here any

    parameters{
       string(name: "SPEC", defaultValue: "cypress/integration/pom/**", description:"Enter the Script Path you want to execute")
       choice(name: "BROWSER", choices: ['electron','chrome', 'edge', 'firefox'], description: "Choose the browser in which you want to execute your scripts.")
    }//u can define any type of parameters string,boolean,passwords etc..
     //SPEC and BROWSER are 2 parameters, in SPEC you have to enter Script Path
     //in BROWSER you have to select browser
    
    options{
        ansiColor('xterm')
    }// to have better and colourful output in Console log output

    stages{
       stage('Build'){
           steps{
               echo "Buiding application"
           }
       }
       stage('Testing'){
           steps{
               bat "npm i"
               bat "npx cypress run --browser ${BROWSER} --spec ${SPEC}"
           }//bat - is like executing batch command in windows cmd/jenkins
       }
       stage('Deploy'){
           steps{
               echo "Deploying the application"
           }
       }
   }

   post{
       always{
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'cypress/report', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
       }
   }// Here post --- is a Post Build Action and
    // always -- No matter what happens to the rest of the pipeline script it always
    // runs the script in always{ ....} section.



   
}
