This repo contains files for use in the "Intro to serverless on Azure" course and the stand-alone lab that is used at the end of the course, titled "Lab - Deploy and Run Your First Azure Function"

You do not need any of these resources until the second half of the lab, when you extend the sample template code to address a real-world scenario.

When you get to the part in the lab diagram where you "Open the Console from Development Tools," open the console, return here, and follow the instructions, below. 

****These instructions are purposely vague for the benefit of those who are trying to complete the lab with minimal assistance. If you prefer step-by-step instructions, please refer to the lab guide and/or the solution video.

The console window will open at the root directory for the Function App you deployed, which hosts the function you created in the first half of the lab.
**You need to traverse to the function subdirectory (for example, "HttpTrigger1"), beneath the Function App directory. Then, inside of that sub-directory, create an empty file called, function.proj 

The command to do that is:
Copy nul function.proj

Important: This file *must* be in the function subdirectory beneath the function app directory.

There are two other files in this GitHub repository: One with the code you will use to populate the function.proj file you just created, and one that you will use to update the run.csx file in your function. Further instructions are in each of those files.
