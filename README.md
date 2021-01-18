# How to run

0. Make sure your Docker environment is ok.
1. docker pull acyang/lfpy_ubuntu:latest
2. docker run --name jupyter -v /work:/work -d -p 6789:8888 lfpy_ubuntu:latest jupyter lab --ip='*' --no-browser --allow-root --NotebookApp.token=''
3. open http://YOUR_IP:6789/lab in browser. 
