pipeline { 
    agent any 
    stages {
        stage('Build') { 
            steps { 
                echo "Build"
                
                script {
                    
                    projects = []
                    for (changeLogSet in currentBuild.changeSets) { 
                        for (entry in changeLogSet.getItems()) { // for each commit in the detected changes
                            for (file in entry.getAffectedFiles()) {
                                // projects.add(file.getPath().substring(0, file.getPath().lastIndexOf("/")>0 ? file.getPath().lastIndexOf("/") : 0 )) // add changed file to list
                                projects.add(file.getPath().substring(file.getPath().indexOf("SSIS_Projects")+13, file.getPath().lastIndexOf("/")>0 ? file.getPath().lastIndexOf("/") : 0 )) 
                            }
                        }
                    }
                    projects.findAll().unique().each {
                        stage(it) {
                                echo "Build $it"
                        }
                    }
                    
                }
                
            }
        }
    }
}
