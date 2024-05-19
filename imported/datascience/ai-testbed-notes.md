# ALCF AI Testbed Notes

Documentation from: [argonne-lcf/ai-testbed-userdocs](https://github.com/argonne-lcf/ai-testbed-userdocs)

- Might be useful to have a home / landing page with Table of Contents for each of the systems
    
    ---
    
# [Cerebras](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/cerebras/)
1. [System Overview](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/cerebras/System-Overview.md)
    - Should make it clear that python support is restricted only to keras models which are compatible with `tf.keras.estimator.model_to_estimator`
        - According to [Create an Estimator from a Keras model](https://www.tensorflow.org/tutorials/estimator/keras_model_to_estimator):  
            - **Estimators are not recommended for new code**
        - Plans to support generic `tf.keras.Model`s?
    - Estimates of timelines for Releases 1.1 or 1.2?
        
2. [Connect to a CS-2 node](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/cerebras/Connecto-to-a-CS-2-node.md)
    - Use markdown formatting for ordered lists in ssh instructions instead of (1), (2), etc.
    - Final section (**Setup the environment**) is duplicated information from [How-to-setup-your-base-environment](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/cerebras/How-to-setup-your-base-environment.md) 
    - Would be nice to include snippet of environment script as in [Sambanova / How to Setup your Base Environment](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/How-to-setup-your-base-environment.md)

3. [Steps to run a model or program](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/cerebras/Steps-to-run-a-model-or-program.md)
    - The `csrun_cpu` and `csrun_wse` section assumes you've read and understood the [Job Queuing and Submission](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/cerebras/Job-Queuing-and-Submission.md) page
    
    > You should see a very fast training rate, e.g. 1400 steps per second, and output that finishes with something similar to this:
    
    - Very fast is ambiguous, fast relative to what?
    - From [The Cerebras ML Workflow — Software Documentation (Version 1.2.0)](https://docs.cerebras.net/en/latest/cerebras-basics/cs-ml-workflow.html)
        - PyTorch and TensorFlow links are both broken:
            - We recommend you read the Cerebras basics and run quickstart first. When you are ready, [start your PyTorch to CS journey here.](https://docs.cerebras.net/en/latest/pytorch-docs/index.html)
            - We recommend you read the Cerebras basics and run quickstart first. When you are ready, [start your TensorFlow to CS journey here.](https://docs.cerebras.net/en/latest/tensorflow-docs/index.html)

4. [Example Programs](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/cerebras/Example-Programs.md)
    - Seems redundant to explicitly list similar instructions for Unet, Bert and BraggNN
    
5. [Job Queuing and Submission](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/cerebras/Job-Queuing-and-Submission.md)
    - Not clear why this is after the Example Programs page
    
6. [Customizing Environments](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/cerebras/Using-virtual-environments-to-customize-environment.md)

7. [Performance Tools](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/cerebras/Performance-Tools.md) 

    > The product of "Active PEs" and "Compute Utilization" is the effective wafer utilization as estimated by the compiler when the application is not I/O bound.
    
    - Why? What does "Active PEs" and "Compute Utilization" measure?
    - Combine `find` and `head` commands into `head -n 7 $(find . -name "compile_report.txt")` 
    
    ```bash
    [foremans@testbed-cs2-02-med8]~/R1.1.0/modelzoo/fc_mnist/tf% head -n 7 $(find . -name "compile_report.txt")
    Estimated Overall Performance
    -------------------------------
    Samples/s:                    1270553.1
    Compute Samples/s:            1270553.1
    Transmission Samples/s:       2607362.0
    Active PEs:                   0%
    Compute Utilization:          74%
    ```
    - What does 0% Active PEs mean?
    
    
8. [Tunneling and forwarding ports](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/cerebras/Tunneling-and-forwarding-ports.md)

9. [System and Storage Policies](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/cerebras/System-and-Storage-Policies.md)

10. [Miscellaneous](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/cerebras/Miscellaneous.md)
    1. Information on Porting applications to the CS-2 should maybe be prioritized?
    - Users interested in running custom models?

---

## [SambaNova](https://github.com/argonne-lcf/ai-testbed-userdocs/tree/main/docs/sambanova)
1. [System Overview](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/System-Overview.md)
    - "half-rack system" ?
    - Configuration section says 
        > SambaNova node can be accessed as sm-01.ai.alcf.anl.gov.
        
       but page on [How to setup your base environment](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/How-to-setup-your-base-environment.md)says
        ```bash
        ssh ALCFUserID@sambanova.alcf.anl.gov
        ```
    
2. [How to setup your base environment](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/System-Overview.md)
    1. Page title reads like an instruction, whereas most of the others read like section titles
    2. Could combine this page with [Using virtual environments to customize environment](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/Using-virtual-environments-to-customize-environment.md) into a single **Environment Setup** page??

3. [Using virtual environments to customize environment](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/Using-virtual-environments-to-customize-environment.md)
    1. Might be worth mentioning what packages are included in `--system-site-packages`
    2. What commonly used packages are missing / might need to be installed manually?


4. [Steps to run a model / program](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/Steps-to-run-a-model-or-program.md)
    - Might be worth mentioning that the [Example Programs](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/Example-Programs.md) page has instructions for making a local copy of the examples used in the documentation
    - "The SambaNova workflow includes the following main steps to run a model"
        - Maybe list steps explicitly and then expand on them in their respective sections? e .g.
        - The SambaNova workflow includes the following main steps to run a model:
            1. Compile
            2. Run
            3. Test (optional)
        - Seems a bit unnecessary to list them as steps if the Test step is optional?
    - Where is the `pef` directory coming from in the `srun python lenet.py run --pef="pef/lenet/lenet.pef `command?

5. [Job Queuing and Submission](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/Job-Queuing-and-Submission.md)

6. [Example Programs](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/Example-Programs.md)

7. [Performance Tools](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/Performance-Tools.md)

8. [Best Practices and FAQs](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/Best-Practices-and-FAQs.md)

9. [Tunneling and Forwarding Ports](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/Tunneling-and-forwarding-ports.md)

10. [System and Storage Policies](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/System-and-Storage-Policies.md)

11. [Miscellaneous](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/Miscellaneous.md)
    1. Might be a good idea to include the links under Resources somewhere on the main page?

12. [Anatomy of SambaNova PyTorch Models](https://github.com/argonne-lcf/ai-testbed-userdocs/blob/main/docs/sambanova/Anatomy-of-SambaNova-PyTorch-Models.md)
    1. Updates section references https://git.cels.anl.gov/ai-testbed-apps/sambanova/sambanova_starter.git but that link requires special permission to view
     



---
