node {
    // Define Maven tool location
    def mavenHome = tool name: "maven3.9.10"

    // Print Jenkins environment info
    echo "GitHub Branch Name: ${env.BRANCH_NAME}"
    echo "Jenkins Job Number: ${env.BUILD_NUMBER}"
    echo "Jenkins Node Name: ${env.NODE_NAME}"
    echo "Jenkins Home: ${env.JENKINS_HOME}"
    echo "Jenkins URL: ${env.JENKINS_URL}"
    echo "Job Name: ${env.JOB_NAME}"

    // Set build properties
    properties([
        [$class: 'JiraProjectProperty'],
        buildDiscarder(logRotator(
            artifactDaysToKeepStr: '', 
            artifactNumToKeepStr: '2', 
            daysToKeepStr: '', 
            numToKeepStr: '2')
        ),
        pipelineTriggers([
            pollSCM('* * * * *') // Poll every minute (adjust as needed)
        ])
    ])

    stage("Checkout Code from Git") {
        git branch: 'development', 
            credentialsId: '65fb834f-a83b-4fe7-8e11-686245c47a65', 
            url: 'https://github.com/MithunTechnologiesDevOps/maven-web-application.git'
    }

    stage("Build with Maven") {
        sh "${mavenHome}/bin/mvn clean package"
    }
}
