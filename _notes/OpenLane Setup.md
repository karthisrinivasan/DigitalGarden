sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt-get update
  403  sudo apt-get install     apt-transport-https     ca-certificates     curl     gnupg     lsb-release
  404  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
  405  echo   "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  406  sudo apt-get update
  407  sudo apt-get install docker-ce docker-ce-cli containerd.io
  408  apt-cache madison docker-ce
  409  sudo apt-get install docker-ce=5:20.10.7~3-0~ubuntu-focal docker-ce-cli=5:20.10.7~3-0~ubuntu-focal containerd.io
  410  sudo docker run heelo-world
  411  sudo docker run hello-world
  412  ls
  413  cd OpenLane/
  414  ls
  415  make openlane
  416  sudo make openlane
  417  make test
  418  sudo make test
  419  cd pdks/

  438  sudo chmod 777 pdks
  440  sudo make test
  441  make mount

