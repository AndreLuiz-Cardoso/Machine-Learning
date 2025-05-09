# AI-900-MachineLearning

Training for certification Azure Basically, I used the same step-by-step procedure demonstrated on the Azure website (https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html) 

# Building the environment

In the panel titled "Basics", in the "Resource Details" section, the signature corresponding to the charge was entered in the field designated as "Signature". Subsequently, the "Resource Group" that will incorporate the resource to be created was specified.

Then, in the "Workspace Details" section, the details of the workspace to be established were provided.

As it was a laboratory, the settings applied were minimal. Finally, the resource was created by selecting the "Query + Create" option. After validation passed, I clicked "Create".


After the resource was established, I clicked the "Go to Resource" button, in the second interface I started the studio, whose function is to redirect to the Azure Machine Learning studio.

# Sending the data

I used: https://aka.ms/bike-rentals as per the procedure on the Azure website determined. In the "Settings" step, I filled in the set settings and when going to the "Schema" option, I checked the data types. Finally, by clicking "Next", I checked the settings created for the data asset and then clicked the "Create" button.

In the "Task Settings" section, I selected the previously imported dataset. Later, in the "Target Column" option, I designated the "rentals" column as the target.

In the "Limit" section, the values were inserted as shown in the image below. After that, I activated the "Enable Early Termination" option.

On the "Validate and test" page, in the "Validation type" option, I chose "Training validation division".

# Issues

I had some problems with the data type, because I put the wrong option, I put table instead of tubular. After fixing this part, everything went fine.
