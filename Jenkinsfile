podTemplate {
    node(POD_LABEL) {
        stage('Run ansible') {
            ansiblePlaybook(credentialsId: 'jenkins', inventory: 'inventories/hosts', playbook: 'playbooks/test.yml')
        }
    }
}
