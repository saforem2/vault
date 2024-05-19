# Save Job Env

1. Submit interactive job
	2. Polaris:
		3. `qsub -A datascience -q preemptable -l select=4 -l walltime=24:00:00,filesystems=eagle:home:grand -I`
	3. ThetaGPU:
		4. `qsub-gpu -A datascience -n 2 -q full-node --attrs="filesystems=home,grand,eagle,theta-fs0:ssds=required" -t 12:00 -I`

2. The job scheduler will start up the job and launch you onto a compute node

3. From _this compute node_ (i.e. _inside this shell with the environment variables_)[^names], run:
  ```Shell
  (foremans@thetagpu21) $ savejobenv
----------------------------------------------------------------------
[DIST INFO]:  Writing Job info to /home/foremans/.jobenv-thetaGPU 
NHOSTS: 2  NGPU_PER_HOST: 8  NGPUS: 16 
Copying COBALT_NODEFILE to clipboard...
COBALT_NODEFILE: /var/tmp/cobalt.10138529
thetagpu10
thetagpu21
----------------------------------------------------------------------
Run 'source getjobenv' in a new shell to automatically set env vars
  ```

[^names]: Should be either `thetagpu*` or `x3*.polaris.alcf.anl.gov`

## `savejobenv`

> [!TLDR]+ `savejobenv`
> ```bash
> #!/bin/bash --login
> 
> HOSTNAME=$(hostname)
> 
> getCOBALT_NODEFILE() {
>   RUNNING_JOB_FILE="/var/tmp/cobalt-running-job"
>   if [[ -f "$RUNNING_JOB_FILE" ]]; then
>     JOBID=$(sed "s/:$USER//" /var/tmp/cobalt-running-job)
>     COBALT_NODEFILE="/var/tmp/cobalt.${JOBID}"
>     export JOBID="${JOBID}"
>     export HOSTFILE="${HOSTFILE}"
>     export COBALT_NODEFILE="${COBALT_NODEFILE}"
>   fi
> }
> 
> setup() {
>   if [[ "${HOSTNAME}" == x3* ]]; then
>     export FNAME="PBS_NODEFILE"
>     export HOSTFILE="${PBS_NODEFILE}"
>     export JOBENV_FILE="${HOME}/.jobenv-polaris"
>     echo "${PBS_NODEFILE}" | rpbcopy
>   elif [[ "${HOSTNAME}" == thetagpu* ]]; then
>     getCOBALT_NODEFILE
>     export FNAME="COBALT_NODEFILE"
>     export HOSTFILE="${COBALT_NODEFILE}"
>     export JOBENV_FILE="${HOME}/.jobenv-thetaGPU"
>     echo "${COBALT_NODEFILE}" | rpbcopy
>   fi
>   NHOSTS=$(wc -l < "${HOSTFILE}")
>   NGPU_PER_HOST=$(nvidia-smi -L | wc -l)
>   NGPUS="$((${NHOSTS}*${NGPU_PER_HOST}))"  # noqa
>   echo "----------------------------------------------------------------------"
>   echo \
>     "[DIST INFO]: " \
>     "Writing Job info to ${JOBENV_FILE} "
>   echo \
>     "NHOSTS: $NHOSTS " \
>     "NGPU_PER_HOST: $NGPU_PER_HOST " \
>     "NGPUS: $NGPUS "
>   export NHOSTS="${NHOSTS}"
>   export NGPU_PER_HOST="${NGPU_PER_HOST}"
>   export NGPUS="${NGPUS}"
>   {
>     echo "export HOSTFILE=${HOSTFILE}"
>     echo "export ${FNAME}=${HOSTFILE}"
>     echo "export NHOSTS=${NHOSTS}"
>     echo "export NGPU_PER_HOST=${NGPU_PER_HOST}"
>     echo "export NGPUS=${NGPUS}"
>   } > "${JOBENV_FILE}"
> }
> 
> PrintAndCopy() {
>   echo "Copying ${FNAME} to clipboard..."
>   echo "${FNAME}: ${HOSTFILE}"
>   cat "${HOSTFILE}"
>   echo "${HOSTFILE}" | rpbcopy
>   echo "export ${FNAME}=${HOSTFILE}" | rpbcopy
>   echo "----------------------------------------------------------------------"
>   echo "Run 'source getjobenv' in a new shell to automatically set env vars"
> }
> 
> setup
> PrintAndCopy
> # vim: ft=bash
> ```