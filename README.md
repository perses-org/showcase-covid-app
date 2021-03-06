[![10.5281/zenodo.4476672](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.4476672-blue.svg)](https://zenodo.org/record/4476672)
# Showcase Covid Mobile App

## Deployment Instructions


**Connect the mobile application to the MQTT server**: Both the mobile and cloud-side applications have to connect to an MQTT server to communicate with each other.
**Now it is connected to an active MQTT server [HiveMQ](https://www.hivemq.com/public-mqtt-broker/)**.
1. Access to:
`./app/src/main/java/com/spilab/percom21/service/MQTTConfiguration.java`

2. Introduce the IP/host and port of the MQTT server in the variable *MQTT_BROKER_URL*.
    ```sh
    public static String MQTT_BROKER_URL = "tcp://<ip/host>:<port>"; 
    ```
    
    
    
    

**Change the tests defined for Perses**
1. Access to:
`./perses.yml`

2.  Insert the IP and port where the server-side application has been deployed in **tests**, *url* field.
    ```sh
    tests:
      - id: "GUI Performance"
        type: "espresso"
      - id: "Observed Performance1"
        type: "apipecker"
        config:
          concurrentUsers: 3
          iterations: 5
          delay: 500
          url: "http://<ip>:<port>/risk?device=Device1"
        expect:
          mean:
            under: 2000
      - id: "Observed Performance2"
        type: "apipecker"
        config:
          concurrentUsers: 6
          iterations: 8
          delay: 500
          url: "http://<ip>:<port>/risk?device=Device2"
        expect:
          mean:
            under: 2000
    ```

Make changes to this file to commit and run Perses
