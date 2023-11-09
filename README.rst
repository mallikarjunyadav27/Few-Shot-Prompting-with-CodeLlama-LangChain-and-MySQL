LangChain SQLAgent Tutorial
This repository contains the code and instructions to connect a Large Language Model (LLM) to a PostgreSQL database using LangChain SQLAgent. With LangChain SQLAgent, you can create intricate chains of calls to language models and other tools to answer user questions about your database. This tutorial will guide you through the process of setting up the necessary components and executing queries to extract meaningful insights from your PostgreSQL database.

Prerequisites
Before you begin, make sure you have the following installed and set up:

PostgreSQL database
Python 3.x
pip package manager
Installation
Install the required packages using pip:

bash
Copy code
pip install langchain
pip install openai
pip install psycopg2
Setting up the Database Connection
Create a Python file called main.py.
Import the necessary modules:
python
Copy code
from langchain.agents import create_sql_agent
from langchain.agents.agent_toolkits import SQLDatabaseToolkit
from langchain.sql_database import SQLDatabase
from langchain.llms.openai import OpenAI
from langchain.agents import AgentExecutor
from langchain.agents.agent_types import AgentType
from langchain.chat_models import ChatOpenAI
Set up your PostgreSQL database connection URI:
python
Copy code
pg_uri = f"postgresql+psycopg2://{username}:{password}@{host}:{port}/{mydatabase}"
db = SQLDatabase.from_uri(pg_uri)
Setting up the LLM (Large Language Model)
Get your OpenAI API key and replace "your OpenAI key" with your actual API key:
python
Copy code
OPENAI_API_KEY = "your OpenAI key"
Define your LLM model:
python
Copy code
gpt = OpenAI(temperature=0, openai_api_key=OPENAI_API_KEY, model_name='gpt-3.5-turbo')
Setting up the Agent
Define the SQLDatabaseToolkit for your agent:
python
Copy code
toolkit = SQLDatabaseToolkit(db=db, llm=gpt)
Create your agent executor with AgentType ZERO_SHOT_REACT_DESCRIPTION:
python
Copy code
agent_executor = create_sql_agent(
    llm=gpt,
    toolkit=toolkit,
    verbose=True,
    agent_type=AgentType.ZERO_SHOT_REACT_DESCRIPTION,
)
Asking a Query
Define your question and execute the agent with the question:

python
Copy code
question = "Average rent in Chicago from Oct 2022 till Dec 2022"
agent_executor.run(question)
Results
The program will output the results of the executed query, providing insights from the PostgreSQL database based on the specified question.

Conclusion
LangChain SQLAgent is a powerful tool for constructing complex LLM chain calls to answer user questions about databases. While it can provide responses for most relevant questions, it may occasionally produce incorrect answers. It is essential to formulate precise questions and cross-verify the results with your database to ensure accuracy.

For more information and examples, please refer to the LangChain documentation and LangChain SQLAgent tutorial.
