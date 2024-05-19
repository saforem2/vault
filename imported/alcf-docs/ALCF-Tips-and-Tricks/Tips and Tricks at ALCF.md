# Tips and Tricks at ALCF

# Interactive Jobs

A common part of my workflow involves running interactive jobs on ALCF compute nodes, allowing me to run commands, edit files, etc. Often, it is useful to have _multiple_ (or at least > 1) shells available to perform different actions (e.g. you may be editing a script in one shell and running a command in the other).

Unfortunately, when launching an interactive job, the necessary environment variables are only setup / defined in the session that the job launched into, meaning that if you `ssh` directly into the compute node you won't have the crucial environment variables `$COBALT_NODEFILE` / `$PBS_NODEFILE`.

![Save-Job-Env](Save-Job-Env.md)

> [!tldr]+ `savejobenv`
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