Lambda function + container

![[Pasted image 20250916160842.png]]

| Architecture Implementation                                                 |
| --------------------------------------------------------------------------- |
| Download the Dockerfile and the app code folder provided with this workbook |
| Package the web application as a Docker image running on Alpine with Python |
| Create an ECR repository and login to it.                                   |
| Build the image with the downloaded dockerfile and the support files        |
| Tag the image appropriately and push it into the ECR repository.            |
| Create a Lambda function with the image in ECR.                             |

# Creating an instance
Created a basic instance, downloaded docker and an image and then we created the image 

# Creating a ECR (Elastic Container Registry)
Created a private repo with default values 

The below screenshot contains the creation of the image, viewing of images created and the AWS push commands. 
![[Pasted image 20250916165744.png]]

After we run the push commands we get:
![[Pasted image 20250916165948.png]]


# Creating lambda function to test image
Created a lambda function that deploys a container image 

## Creating my own permissions
Since I need specific permissions to allow EC2s to run lambda functions I created my own permissions:
![[Pasted image 20250916180903.png]]