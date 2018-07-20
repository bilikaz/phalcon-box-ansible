
# To setup box run:

    ansible-playbook -i hosts/dev.yml box/dev.yml

# To setup basic domain (ssl / path)

    ansible-playbook -i hosts/dev.yml domain/dev.yml -e domain=adminer.local

# Playbook list

    adminer - adminer.local setup
