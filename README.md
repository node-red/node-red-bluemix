node-red-bluemix
================

A wrapper for deploying [Node-RED](http://nodered.org) into the [IBM Cloud](http://bluemix.net) platform.


### What is IBM Cloud?

IBM Cloud is an implementation of IBM's Open Cloud Architecture, built on Cloud Foundry.

To sign-up for a free trial, head on over [here](http://www.bluemix.net).

### Node-RED on IBM Cloud

This repository provides two things.

1. a wrapper to Node-RED that is suitable for deploying your own instance into IBM Cloud - under the `public/app` directory

2. a node.js application that serves this up as a quick-start boilerplate into the IBM Cloud dashboard.

### Deploying Node-RED into IBM Cloud

The quick way to do this is to log into the [IBM Cloud dashboard](http://www.bluemix.net) and select Node-RED Starter from the list of Boilerplates.

To manually deploy an instance, the steps can be taken.

This assumes you already have the `cf` tool [installed](http://www.ng.bluemix.net/docs/BuildingWeb.jsp#install-cf) and logged into IBM Cloud.

1. Decide what you want to call your application. For this example, let's go with `nr-fred`.
2. Via the IBM Cloud dashboard, create an instance of Cloudant NoSQL DB called: `nr-fred:cloudantNoSQLDB`
3. Create the file `public/app/manifest.yml`, with the following contents, updated to reflect your chosen name:

   ```
    ---
    applications:
    - name: nr-fred
      memory: 256M
      command: node node_modules/node-red/red.js --settings ./bluemix-settings.js
      services:
      - nr-fred:cloudantNoSQLDB
   ```
4. From within the `public/app` directory, run:
   ```
    $ cf push
    ```

5. Once deployed, you can access your instance of Node-RED at <https://nr-fred.ng.bluemix.net>.
