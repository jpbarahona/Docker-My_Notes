## Dockerfile
Dockerfile will define what goes on in the environment inside your container. Access to resources like networking interfaces and disk drives is virtualized inside this environment, which is isolated from the rest of your system, so you have to map ports to the outside world, and be specific about what files you want to “copy in” to that environment. However, after doing that, you can expect that the build of your app defined in this Dockerfile will behave exactly the same wherever it runs.

```
# Use an official Python runtime as a parent image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

## Docker-commands

This creates a Docker image, which we’re going to tag using -t so it has a friendly name.

`docker build -t friendlyhello .`

Run the app, mapping your machine’s port 4000 to the container’s EXPOSEd port 80 using -p.

`docker run -p 4000:80 friendlyhello`

Now let’s run the app in the background, in detached mode.

`docker run -d -p 4000:80 friendlyhello`
