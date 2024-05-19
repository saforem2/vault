# `EleutherAI/gpt-neox`

01. `module load conda`
02. `conda activate base`
03. `source /soft/datascience/venvs/polaris/2022-09-08/bin/activate`
04. `git clone https://github.com/EleutherAI/gpt-neox`
05. `cd gpt-neox`
06. `cat $PBS_NODEFILE > hostfile`
07. `sed -e 's/$/ slots=4/' -i hostfile`
08. `export DLTS_HOSTFILE=hostfile`
09. `echo "PATH=$PATH > .deepspeed_env`
10. `echo "LD_LIBRARY_PATH=$LD_LIBRARY_PATH" >> .deepspeed_env`
11. `echo "http_proxy=${http_proxy} >> .deepspeed_env`
12. `echo "https_proxy=${https_proxy} >> .deepspeed_env`
13. `python3 ./deepy.py train.py --hostfile hostfile configs/small.yml configs/local_setup.yml > train.log 2>&1 &`
