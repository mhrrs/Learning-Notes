# Description: Notes on how to store env variables in a production environment

# What is an environment variable?:
- an env var is a variable that lives outside of the python code and within the OS.
- - so on startup when docker injects env variables from the .env file (which can only be read by root), the program ingests them as well

When using env variables in fastapi with a docker setup, you create a schema using pydantic. 

################### settings.py ###############
from pydantic import BaseSettings

class Settings(BaseSettings):
    database_url: str
    secret_key: str
    sentry_dsn: str

    class Config:
        env_file = '.env'

settings = Settings()
###############################################


On startup of the application, the python program creates an instance of the Settings class and the docker program will feed this variable the .env variables.
--> Your secrets are now safe because they are living as in-memory variables. There is no explicit reference to any of your .env variables in the program EVER.


