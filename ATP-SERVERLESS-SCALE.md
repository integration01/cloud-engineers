# How to Scale Down ATP Scorage

We now (as of ECPU release) are encouraging customers to convert to or initiate ATP-Serverless instances using the ECPU model, which allows for less than 1 OCPU to be allocated. 
More importantly, the storage minimum for ATP is now in GB, instead of TB.  This means we can downsize any existing ATP instances to consume less storage.  Across hundreds of ATP instances,
this adds up quickly.  Now that we can reduce storage, this document will show how.

## Overall Process with Screen Shots

The process is simple.  Existing instances must be:
* Autonomous Transaction Processing - Serverless
* Running
* Not updating in any other way

To get to smaller storage, there are 2 steps that must be completed:
1) Convert to ECPU model (1 OCPU -> 4 ECPU)
2) After conversion, scale storage into GB, using an amount closer to what is needed

NOTE - Storage Auto-scaling can be enabled as well, so that if you exceed the allocated amount, more storage can be provisioned for the instance.

### Screen Shots

*Prior to migration*

![OCPU Model](images/1-ATP-S-OCPU.png)

*Migration Screen*

![ECPU Update](images/2-ATP-S-Update.png)

*After ECPU migration*

![After ECPU](images/3-ATP-S-After-Update.png)

*Scaling Down*

![Scale Down](images/4-ATP-S-Scale-Down.png)

*After Scaling*

![After Scale](images/5-ATP-S-After-Scale-Down.png)

*With Storage Auto-Scale (Optional)*

![Storage Scale](images/6-ATP-S-Auto-Scale-Storage.png)

