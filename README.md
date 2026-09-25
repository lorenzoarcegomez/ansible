# Instrucciones ansible
Todos los equipos de las aulas tienen configurado como servidor el equipo del profesor. <br>
Para conseguir que mi equipo funcione como servidor, lo primero, sería correr los scripts que hay en el github del departamento para instalar Ansible, etc.. Después, en cada aula hay que hacer lo siguiente desde el equipo del profesor usando el usuario ansible-admin hacia la IP de mi portatil (o del equipo que queramos que sea el nuevo servidor): 

```bash
su ansible-admin
```

```bash
scp ~/.ssh/ansible-admin_ed25519* ansible-admin@10.0.X.X:~/.ssh/
```
También nos vamos a copiar el inventario:

```bash
scp ~/ansible-aulas/inventarios/* ansible-admin@10.0.X.X:~/ansible-aulas/inventarios/
```

A continuación, le cambiamos el nombre a los archivos copiados:

```bash
mv ~/.ssh/ansible-admin/ansible-admin_ed25519 ~/.ssh/ansible-admin/ansible-admin_ed25519_IF0X
```

```bash
mv ~/.ssh/ansible-admin/ansible-admin_ed25519.pub ~/.ssh/ansible-admin/ansible-admin_ed25519_IF0X.pub
```

Ahora tenemos que incluir la clave dentro del archivo de inventario:

```bash
echo -e "\n[IF0X:vars]\nansible_ssh_private_key_file=~/.ssh/ansible-admin_ed25519_IF0X" >> ~/ansible-aulas/inventarios/IF0X.ini
```
