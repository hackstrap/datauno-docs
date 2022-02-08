# datauno-docs

# Datauno Documentation

Hi! Welcome to **Datauno Demo** documentation. This v1 of the demo makes it possible to deploy Jitsu, Clickhouse, Hue and Metabase in Kubernetes with a single command. The configuration is designed to work with Linode Kubernetes Engine (LKE).

# File Structure

datauno-demo folder consists of two sub-folders which are `frontend` and `kubernetes`. 

## `frontend` Folder

The `frontend` folder requires a standard web server which can serve static files. To easiest alternatives are:

1. Using Node.js run: `npx sirv-cli --port 3000`
2. Using Python run: `python3 -m http.server --port 3000`

Other than these two methods any static file serving web server should do the job. Examples are Nginx & Apache.

## `kubernetes` Folder

All the required files and configuration that are required for deploying Jitsu, Clickhouse, Hue and Metabase in Kubernetes exist in this directory.

# Tools Required

1. Latest version of Node.js (`>=17.x.x`)
2. Latest version of Kubernetes

# Getting Started

After ensuring the above stated tools are installed on your local machine, this demo is designed to be executed/hosted on Linode Kubernetes Engine (LKE). Run this else where at your own risk.

**Step 1 - Unzip the archive.**

Run the below command to `unzip` the provided ZIP archive.

```bash
unzip datauno-demo.zip
```

**Step 2 - Configuring `kubectl` command to connect with your cloud cluster.**

Please follow the following instructions from [Linode's documentation](https://www.linode.com/docs/guides/deploy-and-manage-a-cluster-with-linode-kubernetes-engine-a-tutorial/). To know how to apply this step. You can also follow the vendor specific steps if you're not intending to execute/deploy this demo onto Kubernetes.

**Step 3 - Deploying the demo on LKE.**

Enter into the unarchived folder by running 👇

```bash
cd datauno-demo
```

```bash
cd kubernetes
```

And then run the following command to create all the resources 👇

```
kubectl apply -k .
```

## Active Services

To get a list of active or running services use the following command:

```bash
kubectl get services -n datauno-demo
```

The output gives a table with the following coloumns:
- Service Name
- Service Type
- Cluster-IP
- External-IP
- Port(s)
- Age

## Pods

To get a list of active or running pods use the following command:

```bash
kubectl get pods -n datauno-demo
```
	
The output gives a table with the following coloumns:
- Pod Name
- Ready
- Status
- Restarts
- Age

## Web Application

**Step 1 - Starting the web application.**

The web application is a static website, requiring a static file serving web server like Apache, Nginx or any custom designed server like Hapi.js, Express or even a simple Python command would do.

To start the web application, firstly enter into the `frontend` directory, by running the following command 👇

```bash
cd frontend
```

Now start the a server server in this directory. See [top 👆](#frontend-folder) for some example commands.

> **Note:** Hue and Metabase will open is a new tab because of the `X-Frame-Options` header. Read more about [X-Frame-Options here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options).

## Logs

To check the logs of a pod:

```bash
kubectl logs -n datauno-demo --follow <pod_name>
```
# Delete Services

To delete all the pods and services:

```bash
kubectl delete -k .  
```
