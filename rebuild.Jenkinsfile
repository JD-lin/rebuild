
pipeline {
    agent any
    parameters {
			booleanParam(name: 'PDB', defaultValue: 'false', description: 'true will be trigger pdb mode false will not')
	    		string(name: 'ENV', defaultValue: '', description: 'please input device name , like:dut21 or dut22')
			string(name: 'REBUILD_NUMBER',defaultValue: '', description:'please input the rebuild number')
	    		string(name: 'NODE', defaultValue: '10.17.0.2', description: 'jenkins node name you will execute script')
			string(name: 'MARKER', defaultValue: '', description: 'please input mark type to select execute cases, empty mean execute all cases in test script')
			string(name: 'TEST_TYPE', defaultValue: 'clx_diag_tests', description: 'please input test_type, like: protocol_tests or sdk_tests or kis_tests')
			string(name: 'TESTCASE', defaultValue: '', description: 'input script relative path, like: l2_switching/lldp/test_01.py')
			string(name: 'CLINGENV_URL', defaultValue: 'https://jenkins.clounix.com/job/sdk/job/regression/job/1.x.x/job/clingenv-package/lastSuccessfulBuild/artifact/clingenv.sh', description: 'input CLINGENV_URL for test')
			string(name: 'PYTEST_OPTS', defaultValue: '', description: 'config pytest opts, like: -s')
			string(name: 'WORKDIR', defaultValue: '', description: 'input cases dir, empty will use default path (/home/jenkins/clounix-mgmt-dbg/${BUILD_USER_ID}/clounix-mgmt)')
    }
    
    stages {
        stage('start') {
            steps {
                script{
		    def signature = 'new groovy.json.JsonSlurperClassic'
		    org.jenkinsci.plugins.scriptsecurity.scripts.ScriptApproval.get().approveSignature(signature)	
		    print("Github")
                    dynamicvar = ['MARKER','TESTCASE','PYTEST_OPTS','WORKDIR']
                    if (params.REBUILD_NUMBER){
                        //def jobName = currentBuild.rawBuild.project.getName()
                        //def job = Jenkins.instance.getItem(jobName)
                        //for(int i = 0;i<dynamicvar.size;i++) {
                            //def preBuild = job.getBuild(params.REBUILD_NUMBER)
                            //def envmap = preBuild.getEnvVars()
                            //env[dynamicvar[i]] = envmap [dynamicvar[i]]
                            //while (envmap[dynamicvar[i]]=='' && envmap['REBUILD_NUMBER'] != ''){
                            //    preBuild = job.getBuild(envmap['REBUILD_NUMBER'])
                            //    envmap = preBuild.getEnvironment()
                            //    env[dynamicvar[i]] = envmap [dynamicvar[i]]
                            //}
                        }
                    }
                    for(int i = 0;i<dynamicvar.size;i++) {
                        if (params[dynamicvar[i]]!=''){
                            env[dynamicvar[i]] = params[dynamicvar[i]]
                        }
                    }
                    println "NODE = ${env.NODE}"
                    println "ENV = ${env.ENV}"
                    println "MARKER = ${env.MARKER}"
                    println "TEST_TYPE = ${env.TEST_TYPE}"
                    println "TESTCASE = ${env.TESTCASE}"
                    println "CLINGENV_URL = ${env.CLINGENV_URL}"
                    println "PDB = ${env.PDB}"
                    println "PYTEST_OPTS = ${env.PYTEST_OPTS}"
                    println "WORKDIR = ${env.WORKDIR}"
                }
            }
        }
    }
    post {
        always {
          slackSend channel: 'test', color: "#ff0000", message: "Message from Jenkins Pipeline"
        }
    }    
}
