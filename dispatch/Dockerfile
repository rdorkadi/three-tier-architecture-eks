#Base image
FROM golang:latest

#sets working directory to /go/src/app
WORKDIR /go/src/app

#copying all the files from the current directory to the container
COPY *.go .

#initializes the go module and installs the dependencies
RUN go mod init dispatch && go get
RUN go install

#command to run when the container starts
CMD dispatch
