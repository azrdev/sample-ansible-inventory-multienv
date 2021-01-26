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
      hosts:
        hostA01:
          appA_listen_port: 5001
          appA_portal_url: 'https://a.example.com/ (error: also in test)'
          company_domain: example.com
          fqdn: hostA01.example.com
          reposerver: repos.example.com
        hostA02:
          appA_listen_port: 5001
          appA_portal_url: 'https://a.example.com/ (error: also in test)'
          company_domain: example.com
          fqdn: hostA02.example.com
          reposerver: test.repos.example.com
    appB:
      hosts:
        hostB01:
          company_domain: example.com
          reposerver: repos.example.com
        hostB02:
          company_domain: example.com
          reposerver: test.repos.example.com
    appC:
      hosts:
        hostC01:
          company_domain: example.com
          environment: prod
          reposerver: repos.example.com
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
    appC_test:
      hosts:
        hostC02: {}
        hostC03: {}
    prod:
      hosts:
        hostA01: {}
        hostB01: {}
        hostC01: {}
    test:
      hosts:
        hostA02: {}
        hostB02: {}
        hostC02: {}
        hostC03: {}
    ungrouped: {}
~~~
