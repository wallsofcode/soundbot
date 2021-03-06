# SoundBot
SoundBot is a containerized soundboard for Discord. The soundbot image is hosted on [Dockerhub](https://hub.docker.com/repository/docker/wallsofcode/soundbot).
It can be pulled to your local machine by running _"docker pull wallsofcode/soundbot"_.

## How to use SoundBot
Build and run the docker container with the following environment variables set:
* SOUNDBOT_TOKEN: The API token of the bot retrieved from the [Discord Developers Portal](https://discord.com/developers/applications)
* SOUNDBOT_PREFIX: The command prefix for the soundboard. The default is ';'.
* SOUNDBOT_ACTIVITY: The activity string for the bot user. This defaults to the help message.

If docker-compose is your cup of tea, I've included a very simple example file named _example-soundbot-compose.yaml_ 
which will get you up and running quickly. Make sure to change your API token in the file!

## Adding Sounds
Begin by collecting MP3 sounds you would like to use in the SoundBot in a folder. 

Standalone Docker Deployment:
* Mount the folder as a volume to "/app/soundboard" in the container. _(docker run --volume ./sounds:/app/soundboard wallsofcode/soundbot)_

Kubernetes Deployment:
* Create a volume and populate it through kubectl. _(kubectl cp ./sounds your-soundbot-pod:/app/soundboard)_
  This method can be done with an emptyDir without problems, however a PVC is better as it will persist the data.  


## Notes
* The basename of the file is what will be used as the command name. For example, if a file is 
  named "hello.mp3", then the command will be the bot prefix + "hello".
