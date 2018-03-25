=================================================
 How to setup a bare minimum ubuntu 16.04 server
=================================================

#. Boot live disk
   
   - Set the language and keymap if necessary
   - Select 'Install Ubuntu Server'
    
#. Follow onscreen prompts
       
   - If you don't know that you want something else for disk partition use 'Guided - use entire disk and set up LVM' and maybe just use 50% to make the setup more flexible
   - I like security updates especially when they're automatic
   - Select OpenSSH server to be installed
  
#. Append your ssh public key to ~/.ssh/authorized_keys
   - If you have ssh-copy-id you can do this like so::

     > ssh-copy-id the-hostname-or-ip-address

#. Create docker group and add your user to it (run the following as root)
   ::
   
      # addgroup docker
      # usermod -a -G docker your-username

#. Run the ansible playbook host-setup-playbook.yaml
   - This requires you to have ansible on your machine which could be the server

#. Enter the tendenci container and run some commands
   The following come from the tendenci documentation https://tendenci.readthedocs.io/en/latest/installation/installation.html#scalable-installation
   
   ::
   
      > docker exec -it container_tendenci_1 bash
      # python manage.py migrate
      # python deploy.py
      # python manage.py load_creative_defaults
      # chmod -R -x+X media
      # python manage.py createsuperuser



