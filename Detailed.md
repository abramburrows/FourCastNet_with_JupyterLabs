## SDSU FourCastNet 

### Step 1: Get Access to Nautlis Portal

Send in a request to SDSU Research Software Engineer Team to get approval to work on this project. 
Once you have approval, 
1. Log in to the Nautilus Portal located here with your SDSUid: https://portal.nrp-nautilus.io/. (Detailed instructions with screen grabs are available at Tutorials for getting access are found in SDSU's Software Factory page: https://sdsu-research-ci.github.io/softwarefactory/gettingaccess.) 
  ![image](https://github.com/user-attachments/assets/77556125-fc56-4140-ab71-113c409f04bb)

2. Notify SDSU IT team and request to be added to the **sdsu-shen-climate-lab namespace**
3. Install the "kubectl" tool for working with Nautilus: https://kubernetes.io/docs/tasks/tools/

a. Select Instructions based on your computers operating system 
  ![image](https://github.com/user-attachments/assets/84c59ade-3ca5-4c98-9cb8-6fd56adf4e4f)
  
b. Verify kubectl configurations



### Step 2: Create Your Own Image 

1. Copy jupyter-pod-L40.yaml and jupyter-volume.yaml from https://github.com/SDSU-Research-CI/shen-climate-lab/tree/main/jupyterhub. 
  a. Open jupyter-volume.yaml and set your volume name on Line 5.
<p align="center">
  <img src="https://github.com/user-attachments/assets/05f2b790-36d1-4191-bbf8-b0cc89d1ae5a" />
</p>

  b. Set name of pod on line 4 on jupyter-pod-L40.yaml 
   
  <p align="center">
    <img src="https://github.com/user-attachments/assets/14fd32e9-bd25-4171-af9c-5ff00cb50a57" />
  </p>

  c. Set name of volume on lin 52 jupyter-pod-L40.yaml 


   <p align="center">
    <img src="https://github.com/user-attachments/assets/58914047-bdc1-47b3-b17c-575f2a90e55f" />
   </p>
  
2. Open terminal and navigate to ```~./kube``` in your file directory. 

![image](https://github.com/user-attachments/assets/350b1749-aa3e-4f72-8e85-de9a22f2c1d8)


3. Set context 

![image](https://github.com/user-attachments/assets/1c5329da-45ef-47a6-8fee-5368b28442e6)

4. Create Personal Volume/PVC

kubectl create -f jupyter-volume.yaml -n sdsu-shen-climate-lab


![image](https://github.com/user-attachments/assets/ffa6d677-ada0-4818-9900-d23641a15e48)



5. Create the Pod

![image](https://github.com/user-attachments/assets/f14d0fd6-a4d8-4044-962f-61c640534036)

6. Access your Pod

   a. Ensure your pod is running. 

![image](https://github.com/user-attachments/assets/8f97b637-4743-4446-b6f9-03b3db9f2988)

  b. Get logs from your pod. Make sure to enter in the name of your pod when getting logs. 

  ![image](https://github.com/user-attachments/assets/85a00772-eb99-4f42-bca3-4e53bee15587)

  c. In a second terminal window, run the following command to set up port forwarding between your computer and the container running Jupyter.

  ![image](https://github.com/user-attachments/assets/72ce2737-d5aa-4e8f-9c93-bd000f9c1c50)

d. From the output on your first terminal, copy the URL to the clipboard that starts with http://127.0.0.1./ 

_Note_: If you get an error message indicating port 8888 is already taken, simply change the port number on the left side of the colon in the above command i.e. 8889:8888. Then when you paste the URL from the output, make sure to update the port from 8888 to 8889, or whatever number you chose. This issue can arise if you have a local instance of Jupyter Lab already running on port 8888.

You should now be able to access the URL you copied to the clipboard in your web browser.

![image](https://github.com/user-attachments/assets/c47ec0d9-344b-447b-a6f5-7af6f914aabb)



### Step 3: Copy FourCastNet 

In your JupyterHub file directory, create a new folder to store your files by clicking on the gray folder icon. 

https://github.com/user-attachments/assets/6415e321-9066-4817-b839-e77c1fd7ac7

Open the terminal. Type in '''bash''' and press enter. From there, navigted to your new folder in the directory and copy the following code in the terminal. 
```
git clone https://github.com/NVlabs/FourCastNet.git

```

![image](https://github.com/user-attachments/assets/5f79d755-cf28-4602-ab66-0cc4d177c136)


## Step 4: Updating ANFO.yaml file 

Open the file at ~/FourCastNet/config/ANFO.yaml. If you are using the 5T data set stored in the SDSU shared file, you can copy the ANFO.yaml file attached to this GitHub. If you are able to access more than 80GB of GPU memory you will be able to edit the ANFO file by increasing the batch size. This will allow shorter training time.

![image](https://github.com/user-attachments/assets/a482a50d-e60b-45dd-a108-8b709bf1525e)


## Step 5: Set Up Wandb 

FourCastNet uses Wandb to monitor the progress of your model in real time. Create an account at https://wandb.ai/site. Once you have created an account, you will need to start a project titled ERA5_precip 

![image](https://github.com/abramburrows/FourCastNet-with-JuypterLabs/assets/147460119/cbbf648c-e1d4-47f5-9098-630b2965d939)

## Step 6 Set up Train.py 

Two lines in train.py determine which wandb project will be associated
- Line 537: ``` default = 'default' ``` to  ``` default = 'full_field' ```

![image](https://github.com/user-attachments/assets/c9004366-a2fa-485b-8fac-24ece91cc6fa)

- Line 588: ``` params['entity'] = "flowgan" ``` to ``` params['entity'] = "wandb_username" ```

![image](https://github.com/user-attachments/assets/a7d0104b-adfd-4995-ab20-21edadc9caaa)


## Step 7 Determine Extent of Training 

Determine the batch size and number of epochs you plan on using to train your model and adjust your ~/ANFO.yaml file accordingly. For reference, when training our model for the first time, it took two weeks to run 50 epochs with a batch size of 10. Further training is needed when working from the original backbone checkpoint and a single A100 with 80GB of memory to ensure that an accurate model is produced. A jupyter notebook to test the accuracy of the model is found in the repo. We also share the training checkpoints of our model which can be used as the base parameters to train a better model.
Training checkpoints will be adjusted in the ```train.py``` file for the variable ```pretrained_ckpt_path```.

## Step 8 Running train.py 


Navigate to ~/FourCastNet in an active terminal. From there, you can run train.py by entering in ``` python3 train.py```. 
