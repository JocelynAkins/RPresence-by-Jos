# RPresence-by-Jos
This is a work-in-progress to use RPresence to model occupancy for carnivore camera and trail transect data. The purpose is to have researchers contribute their coding knowledge to this conservation problem in a practical sense.

####Getting started with RPresence on mac
##I found I couldnt run RPresence on my mac because Presece.exe from the Presence GUI resides on the Parallels side of my computer as its only a Windows oeprating software
setwd("/Users/yourcomputersname/Foldername/myRfoler/myoccupancyfolder") #set working directory
PRES_FLDR<-"/Users/yourcomputersname/Foldername/myRfoler/myoccupancyfolder"
##Loading a package from source ; only have to do this once
install.packages("/Users/cascades/yourcomputersname/Foldername/myRfoler/myoccupancyfolder/RPresence_1.0.5.tar.gz", repos = NULL, type="source")  

###Getting started with RPresence on Windows

##Put RPresence_1.0.5.tar.gz (its in my email) in folder on Parallels: R – occupancy
##Load the RPresence package (RPresence_1.0.5.tar.gz) from source 
#(you only have to do this once)
install.packages("C:/Users/mycomputersname/Documents/myRfolder/myoccupancyfolder/RPresence_1.0.5.tar.gz", repos = NULL, type="source")  
##you should get output: DONE (RPresence)

# read in the csv data file of detections and covariates
mydata <- read.csv("filename.csv",stringsAsFactors=F ,header=T) 
# load in the detections
data <- mydata[,2:91]
# load in the covariates
sitecovars <- mydata[,92:105]
surveycovars <- mydata[,106:109]
# another way to load in the covariates
#sitecovars <- mydata[,c("veg", "year", "CALA")]
#create the pao
datapao <- create.pao(data = data, unitcov = sitecovars, survcov = surveycovars, paoname = "ninetydays.pao")
#the basic occupancy model – SO, no covariates
modelnocovars<-occ.mod(model=list(psi~1,p~1),data=datapao,unitcov = NULL, survcov = NULL,type="so")
#the basic occupancy model with covariates
modelwcovars<-occ.mod(model=list(psi~1,p~1),data=datapao,unitcov = sitecovars,survcov = surveycovars,type="so")
