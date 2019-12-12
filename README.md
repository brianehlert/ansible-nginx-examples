NGINX Controller Example
=========

The whats
------------

note: all playbooks tested with Ubuntu 18.04 minimum AMI image

Download the playbooks.
clone the latest github repository for the [nginx role](https://github.com/nginxinc/ansible-role-nginx) for the latest fixes.
some of the referenced playbooks can be found [here](https://github.com/brianehlert/ansible-nginx-controller-examples)

`ansible-playbook controller_environment_deploy_aws.yaml`

- Deploys the machines to the vpc
- uses controller_aws_vars.yaml
- writes individual inventory files in `playbook_dir`

`ansible_playbook nginx_lb_oss.yaml -i loadbalancers`

- uses nginx_lb_vars.yaml
- reads webservers inventory file
- results in: loadbalancer http response "an error occurred", becuase no webservers are responding

`ansible-playbook nginx_web_demo_oss.yaml -i webservers`

- uses included vars
- results in: "403 forbidden", index.html is not at the defined path

`ansible-playbook update_demo_index.html.yaml -i webservers`

- copies html file demo_index.html to remote
- reloads nginx

`ansible-playbook nginx_controller_postgresl_install.yaml -i dbserver`

- installs PostgreSQL, naas user, naas database

`ansible-playbook nginx_install_controller.yaml -i controller`

- installs Controller
- reads dbserver inventory file
- sets root password for su task (Ubuntu 18.04)
- requires nginx_install_controller_vars.yaml

`ansible-playbook nginx_remove.yaml -i loadbalancers`

- removes nginx oss from loadbanacer

`ansible-playbook nginx_lb_plus.yaml -i loadbalancers`

- installs nginx plus
- enables the plus api
- requires nginx_lb_plus_vars.yaml
- requires nginx plus license

`ansible-playbook nginx_controller_agent.yaml -i loadbalancers`

- reads controller inventory file
- requires controller_user_email, controller_password

----

`nginx_lb_plus_modsec.yaml`

- enables modsec on nginx plus
- requires nginx plus and modsec license
- uses nginx_lb_plus_modsec_vars.yaml

`nginx_lb_plus_modsec_OWASP_CRS.yaml`

- enables modsec on nginx plus
- downloads and sets up the OWASP_CRS
- uses nginx_lb_plus_modsec_vars.yaml