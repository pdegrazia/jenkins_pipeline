pipeline {
    agent none
    parameters {
        string(defaultValue: '', description: 'The SUT base url', name: 'URL')
        string(defaultValue: '', description: 'The Grinder machine', name: 'CNAME')
        string(defaultValue: '', description: 'Full path to the performance script ', name: 'SCRIPT_PATH')
        string(defaultValue: '1', description: 'Number of concurrent processes', name: 'PROCESSES')
        string(defaultValue: '1', description: 'Number of concurrent threads', name: 'THREADS')
        string(defaultValue: '1', description: 'Set to 0 (zero) to run indefinitely', name: 'RUNS')
        string(defaultValue: '1', description: 'Maximum time for each process', name: 'MAX_EXEC_TIME')
        string(defaultValue: '1', description: 'To be defined', name: 'PROCESS_INCREMENT')
        string(defaultValue: '1', description: 'To be defined', name: 'PROCESS_INCREMENT_INTERVAL')
        string(defaultValue: '0', description: 'To be defined', name: 'MAX_DURATION')
	}
	stages {
		stage('start_vm') {
		    agent {
				node {
					label ''
				}
			}

            steps {
                build job: 'Start_VM', propagate: true
            }
		}

		stage('star perf test'){
		    agent {
				node {
					label ''
				}
			}

		    steps {
		        script {
					echo 'About to start performance testing'

				}
		        build job: 'Start_Perf_Testing', propagate: true, parameters: [
		            [$class: 'StringParameterValue', name: 'URL', value: "${params.URL}"],
                    [$class: 'StringParameterValue', name: 'CNAME', value: "${params.CNAME}"],
                    [$class: 'StringParameterValue', name: 'SCRIPT_PATH', value: "${params.SCRIPT_PATH}"],
                    [$class: 'StringParameterValue', name: 'PROCESSES', value: "${params.PROCESSES}"],
                    [$class: 'StringParameterValue', name: 'THREADS', value: "${params.THREADS}"],
                    [$class: 'StringParameterValue', name: 'RUNS', value: "${params.RUNS}"],
                    [$class: 'StringParameterValue', name: 'MAX_EXEC_TIME', value: "${params.MAX_EXEC_TIME}"],
                    [$class: 'StringParameterValue', name: 'PROCESS_INCREMENT', value: "${params.PROCESS_INCREMENT}"],
                    [$class: 'StringParameterValue', name: 'PROCESS_INCREMENT_INTERVAL', value: "${params.PROCESS_INCREMENT_INTERVAL}"],
                    [$class: 'StringParameterValue', name: 'MAX_DURATION', value: "${params.MAX_DURATION}"]
		        ]
		    }
		}

        stage('Produce logs'){
            agent {
				node {
					label ''
				}
			}

		    steps {
		        build job: 'Post_Process_Logs', propagate: true
		    }
		}


		stage('stop_vm') {
		    agent {
				node {
					label ''
				}
			}

		    steps {
		        build job: 'Stop_VM'
            }

		}
	}
}
