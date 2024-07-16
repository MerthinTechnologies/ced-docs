**Using the Shell Deployment Agent**

This special CED agent provides the CED user with the ability to deploy a subsystem artifacts using custom scripts. The potential here is unlimited, as the user can choose the script interpreter of it preference, as well as consume all the CED connection and ecosystems properties, as other any CED subsystem can.

There are 3 major subsets of scripts, focused on the functionality:

*Provisioning Scripts:*

 - Recommended for the scripts dedicated to prepare the target platform (ie. create a new dyno in Heroku, if it doesn't exist)

   The execution of this section occurs first, including whenever a change is done to the subsystem settings

*Deployment Scripts:*

 - Core location of the scripts dedicated to exchange with an existent infrastructure and the deployment of the artifact versioned in the subsystem

   This subset is launched every time a version is published, as the artifact on the version is the intended object of the deployment actions been carried here

*Clean-up Scripts:*

 - Subset where clean-up scripts are located, if needed. Some platforms require (or recommend) the liberation of certain resources once the artifacts have been deployed. This is the right place to do that.

   

Important note: The 3 subsets are executed as distinct instances, so you should never configure inter-subset dependent task on your scripts. They're different points in the subsystem's life cycle.
