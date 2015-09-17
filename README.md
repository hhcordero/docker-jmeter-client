# JMeter Client (Non-gui)

Docker image for JMeter (non-gui client) running on Ubuntu. Make sure to open port 1099.

## Environment variables

Configure the following variables:

* FULL_PATH_OF_TEST_DIR - Full path for the test directory (eg. /home/user/load_tests)
* TEST_DIR - Parent directory for the test plan (eg. load_tests)
* TEST_PLAN - Test plan, **do not** put extension and must be inside $TEST_DIR (eg. test)
* IP - Public ip of the jmeter client machine
* REMOTE_HOSTS - Comma separated ip addresses for the jmeter servers

On JMeter Client machine, you need to provide the full path for the test directory. It will be mapped to /load_tests/$TEST_DIR inside the container.

## Usage
```sh
$   docker run \
        --detach \
        --publish 1099:1099 \
        --volume $FULL_PATH_OF_TEST_DIR:/load_tests/$TEST_DIR \
        --env TEST_DIR=$TEST_DIR \
        --env TEST_PLAN=$TEST_PLAN \
        --env IP=$IP \
        --env REMOTE_HOSTS=$REMOTE_HOSTS \
        hhcordero/docker-jmeter-client
```

Result will be saved as /load_tests/$TEST_DIR/$TEST_PLAN.jtl file. Download the result using scp.
