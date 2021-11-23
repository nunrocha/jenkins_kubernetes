def generateStage(job) {
    return {
        stage("stage: ${job}") {
                echo "This is ${job}."
        }
    }
}
 
pipeline {
    agent { label 'master' }
 
    stages {
        stage('Create List of Stages to run in Parallel') {
            steps {
                script {
                    def list = ["Test-1", "Test-2", "Test-3", "Test-4", "Test-5"]
                    // you may create your list here, lets say reading from a file after checkout
                    // personally, I like to use scriptler scripts and load the as simple as:
                    // list = load '/var/lib/jenkins/scriptler/scripts/load-list-script.groovy'
                    parallelStagesMap = list.collectEntries {
                        ["${it}" : generateStage(it)]
                    }
                }
            }
        }
 
        stage('Run Stages in Parallel') {
            steps {
                script {
                    parallel parallelStagesMap
                }
            }
        }
    }
}
