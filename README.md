sample ansible inventory layout with multiple apps & environments,
showcasing the use of nested & intersected groups

follows [Ansible > User Guide > Sample Ansible setup > Sample directory layout](https://docs.ansible.com/ansible/latest/user_guide/sample_setup.html#sample-directory-layout)

~~~sh
$ ansible-inventory -i . --list --yaml
~~~

~~~yaml
all:
  children:
    appA:
      children:
        appA_prod:
          hosts:
            hostA01:
              appA_listen_port: 5001
              appA_portal_url_correct: https://a.example.com/
              appA_portal_url_wrong: 'https://a.example.com/ (error: also in test)'
              company_domain: example.com
              fqdn: hostA01.example.com
              reposerver: repos.example.com
        appA_test:
          hosts:
            hostA02:
              appA_listen_port: 5001
              appA_portal_url_wrong: 'https://a.example.com/ (error: also in test)'
              company_domain: example.com
              fqdn: hostA02.example.com
              reposerver: test.repos.example.com
    appB:
      children:
        appB_prod:
          hosts:
            hostB01:
              company_domain: example.com
              reposerver: repos.example.com
        appB_test:
          hosts:
            hostB02:
              company_domain: example.com
              reposerver: test.repos.example.com
    appC:
      children:
        appC_prod:
          hosts:
            hostC01:
              company_domain: example.com
              environment: prod
              reposerver: repos.example.com
        appC_test:
          hosts:
            hostC02:
              company_domain: example.com
              environment: test
              reposerver: test.repos.example.com
              verify_certificates: false
            hostC03:
              company_domain: example.com
              environment: test
              reposerver: test.repos.example.com
              verify_certificates: false
    appD:
      hosts:
        hostD01:
          company_domain: example.com
          environment:
          - appD_prod
          - prod
          reposerver: repos.example.com
        hostD02:
          company_domain: example.com
          environment:
          - appD_test
          - test
          reposerver: test.repos.example.com
    appD_prod:
      hosts:
        hostD01: {}
    appD_test:
      hosts:
        hostD02: {}
    prod:
      children:
        appA_prod:
          hosts:
            hostA01: {}
        appB_prod:
          hosts:
            hostB01: {}
      hosts:
        hostC01: {}
        hostD01: {}
    test:
      children:
        appA_test:
          hosts:
            hostA02: {}
        appB_test:
          hosts:
            hostB02: {}
      hosts:
        hostC02: {}
        hostC03: {}
        hostD02: {}
    ungrouped: {}
~~~
