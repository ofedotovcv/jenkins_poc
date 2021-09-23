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
                                c = f.count("/")
                                if ( c >= 2) {
	                                list = f.split("/")
                                    if (list[0] == "SSIS_Projects") {
                                        if ( c == 2 ) {
                                            projects.add(list[1])
                                        } else {
                                            projects.add(list[1,2])
                                        }
    	                            }
                                }
                                //projects.add(file.getPath().substring(0, file.getPath().lastIndexOf("/")>0 ? file.getPath().lastIndexOf("/") : 0 )) // add changed file to list
                                //projects.add(file.getPath().substring(file.getPath().indexOf("SSIS_Projects"), file.getPath().lastIndexOf("/")>0 ? file.getPath().lastIndexOf("/") : 0 )) 
                            }
                        }
                    }
                    projects.unique().each {
                        stage(it[0]+" "+it[1]) {
                                echo it[0] 
                                echo it[1]
                                build job: 'job_build', parameters: [[$class: 'StringParameterValue', name: 'name1', value: it[0]], [$class: 'StringParameterValue', name: 'name2', value: it[1]]]
                        }
                    }
                    
                }
                
            }
        }
    }
}
