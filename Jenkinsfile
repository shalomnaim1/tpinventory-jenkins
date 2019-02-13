@Library("github.com/RedHatInsights/insights-pipeline-lib") _
 
openShift.withUINode(namespace: "jenkins") {
 
   stage('Install integration tests env') {
       sh 'iqe plugin install topology_inventory'
       sh "iqe plugin install iqe-red-hat-internal-envs-plugin"
   }
 
   stage('Run integration tests') {
       withStatusContext.integrationTest {
           withEnv(['ENV_FOR_DYNACONF=ci']) {
              sh "iqe tests plugin topology_inventory -v -s --junitxml=junit.xml"   
           }
       }
       junit 'junit.xml'
   }
 
}
