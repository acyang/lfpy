# How to run

0. Make sure your Docker environment is ok.
`systemctl status docker`
1. Create a permanent storage area on host machine.
`mkdir /work` 
2. docker pull acyang/lfpy_ubuntu:latest
3. docker run --name lfpy -d --privileged -v /work:/work -p 6789:8888 lfpy:latest jupyter lab --ip='*' --no-browser --allow-root
4. open http://YOUR_IP:6789/lab in browser. 
