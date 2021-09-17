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
                                f = file.getPath()
                                echo f
                                if (f.count("/") > 2) {
	                                list = f.split("/")
                                    if (list[0] == "SSIS_Projects") {
    	                                projects.add(list[1,2])
    	                            }
                                }
                                //projects.add(file.getPath().substring(0, file.getPath().lastIndexOf("/")>0 ? file.getPath().lastIndexOf("/") : 0 )) // add changed file to list
                                //projects.add(file.getPath().substring(file.getPath().indexOf("SSIS_Projects"), file.getPath().lastIndexOf("/")>0 ? file.getPath().lastIndexOf("/") : 0 )) 
                            }
                        }
                    }
                    projects.unique().each {
                        stage(it) {
                                echo it[0] 
                                echo it[1]
                        }
                    }
                    
                }
                
            }
        }
    }
}
