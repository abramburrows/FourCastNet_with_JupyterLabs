## SDSU FourCastNet 

### Step 1: Create Your Own Image 

Access to the full 5T data set used to train FourCastNet is avaible using the shared JupyterLab. To create your own image, follow the instructions outlined at SDSU-Research-CI page: https://github.com/SDSU-Research-CI/shen-climate-lab/blob/main/jupyterhub/README.md

### Step 2: Copy FourCastNet 

In your JupyterHub file directory, create a new folder to store your files. Open the terminal and navigate to said directory. From there use the code snippet below to copy FourCastNet onto your Image. 
```
git clone https://github.com/NVlabs/FourCastNet.git
```

### Step 3: Updating ANFO.yaml file 

Update the paths in your ANFO.yaml to point to your data set used for training. In the case that you are using the shared directory at SDSU, navigate from the "shared" file in your directory to the training data.

## Step 4: Set Up Wandb 

FourCastNet uses Wandb to monitor the progress of your model in real time. Create an account at https://wandb.ai/site. Once you have created an account, you will need to start a project titled ERA5_precip 
```
code 
```

