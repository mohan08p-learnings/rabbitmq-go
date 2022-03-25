# RabbitMQ Go Implemntation

RabbitMQ is an open-source message broker that makes communication between services very easy. In particular, RabbitMQ uses a Publish/Subscribe pattern with an Advanced Message Queuing Protocol.

This reduces the load on web app servers and their delivery times because it efficiently delegates resource-intense tasks to third parties with no other tasks.

#### Pre-requisites

1. [Docker](https://x-team.com/blog/set-up-rabbitmq-with-docker-compose/#:~:text=the%20following%20installed%3A-,Docker,Go,-Setting%20Up%20Docker)

2. [Docker-compose](https://docs.docker.com/compose/)

3. [Go lang](https://golang.org/dl/)

#### Installing RabbitMQ using docker-compose

To start, create a folder called rabbitmq-go in your Golang project folder. Then, create a new file with the name docker-compose.yml. Inside that file, add the following:

Refer the `docker-compose.yml` file

Here's what we've just done:

`image:` where we tell Docker which image to pull. We're using an Alpine implementation of RabbitMQ with the management plugin. The Alpine distro is the one you'll want to use if you want to save disk space.

`container_name:` this represents the container created from the image above.
`ports:` the list of ports that will be mapped from the container to the outside world, for interacting with the queue and the web UI.

`volumes:` where we map the log and data from the container to our local folder. This allows us to view the files directly in their local folder structure instead of having to connect to the container.

`networks:` where we specify the network's name that the container will be using. This helps to separate container network configurations.

Now that we have this all set up, we can check if RabbitMQ is working correctly. Open a terminal, navigate to your rabbitmq-go folder and run `docker-compose up`

This command will pull the rabbitmq:3-management-alpine image, create the container rabbitmq and start the service and webUI. You should see something like this:

![RabbitMQ Application](/images/rabbitmq-init.PNG)

Once you see this, open your browser and head over to http://localhost:15672. You should see the RabbitMQ UI. Use guest as username and password.

![RabbitMQ Dashboard](/images/rabbitmq-dashboard.PNG)

#### Publishing a message with Go

Now that RabbitMQ is ready to Go, let's connect to it and send a message to the queue. But first, we need the amqp library. 
To install it, run the following command in your terminal: 

```
go get github.com/streadway/amqp.
```

As `go get` has deprecated in the latest version, you can use below command as an alternative to fetch the dependencies,

```
go mod init rabbitmq-go
go mod tidy
```

Then, create a filed called `sendMessage.go` inside the rabbitmq-go directory. Refer the same file from the current directroy.

![RabbitMQ Producer](/images/rabbitmq-producer.PNG)

See the rabbitmq dashbaord when the message has been produced by the producer,

![RabbitMQ Dashboard](/images/rabbitmq-dashboard1.PNG)

#### Consuming a message with Go

Create a file called `consumer.go`. Refer the same file from the current directroy.

![RabbitMQ Dashboard](/images/rabbitmq-consumer.PNG)

The beauty of using RabbitMQ is that you can send messages using Go, but read them with Python, JavaScript, PHP, Java, and more!

#### Learnings

You now know how to spin up a docker image, start RabbitMQ, dynamically send messages to the queue, and read messages from the queue. Voila! You have everything you need to create amazing applications that efficiently send and receive messages.

#### To Do

Dockerize both the producer and consumer application.