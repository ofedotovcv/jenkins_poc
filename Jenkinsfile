pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps { 
                echo "Build"
                
                script {
                    
                    changedFiles = []
                    for (changeLogSet in currentBuild.changeSets) { 
                        for (entry in changeLogSet.getItems()) { // for each commit in the detected changes
                            for (file in entry.getAffectedFiles()) {
                                changedFiles.add(file.getPath().substring(0, file.getPath().lastIndexOf("/"))) // add changed file to list
                            }
                        }
                    }
                    println changedFiles.dump()
                    
                }
                
            }
        }
        stage('Test'){
            steps {
                echo "Test"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploy"
            }
        }
    }
}
