[[Container]] [[AI]]

# The Goal
The following are the goals of this hands-on:
1. Clone the Docker GenAI sample application repository to an EC2 instance 
2. Install Docker and Docker Compose on the Ubuntu server 
3. Configure the environment variables for the LLM, embedding model, and Neo4j database 
4. Build and run the containerized application using Docker Compose 
5. Test different LLM models (starting with orca-mini) to demonstrate the application's flexibility 6. Demonstrate error handling and troubleshooting scenarios

## Expected Outcome 
A functioning GenAI application that uses LangChain for orchestration, Streamlit for the UI, Ollama for running various LLM models, and Neo4j for vector storage, all running in Docker containers on an EC2 instance and accessible via web browser. 

A functioning containerized application where users can converse with PDF documents through natural language interactions, asking questions and receiving informed responses as if speaking with a knowledgeable person who has studied the material—moving beyond traditional keyword-based document search to a more intuitive, conversational experience for extracting information and insights from PDF content.

The exercise will provide practical experience switching between different LLM models (such as orca-mini, tinyllama, and others) to observe how model selection affects response quality, latency, and resource utilization. Through intentional error simulation, you will develop troubleshooting skills for common issues like container networking problems, configuration errors, and resource limitations—essential capabilities for managing containerized applications effectively.


What You Will Learn This exercise demonstrates how modern AI applications can be architected as microservices rather than monolithic applications, allowing teams to independently develop, deploy, and scale different components of AI systems. By working with this containerized solution, you'll gain handson experience with the architectural patterns increasingly adopted in enterprise AI deployments. You'll see how separating components like the language model (Ollama), vector database (Neo4j), and user interface (Streamlit) into distinct containers creates a flexible and maintainable system that can be modified and improved incrementally. You'll also experiment with different language models available through Ollama, observing how model selection impacts response quality, speed, and resource requirements. This hands-on comparison will help you understand the practical tradeoffs involved when selecting AI models PGP in Cloud Computing Try it out! V0.9 © Great Learning. All rights reserved. 3 for specific use cases. These troubleshooting scenarios provide valuable experience in diagnosing and addressing the kinds of issues that frequently arise when working with containerized AI applications in real-world environments.

## Industry Relevance and Practical 

### Knowledge Management & Document Processing:
● Organizations with large document repositories (legal firms, research institutions, healthcare providers) can deploy this solution to make their PDF-based knowledge accessible through natural language questions rather than keyword searches. 

● Employees can interact with complex technical documentation, policy manuals, or research papers by asking specific questions without reading entire documents.

### Enterprise Information Accessibility:
● Businesses can transform static PDF archives (annual reports, technical specifications, contracts) into interactive knowledge bases accessible to stakeholders without specialized training.

● This addresses the common challenge of information being "locked" in document formats that are difficult to query programmatically.

### Compliance and Regulatory Review:
● Financial institutions and regulated industries can use this system to quickly extract relevant information from lengthy regulatory documents and compliance guidelines.

● Legal teams can accelerate contract review by querying specific clauses or terms across multiple PDF agreements.

# TIO
## Launching a EC2 instance 
*EC2 specs*:
Ubuntu Server 22.04 LTS (HVM), SSD Volume Type
t3.xlarge(Family: t3 4 vCPU 16 GiB Memory)

40 gigs of storage 

*Network security group*
![[Pasted image 20250825172008.png]]


SSH and TCP 

## Launching a Vector Database Aura Instance
[neo4j - vector database](https://neo4j.com/)
- for free

After sign up - create instance 

Download text file provided when creating instance - this file contains the credentials 

user for this instance - `neo4j`
password for this instance - `kLKOyrya-LEjVn-7pNJM0p0ai6q5CdZu7shz_5JAXDA`

```
# Wait 60 seconds before connecting using these details, or login to https://console.neo4j.io to validate the Aura Instance is available
NEO4J_URI=neo4j+s://45f4516b.databases.neo4j.io
NEO4J_USERNAME=neo4j
NEO4J_PASSWORD=kLKOyrya-LEjVn-7pNJM0p0ai6q5CdZu7shz_5JAXDA
NEO4J_DATABASE=neo4j
AURA_INSTANCEID=45f4516b
AURA_INSTANCENAME=Free instance
```

instance UI:
![[Pasted image 20250825173640.png]]

## Setting up the EC2 instance to host containers
Ran this command:
`wget https://d6opu47qoi4ee.cloudfront.net/genAI/msad/containers/docker-genai-sample.zip`

then

```
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl 
unzip docker-genai-sample.zip curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Adding a repo:
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

```
sudo apt install -y docker-ce docker-ce-cli containerd.io
sudo apt install -y docker-compose-plugin sudo usermod -aG docker ${USER} newgrp docker 
exit 
exit
```

After we run all these commands we exit and re enter the instance so that permissions can take place

Then we cd inside the docker-gen-ai folder and open the file .env:

```
#*****************************************************************
# LLM and Embedding Model
#*****************************************************************

LLM=tinyllama  # or another smaller model like "orca-mini or Set to "gpt-3.5" to use OpenAI.
EMBEDDING_MODEL=sentence_transformer

#*****************************************************************
# Neo4j
#*****************************************************************
NEO4J_URI=neo4j+s://a952e199.databases.neo4j.io
NEO4J_USERNAME=neo4j
NEO4J_PASSWORD=sJajjOdPJrhnGdhAlACU-Wuhi1HFZSAb-cib_7o8yYg

#*****************************************************************
# Ollama
#*****************************************************************
OLLAMA_BASE_URL=http://ollama:11434
#*****************************************************************
# OpenAI
#*****************************************************************
# Only required when using OpenAI LLM or embedding model
# OpenAI charges may apply. For details, see 
# https://openai.com/pricing

#OPENAI_API_KEY=sk-..
```

We modify the .env file with out neo4j vector database credentials that we get from the text file we downloaded when creating the instance. 

![[Pasted image 20250825175427.png]]

after that we do:

`docker compose up -d`

```
docker exec -it $(docker ps -qf "name=ollama") ollama pull tinyllama
docker exec -it $(docker ps -qf "name=ollama") ollama list
```


by doing `http://EC2 public id:8000` you can access the streamlit web app 

![[Pasted image 20250825181539.png]]

It takes a bit to generate the response, but the more you use this the better it becomes at generating a response


