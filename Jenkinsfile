podTemplate {
    node(POD_LABEL) {
        stage('Run ansible') {
            ansiblePlaybook(credentialsId: 'jenkins', inventory: 'ansible/inventories/hosts', playbook: 'ansible/playbooks/test.yml')
        }
    }
}
