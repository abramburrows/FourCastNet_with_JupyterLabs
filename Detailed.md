## SDSU FourCastNet 

### Step 1: Get Access to Nautlis Portal

Send in a request to SDSU Research Software Engineer Team to get approval to work on this project. 
Once you have approval, 
1. Log in to the Nautilus Portal located here with your SDSUid: https://portal.nrp-nautilus.io/. (Detailed instructions with screen grabs are available at Tutorials for getting access are found in SDSU's Software Factory page: https://sdsu-research-ci.github.io/softwarefactory/gettingaccess.) 
  ![image](https://github.com/user-attachments/assets/77556125-fc56-4140-ab71-113c409f04bb)
  a. Sign in through Instution 
2. Once you have been able to succesfully login, notify SDSU IT team and request to be added to the **sdsu-shen-climate-lab namespace**
3. Install the "kubectl" tool for working with Nautilus: https://kubernetes.io/docs/tasks/tools/
  a. Select Instructions based on your computers operating system 
  ![image](https://github.com/user-attachments/assets/84c59ade-3ca5-4c98-9cb8-6fd56adf4e4f)
  b. Verify kubectl configurations



### Step 2: Create Your Own Image 

1. Copy jupyter-pod-L40.yaml and jupyter-volume.yaml from https://github.com/SDSU-Research-CI/shen-climate-lab/tree/main/jupyterhub. 
  a. Open jupyter-volume.yaml and set your volume name on Line 5. 
    ![image](https://github.com/user-attachments/assets/05f2b790-36d1-4191-bbf8-b0cc89d1ae5a)

  b. Open jupyter0-pod-L40.yaml and set your meta

2. Open terminal and navigate to '~./kube' in your file directory. 

![image](https://github.com/user-attachments/assets/350b1749-aa3e-4f72-8e85-de9a22f2c1d8)


3. Set context 

![image](https://github.com/user-attachments/assets/1c5329da-45ef-47a6-8fee-5368b28442e6)

4. Create Personal Volume/PVC

kubectl create -f jupyter-volume.yaml -n sdsu-shen-climate-lab


kubectl get pvc -n sdsu-shen-climate-lab


5. Create the Pod

kubectl create -f jupyter-pod-L40.yaml -n sdsu-shen-climate-lab


### Step 3: Copy FourCastNet 

In your JupyterHub file directory, create a new folder to store your files. Open the terminal and navigate to said directory. From there use the code snippet below to copy FourCastNet into your directory. 
```
git clone https://github.com/NVlabs/FourCastNet.git
```

## Step 4: Updating ANFO.yaml file 

Update the file ~/FourCastNet/config/ANFO.yaml to point to your training data. If you are using the 5T data set stored in the SDSU shared file, you can copy the ANFO.yaml file attached to this GitHub. If you are able to access more than 80GB of GPU memory you will be able to edit the ANFO file by increasing the batch size. This will allow shorter training time.

## Step 5: Set Up Wandb 

FourCastNet uses Wandb to monitor the progress of your model in real time. Create an account at https://wandb.ai/site. Once you have created an account, you will need to start a project titled ERA5_precip 

![image](https://github.com/abramburrows/FourCastNet-with-JuypterLabs/assets/147460119/cbbf648c-e1d4-47f5-9098-630b2965d939)

## Step 6 Set up Train.py 

Two lines in train.py determine which wandb project will be associated
- Line 537: ``` default = 'default' ``` to  ``` default = 'full_field' ```
- Line 588: ``` params['entity'] = "flowgan" ``` to ``` params['entity'] = "wandb_username" ```

## Step 7 Determine Extent of Training 

Determine the batch size and number of epochs you plan on using to train your model and adjust your ~/ANFO.yaml file accordingly. For reference, when training our model for the first time, it took two weeks to run 50 epochs with a batch size of 10. Further training is needed when working from the original backbone checkpoint and a single A100 with 80GB of memory to ensure that an accurate model is produced. A jupyter notebook to test the accuracy of the model is found in the repo. We also share the training checkpoints of our model which can be used as the base parameters to train a better model.
Training checkpoints will be adjusted in the ```train.py``` file for the variable ```pretrained_ckpt_path```.
