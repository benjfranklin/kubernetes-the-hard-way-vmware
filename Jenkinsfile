podTemplate(containers: [
    containerTemplate(
        name: 'ansible', 
        image: 'benjfranklin/jenkins-agent-ansible:1.2',
        command: 'sleep', 
        args: '5m'
        )
  ]) {

    node(POD_LABEL) {
        stage('Testing Ansible Agent') {
            container('ansible') {
                stage('Run ansible') {
                    ansiblePlaybook(credentialsId: 'jenkins', inventory: 'ansible/inventories/hosts', playbook: 'ansible/playbooks/test.yml')
                }
            }
        }

    }
}
