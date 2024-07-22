## SDSU FourCastNet 

### Step 0: Get Access to Nautlis Portal

Send in a request to SDSU Research Software Engineer Team to get approval to work on this project. Tutorials for getting access are found in SDSU's Software Factory page: https://sdsu-research-ci.github.io/softwarefactory/gettingaccess.

### Step 1: Create Your Own Image 

Access to the full 5T data set used to train FourCastNet is available under the sdsu-shen-climate-lab namespace. To create your own Pod, follow the instructions outlined at SDSU-Research-CI page: https://github.com/SDSU-Research-CI/shen-climate-lab/blob/main/jupyterhub/README.md.

### Step 2: Copy FourCastNet 

In your JupyterHub file directory, create a new folder to store your files. Open the terminal and navigate to said directory. From there use the code snippet below to copy FourCastNet into your directory. 
```
git clone https://github.com/NVlabs/FourCastNet.git
```

### Step 3: Updating ANFO.yaml file 

Update the file ~/FourCastNet/config/ANFO.yaml to point to your training data. If you are using the 5T data set stored in the SDSU shared file, you can copy the ANFO.yaml file attached to this GitHub. If you are able to access more than 80GB of GPU memory you will be able to edit the ANFO file by increasing the batch size. This will allow shorter training time.

## Step 4: Set Up Wandb 

FourCastNet uses Wandb to monitor the progress of your model in real time. Create an account at https://wandb.ai/site. Once you have created an account, you will need to start a project titled ERA5_precip 

![image](https://github.com/abramburrows/FourCastNet-with-JuypterLabs/assets/147460119/cbbf648c-e1d4-47f5-9098-630b2965d939)

## Step 5 Set up Train.py 

Two lines in train.py determine which wandb project will be associated
- Line 537: ``` default = 'default' ``` to  ``` default = 'full_field' ```
- Line 588: ``` params['entity'] = "flowgan" ``` to ``` params['entity'] = "wandb_username" ```

## Step 6 Determine Extent of Training 

Determine the batch size and number of epochs you plan on using to train your model and adjust your ~/ANFO.yaml file accordingly. For reference, when training our model for the first time, it took two weeks to run 50 epochs with a batch size of 10. Further training is needed when working from the original backbone checkpoint and a single A100 with 80GB of memory to ensure that an accurate model is produced. A jupyter notebook to test the accuracy of the model is found in the repo. We also share the training checkpoints of our model which can be used as the base parameters to train a better model.
Training checkpoints will be adjusted in the ```train.py``` file for the variable ```pretrained_ckpt_path```.
