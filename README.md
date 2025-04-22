#!/bin/bash

# Excluir diretórios, arquivos, grupos e usuários criados anteriormente
rm -rf /diretorio1 /diretorio2 /publico
userdel -r usuario1
userdel -r usuario2
groupdel grupo1
groupdel grupo2

# Criar diretórios
mkdir /diretorio1 /diretorio2 /publico

# Definir o dono dos diretórios como root
chown root:root /diretorio1 /diretorio2 /publico

# Criar grupos
groupadd grupo1
groupadd grupo2

# Criar usuários e adicionar aos grupos
useradd -m -G grupo1 usuario1
useradd -m -G grupo2 usuario2

# Definir permissões
chmod 777 /publico
chmod 770 /diretorio1
chmod 770 /diretorio2

# Definir permissões de grupo nos diretórios
chown :grupo1 /diretorio1
chown :grupo2 /diretorio2

# Remover permissões de leitura, escrita e execução para outros usuários
chmod o-rwx /diretorio1
chmod o-rwx /diretorio2

# Subir arquivo de script para o GitHub
# Certifique-se de ter configurado o Git e ter acesso ao repositório
git init
git add script.sh
git commit -m "Adicionando script de provisionamento"
git remote add origin <URL_DO_SEU_REPOSITORIO>
git push -u origin master
