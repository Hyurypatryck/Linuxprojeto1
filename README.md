sudo apt update
sudo apt install ansible -y

[webserver]
192.168.1.100 ansible_user=seu_usuario ansible_ssh_private_key_file=~/.ssh/id_rsa

- hosts: webserver
  become: yes
  tasks:
    - name: Instalar Apache
      apt:
        name: apache2
        state: present

    - name: Iniciar o serviço Apache
      service:
        name: apache2
        state: started
        enabled: yes

    - name: Copiar arquivo de configuração do site
      copy:
        src: /caminho/para/seu/index.html
        dest: /var/www/html/index.html

ansible-playbook -i hosts webserver.yml
