# l2hmc-qcd: HPO & Scaling Studies

---
# 2022-06-27

## Agenda Items

- [x] Login issues resolved?
- [x] Discuss `alcf-edge-dev_collab` / `edtb-02` access
    - Uses `PBS` instead of `cobalt`
- [ ] Setup / test qsub job scripts for running script jobs
- [ ] Test environment setup on `edtb-02` and share with Sirak
- [ ] Datascience meeting this week
    - [ ] Prepare slides
    - [ ] Reuse slides from last presentation ?
- [ ] Discuss testing / debugging bash scripts for
    - generic (elastic) training
    - WandB HPO runs
- [ ] Add to WandB slack channel
- [ ] Finish project request for LCRC allocation
- [ ] Write job script for running WandB sweeps







---
# 2022-06-23

- `~/.ssh/config`:

```bash
ControlMaster auto
ControlPath ~/.ssh/master%r@%h:%p
IPQoS=throughput
ServerAliveInterval 60
Compression yes
# ServerAliveCountMax=1
PreferredAuthentications publickey,password,keyboard-interactive

Host *.alcf.anl.gov
    AddKeysToAgent yes
    UseKeychain yes
    IdentityFile ~/.ssh/id_rsa

Host theta
    Hostname theta.alcf.anl.gov
    ControlMaster auto
    ControlPath ~/.ssh/master%r@%h:%p
    AddKeysToAgent yes
    # ForwardX11 yes
    IPQoS=throughput
    ServerAliveInterval 60
```

---
# 2022-06-15

- To see YOUR jobs in the queue:
    - `qstat -u $(whoami)`
- To delete a pending job:
    - `qdel JOB_ID`
- To see your storage quota (in your `$HOME` directory):
    - `myquota`
- To see your project storage:
    - `myprojectquotas`
- Useful for viewing free nodes:
    - `nodelist | grep idle`


---

# 2022-06-08
### Advice
- Try and write down _everything_ you're doing
    - Useful for preparing presentations / talking about what you've been working on


---
## Onboarding

## TODO
- [ ] Add to `l2hmc` meetings
- [x] Add to datascience meetings / channel / slack?

## Meeting
- [x] Login to Theta, ThetaGPU
    - [x] Add to projects / groups?
    - [x] Information on logging in, systems
    - [x] Information on environment / conda setup
        - [x] Create copy of base env
        - [x] Install packages
        - [x] Install `l2hmc`
        - [x] Try running
- Datascience channel / slack / meetings
- Broad overview of topic
- MCMC / HMC ??
- Overview of `l2hmc`
