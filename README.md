**0. Setting up server** 
- Select number of GPU's, CPU's and data you would like allocated to run FourCastNet. The original data set used to train FourCastNet is 5T large and you will likely need special permission from your institution before allocating that much data.
- Select the "TBD" environment to create a server with all of the necessary packages.
  
**1. Create a foulder to work in**
- Press the gray folder icon at the top left corner of the screen to create a folder

**2. Clone FourCastNet into**
- Press the blue '+' icon. In the new window that opens, select terminal to create a terminal.
- Navigate your terminal to where ever you plan on storing the FourCastNet files and then run `!git clone https://github.com/NVlabs/FourCastNet.git`

**4. Import climate data using copernicus**

- Create an account https://cds.climate.copernicus.eu/#!/home
  
- Once you have created an account, you will need to get access your 'url' and 'key' that should be formatted as
  
> url: https://cds.climate.copernicus.eu/api/v2
> 
> key: 291759:39eme899-cbb6-4b6c-8fd0-f58b568dc3b7
- Use the commands `export CDS_API_URL="https://cds.climate.copernicus.eu/api/v2` and `export CDS_API_KEY="291759:576acfa7-cbb6-4b6c-8fd0-f58b568dc3b7` to set your personal 'url' and key'
- In the copernicus file from FourCastNet, there will be three python files. Adjust the number of variables, the date, and times you would like to use to train your data set. You also need to adjust the file path at the bottom of each python file to ensure the information get downloaded to the correct place.
- Once all of your information is downloaded, you must format the data using the files in data process folder. (more notes coming for this because I ran into a lot of trouble getting the files formatted correctly)

**5. Importing climate data using globus** 
- Create a globus account at https://www.globus.org/
- Once you have an account, login and search the file manager for "FourCastNet"
- From here, you have access to all the information needed to train and run FourCastNet by downloading the information from globus to your server. The only draw back is, the files are very large. 1 year's worth of information is 130 GB of data and the whole data set is 5T.

**6. Training your model** 

**7. Setting up inference.py** 

